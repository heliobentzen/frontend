# Manipulando APIs com `fetch`

A API `fetch` é uma interface moderna do JavaScript para realizar requisições de rede (HTTP), como buscar dados de um servidor. Ela é baseada em Promises e oferece uma alternativa mais poderosa e flexível ao `XMLHttpRequest`.

## O que é uma API?

API (Application Programming Interface) é um conjunto de regras e definições que permite que diferentes aplicações se comuniquem entre si. No contexto web, usamos APIs para buscar ou enviar dados para um servidor sem precisar recarregar a página.

Usaremos a [JSONPlaceholder](https://jsonplaceholder.typicode.com/), uma API gratuita para testes e prototipagem.

## Realizando Requisições `GET`

A requisição mais comum é a `GET`, usada para solicitar dados de um recurso específico.

O `fetch` retorna uma *Promise*. Uma *Promise* é um objeto que representa a eventual conclusão (ou falha) de uma operação assíncrona.

```javascript
// A URL da API para a qual faremos a requisição
const apiUrl = 'https://jsonplaceholder.typicode.com/posts/1';

fetch(apiUrl)
    .then(response => {
        // O primeiro .then() recebe o objeto Response.
        // Precisamos converter o corpo da resposta para JSON.
        // O método .json() também retorna uma Promise.
        return response.json();
    })
    .then(data => {
        // O segundo .then() recebe os dados já convertidos.
        console.log('Dados recebidos:', data);
        // Exemplo de como usar os dados:
        // document.body.innerHTML = `<h1>${data.title}</h1><p>${data.body}</p>`;
    })
    .catch(error => {
        // O .catch() é executado se ocorrer um erro de rede.
        console.error('Houve um problema com a requisição fetch:', error);
    });
```

### Tratando Erros de HTTP

Por padrão, o `fetch` só rejeita a *Promise* em caso de falha de rede. Respostas com códigos de erro HTTP (como 404 - Não Encontrado ou 500 - Erro Interno do Servidor) não são consideradas falhas de rede.

Para tratar esses casos, verificamos a propriedade `response.ok`, que é `true` se o status da resposta estiver na faixa de 200-299.

```javascript
fetch('https://jsonplaceholder.typicode.com/posts/9999') // Post inexistente
    .then(response => {
        if (!response.ok) {
            // Se a resposta não for "ok", lançamos um erro para ser pego pelo .catch()
            throw new Error(`Erro HTTP! Status: ${response.status}`);
        }
        return response.json();
    })
    .then(data => {
        console.log(data);
    })
    .catch(error => {
        console.error('Erro:', error);
    });
```

## Realizando Requisições `POST`

Para enviar dados para um servidor (criar um novo recurso), usamos o método `POST`. Para isso, passamos um segundo argumento para o `fetch`: um objeto de configuração.

```javascript
const newPost = {
    title: 'Meu Novo Post',
    body: 'Este é o conteúdo do meu novo post.',
    userId: 1,
};

fetch('https://jsonplaceholder.typicode.com/posts', {
    method: 'POST', // Método HTTP
    headers: {
        // Cabeçalhos da requisição
        'Content-Type': 'application/json; charset=UTF-8',
    },
    body: JSON.stringify(newPost), // Corpo da requisição, convertido para string JSON
})
    .then(response => response.json())
    .then(data => {
        console.log('Post criado com sucesso:', data);
    })
    .catch(error => {
        console.error('Erro ao criar o post:', error);
    });
```

## 3. Métodos HTTP com `fetch`

Além de `GET`, o `fetch` suporta outros métodos HTTP como `POST`, `PUT` e `DELETE`.

### Exemplo: Enviando Dados com `POST`

```javascript
fetch('https://jsonplaceholder.typicode.com/posts', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json'
    },
    body: JSON.stringify({ titulo: 'Novo Post', conteudo: 'Conteúdo do post' })
})
    .then(response => response.json())
    .then(data => console.log('Post criado:', data))
    .catch(error => console.error('Erro:', error));
```

### Exemplo: Atualizando Dados com `PUT`

```javascript
fetch('https://jsonplaceholder.typicode.com/posts/1', {
    method: 'PUT',
    headers: {
        'Content-Type': 'application/json'
    },
    body: JSON.stringify({ titulo: 'Post Atualizado', conteudo: 'Conteúdo atualizado' })
})
    .then(response => response.json())
    .then(data => console.log('Post atualizado:', data))
    .catch(error => console.error('Erro:', error));
```

## Usando `async/await`

`async/await` é uma sintaxe mais moderna e legível para trabalhar com *Promises*. Ela permite escrever código assíncrono que se parece com código síncrono.

Para usar `await`, a função que o contém deve ser declarada com a palavra-chave `async`.

### Exemplo `GET` com `async/await`

```javascript
const getPost = async (postId) => {
    try {
        const response = await fetch(`https://jsonplaceholder.typicode.com/posts/${postId}`);

        if (!response.ok) {
            throw new Error(`Erro HTTP! Status: ${response.status}`);
        }

        const data = await response.json();
        console.log('Dados do post:', data);
    } catch (error) {
        console.error('Erro ao buscar o post:', error);
    }
};

