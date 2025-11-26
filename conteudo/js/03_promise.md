# Promises em JavaScript: A Base para a Reatividade

Promises são um conceito fundamental em JavaScript moderno para lidar com operações assíncronas. Elas representam um valor que pode estar disponível agora, no futuro ou nunca. Para quem pretende trabalhar com bibliotecas como o React, dominar Promises é essencial, pois a busca de dados de APIs é uma das tarefas mais comuns em aplicações web dinâmicas.

## 1. O Problema: Callback Hell

Antes das Promises, o código assíncrono era frequentemente escrito com funções de callback aninhadas, levando a um padrão difícil de ler e manter, conhecido como "Callback Hell" ou "Pirâmide da Perdição".

```javascript
// Exemplo de Callback Hell
primeiraFuncao(args, function(resultado1) {
    segundaFuncao(resultado1, function(resultado2) {
        terceiraFuncao(resultado2, function(resultado3) {
            // E assim por diante...
            console.log('Resultado final:', resultado3);
        });
    });
});
```

## 2. O que é uma Promise?

Uma `Promise` é um objeto que representa a eventual conclusão (ou falha) de uma operação assíncrona e seu valor resultante.

Uma Promise pode estar em um destes três estados:

*   **Pendente (Pending):** Estado inicial, nem cumprida, nem rejeitada.
*   **Cumprida (Fulfilled):** A operação foi concluída com sucesso.
*   **Rejeitada (Rejected):** A operação falhou.

## 3. Criando uma Promise

Você cria uma Promise usando o construtor `new Promise()`, que recebe uma função (o "executor") com dois argumentos: `resolve` e `reject`.

*   `resolve(value)`: Chamada quando a operação é bem-sucedida.
*   `reject(error)`: Chamada quando ocorre um erro.

```javascript
const minhaPromise = new Promise((resolve, reject) => {
    const sucesso = true; // Simula uma operação que pode dar certo ou errado

    setTimeout(() => {
        if (sucesso) {
            resolve("Operação concluída com sucesso!");
        } else {
            reject("A operação falhou.");
        }
    }, 2000); // Simula um atraso de 2 segundos
});
```

## 4. Consumindo uma Promise

Para consumir o valor de uma promise, usamos os métodos `.then()`, `.catch()` e `.finally()`.

*   **.then(onFulfilled):** Executa quando a promise é resolvida (cumprida). Recebe o valor passado para `resolve()`.
*   **.catch(onRejected):** Executa quando a promise é rejeitada. Recebe o erro passado para `reject()`.
*   **.finally():** Executa sempre ao final, seja a promise resolvida ou rejeitada.

```javascript
console.log("Iniciando a operação...");

minhaPromise
    .then((mensagem) => {
        console.log("Sucesso:", mensagem); // Será executado se a promise for resolvida
    })
    .catch((erro) => {
        console.error("Erro:", erro); // Será executado se a promise for rejeitada
    })
    .finally(() => {
        console.log("Operação finalizada."); // Será executado de qualquer forma
    });
```

## 5. Encadeamento (Chaining)

O método `.then()` sempre retorna uma nova Promise, o que nos permite encadear várias operações assíncronas em sequência de forma legível. Isso é útil para fluxos de dados onde uma requisição depende do resultado da anterior.

```javascript
function buscarDados() {
    return new Promise((resolve) => {
        setTimeout(() => resolve({ id: 1, nome: "Usuário" }), 1000);
    });
}

function buscarPedidos(usuario) {
    return new Promise((resolve) => {
        setTimeout(() => resolve([ 'Pedido 1', 'Pedido 2' ]), 1000);
    });
}

buscarDados()
    .then((usuario) => {
        console.log("Usuário encontrado:", usuario.nome);
        return buscarPedidos(usuario); // Retorna a próxima promise
    })
    .then((pedidos) => {
        console.log("Pedidos:", pedidos);
    })
    .catch((erro) => {
        console.error("Ocorreu um erro na cadeia:", erro);
    });
```

## 6. Métodos Estáticos de Promise

Existem métodos úteis no próprio construtor `Promise`:

*   `Promise.all(iterable)`: Espera que **todas** as promises do iterável sejam resolvidas. Se uma for rejeitada, a promise retornada é imediatamente rejeitada. Muito útil em React para carregar dados de múltiplas fontes antes de renderizar um componente.
*   `Promise.race(iterable)`: Retorna uma promise que resolve ou rejeita assim que a **primeira** promise do iterável resolver ou rejeitar.
*   `Promise.allSettled(iterable)`: Espera que todas as promises sejam concluídas (resolvidas ou rejeitadas) e retorna um array com o estado de cada uma.

```javascript
const p1 = Promise.resolve(3);
const p2 = 42;
const p3 = new Promise((resolve) => setTimeout(resolve, 100, 'foo'));

Promise.all([p1, p2, p3]).then((values) => {
    console.log(values); // [3, 42, "foo"]
});
```

## 7. `async/await`: Uma Alternativa às Promises

O `async/await` simplifica o uso de Promises, tornando o código mais legível.

### Exemplo
```javascript
async function buscarDados() {
    try {
        const resposta = await fetch('https://jsonplaceholder.typicode.com/posts/1');
        const dados = await resposta.json();
        console.log('Dados recebidos:', dados);
    } catch (erro) {
        console.error('Erro ao buscar dados:', erro);
    }
}

buscarDados();
```

### Comparação com Promises
```javascript
// Com Promises
fetch('https://jsonplaceholder.typicode.com/posts/1')
    .then(res => res.json())
    .then(data => console.log(data))
    .catch(err => console.error(err));

// Com async/await
async function exemplo() {
    try {
        const res = await fetch('https://jsonplaceholder.typicode.com/posts/1');
        const data = await res.json();
        console.log(data);
    } catch (err) {
        console.error(err);
    }
}
```

## 8. Promises no Contexto do React

Em React, a busca de dados de uma API é um "efeito colateral" (side effect), gerenciado pelo hook `useEffect`. A API `fetch` do navegador, que retorna uma Promise, é comumente usada para isso.

O padrão mais comum é criar uma função `async` *dentro* do `useEffect` e chamá-la imediatamente. Isso é necessário porque o próprio `useEffect` não deve ser `async`.

Vamos ver um exemplo conceitual de como buscar dados em um componente React, gerenciando os estados de carregamento, erro e sucesso.

```jsx
// Exemplo de um componente React funcional (pseudo-código)
import React, { useState, useEffect } from 'react';

function PerfilUsuario({ id }) {
    // 1. Estados para gerenciar os dados, carregamento e erros
    const [usuario, setUsuario] = useState(null);
    const [loading, setLoading] = useState(true);
    const [error, setError] = useState(null);

    // 2. useEffect para buscar os dados quando o componente montar ou o 'id' mudar
    useEffect(() => {
        // 3. Função async interna para usar await
        const fetchData = async () => {
            try {
                // Inicia o carregamento
                setLoading(true);
                setError(null);

                // A API fetch retorna uma Promise
                const response = await fetch(`https://api.exemplo.com/users/${id}`);
                
                if (!response.ok) {
                    // Se a resposta não for OK (ex: 404, 500), lança um erro
                    throw new Error(`HTTP error! status: ${response.status}`);
                }

                // O método .json() também retorna uma Promise
                const data = await response.json();

                // 4. Sucesso: atualiza o estado com os dados
                setUsuario(data);
            } catch (e) {
                // 5. Erro: atualiza o estado de erro
                setError(e.message);
            } finally {
                // 6. Finalização: para de carregar, independentemente do resultado
                setLoading(false);
            }
        };

        fetchData(); // Chama a função para iniciar a busca

    }, [id]); // O array de dependências garante que o efeito rode novamente se o 'id' mudar

    // 7. Renderização condicional baseada nos estados
    if (loading) return <div>Carregando...</div>;
    if (error) return <div>Erro: {error}</div>;
    if (!usuario) return null;

    return (
        <div>
            <h1>{usuario.nome}</h1>
            <p>{usuario.email}</p>
        </div>
    );
}
```

Entender este padrão é crucial, pois ele combina o poder das Promises (`fetch`, `async/await`) com os hooks do React (`useState`, `useEffect`) para criar componentes reativos e robustos que interagem com fontes de dados externas.