// Chamando a função
getPost(2);
```

### Exemplo `POST` com `async/await`

```javascript
const createPost = async (postData) => {
    try {
        const response = await fetch('https://jsonplaceholder.typicode.com/posts', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json; charset=UTF-8',
            },
            body: JSON.stringify(postData),
        });

        if (!response.ok) {
            throw new Error(`Erro HTTP! Status: ${response.status}`);
        }

        const data = await response.json();
        console.log('Post criado:', data);
    } catch (error) {
        console.error('Erro ao criar o post:', error);
    }
};

// Dados do novo post
const myNewPost = {
    title: 'Usando async/await',
    body: 'O código fica mais limpo!',
    userId: 5,
};

// Chamando a função
createPost(myNewPost);
```

## Trabalhando com Múltiplas Promises

Às vezes, precisamos lidar com várias requisições assíncronas ao mesmo tempo. O objeto `Promise` oferece métodos estáticos para orquestrar múltiplas promises, como `Promise.all` e `Promise.race`.

### `Promise.all`

`Promise.all` recebe um array de promises e retorna uma única promise. Essa nova promise é resolvida quando **todas** as promises no array são resolvidas. O valor resolvido é um array com os resultados de cada promise, na mesma ordem.

Se **qualquer uma** das promises for rejeitada, `Promise.all` é imediatamente rejeitado com o motivo da primeira promise que falhou.

É útil quando você precisa dos resultados de várias chamadas de API antes de continuar.

```javascript
const fetchMultiplePosts = async () => {
    try {
        const urls = [
            'https://jsonplaceholder.typicode.com/posts/1',
            'https://jsonplaceholder.typicode.com/posts/2',
            'https://jsonplaceholder.typicode.com/posts/3'
        ];

        // Cria um array de promises de fetch
        const promises = urls.map(url => fetch(url).then(res => res.json()));

        // Espera todas as promises serem resolvidas
        const posts = await Promise.all(promises);

        console.log('Todos os posts foram recebidos:', posts);
        // posts é um array com os 3 objetos de post
    } catch (error) {
        console.error('Uma das requisições falhou:', error);
    }
};

fetchMultiplePosts();
```

### `Promise.race`

`Promise.race` também recebe um array de promises, mas retorna uma promise que é resolvida ou rejeitada assim que a **primeira** promise do array for resolvida ou rejeitada.

É útil para cenários de "corrida", como buscar um recurso de múltiplos servidores espelhados e usar a resposta do que responder primeiro, ou para implementar um timeout para uma requisição.

#### Exemplo: Implementando um Timeout

```javascript
const fetchWithTimeout = async (url, timeoutMs) => {
    // Cria uma promise que rejeita após um tempo
    const timeoutPromise = new Promise((_, reject) => {
        setTimeout(() => {
            reject(new Error(`A requisição excedeu o tempo limite de ${timeoutMs}ms`));
        }, timeoutMs);
    });

    try {
        // "Corre" a requisição fetch contra a promise de timeout
        const response = await Promise.race([
            fetch(url),
            timeoutPromise
        ]);

        if (!response.ok) {
            throw new Error(`Erro HTTP! Status: ${response.status}`);
        }

        const data = await response.json();
        console.log('Dados recebidos a tempo:', data);
    } catch (error) {
        console.error('Ocorreu um erro:', error.message);
    }
};

// Tenta buscar um post com um timeout de 500ms
fetchWithTimeout('https://jsonplaceholder.typicode.com/posts/4', 500);
```

## 4. Criando Hooks Customizados para `fetch`

Reutilize lógica de chamadas à API com hooks customizados.

### Exemplo: `useFetch`

```javascript
import { useState, useEffect } from 'react';

function useFetch(url) {
    const [data, setData] = useState(null);
    const [loading, setLoading] = useState(true);
    const [error, setError] = useState(null);

    useEffect(() => {
        setLoading(true);
        fetch(url)
            .then(response => {
                if (!response.ok) {
                    throw new Error('Erro na requisição');
                }
                return response.json();
            })
            .then(data => setData(data))
            .catch(error => setError(error))
            .finally(() => setLoading(false));
    }, [url]);

    return { data, loading, error };
}

export default useFetch;
```