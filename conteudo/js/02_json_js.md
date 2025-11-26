# Guia Prático de JSON em JavaScript

JSON (JavaScript Object Notation) é um formato de texto leve para intercâmbio de dados. Pense nele como a "língua" que aplicações web usam para conversar. Embora se pareça com um objeto JavaScript, **JSON é sempre um texto (string)**.

Em JavaScript, temos duas funções principais para trabalhar com JSON:
- `JSON.parse()`: Converte uma string JSON em um objeto JavaScript.
- `JSON.stringify()`: Converte um objeto JavaScript em uma string JSON.

---

## 1. Convertendo entre Objeto e JSON

### De Objeto JavaScript para String JSON (`stringify`)

Para enviar dados para um servidor ou salvá-los em um arquivo, você precisa converter seu objeto em uma string.

```js
const usuario = {
    id: 1,
    nome: "Ana",
    ativo: true
};

// Converte o objeto para uma string JSON compacta
const jsonString = JSON.stringify(usuario);
console.log(jsonString); // Saída: '{"id":1,"nome":"Ana","ativo":true}'

// Para facilitar a leitura (debug), podemos "embelezar" o JSON
// O 'null, 2' formata a string com 2 espaços de indentação
const jsonFormatado = JSON.stringify(usuario, null, 2);
console.log(jsonFormatado);
/* Saída:
{
  "id": 1,
  "nome": "Ana",
  "ativo": true
}
*/
```

### De String JSON para Objeto JavaScript (`parse`)

Quando você recebe dados de uma API, eles chegam como uma string JSON. Para poder usar esses dados no seu código (ex: `dados.nome`), você precisa convertê-los em um objeto.

**Importante:** A conversão pode falhar se a string não for um JSON válido. Por isso, é uma boa prática usar um bloco `try...catch`.

```js
const jsonRecebido = '{"nome":"Carlos","idade":35}';

try {
    const dados = JSON.parse(jsonRecebido);
    console.log(dados.nome);   // Saída: "Carlos"
    console.log(dados.idade);  // Saída: 35
} catch (erro) {
    console.error("Erro ao processar o JSON:", erro.message);
}
```

---

## 2. Validando e Manipulando JSON

Antes de usar um JSON, é importante validá-lo. Use ferramentas como [jsonlint.com](https://jsonlint.com) para verificar a estrutura.

### Exemplo: Validando e Manipulando JSON
```javascript
const jsonString = '{ "nome": "Ana", "idade": 28 }';

try {
    const objeto = JSON.parse(jsonString);
    console.log(objeto.nome); // Ana

    // Adicionando uma nova propriedade
    objeto.ativo = true;
    console.log(JSON.stringify(objeto));
} catch (error) {
    console.error('JSON inválido:', error);
}
```

---

## 3. Usando JSON com APIs (Fetch)

A principal aplicação de JSON é na comunicação com APIs.

### Recebendo Dados (GET)

O método `.json()` da resposta do `fetch` é um atalho que lê o corpo da resposta e já faz o `JSON.parse()` para você.

```js
async function buscarUsuarios() {
    try {
        const resposta = await fetch('https://api.exemplo.com/usuarios');
        if (!resposta.ok) {
            throw new Error(`Erro HTTP: ${resposta.status}`);
        }
        const usuarios = await resposta.json(); // Converte a resposta em objeto/array
        console.log(usuarios);
        return usuarios;
    } catch (erro) {
        console.error("Falha ao buscar usuários:", erro);
    }
}
```

### Enviando Dados (POST)

Ao enviar dados, você faz o processo inverso: converte seu objeto para string com `JSON.stringify` e informa ao servidor que está enviando JSON através do cabeçalho `Content-Type`.

```js
async function criarUsuario(novoUsuario) {
    try {
        const resposta = await fetch('https://api.exemplo.com/usuarios', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json', // Essencial!
            },
            body: JSON.stringify(novoUsuario), // Converte o objeto para string
        });

        if (!resposta.ok) {
            throw new Error(`Erro HTTP: ${resposta.status}`);
        }
        const usuarioCriado = await resposta.json();
        console.log("Usuário criado:", usuarioCriado);
        return usuarioCriado;
    } catch (erro) {
        console.error("Falha ao criar usuário:", erro);
    }
}

// Exemplo de uso
criarUsuario({ nome: 'Beatriz', email: 'bia@exemplo.com' });
```

### Exemplo com `fetch`

Ao consumir APIs, o JSON é o formato mais comum para enviar e receber dados.
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

---

## 4. Manipulando os Dados Recebidos

Uma vez que você tem o objeto JavaScript, pode usar todos os recursos da linguagem para manipulá-lo.

### Acesso Seguro a Propriedades

Dados de APIs podem não ter a estrutura que você espera. Use o **Optional Chaining (`?.`)** para evitar erros ao acessar propriedades aninhadas que podem não existir. Use o **Nullish Coalescing (`??`)** para fornecer um valor padrão.

```js
const usuario = {
    nome: "Ana",
    endereco: {
        rua: "Rua Principal, 123"
        // cidade não existe
    }
};

// Sem acesso seguro, isso daria um erro:
// const cidade = usuario.endereco.cidade.toUpperCase(); // Erro!

// Com acesso seguro:
const cidade = usuario.endereco?.cidade ?? 'Cidade não informada';
console.log(cidade); // Saída: "Cidade não informada"
```

### Transformação de Arrays

É muito comum receber arrays de objetos e precisar transformá-los.

```js
const produtos = [
    { id: 1, nome: 'Laptop', categoria: 'Eletrônicos', preco: 5000 },
    { id: 2, nome: 'Mouse', categoria: 'Eletrônicos', preco: 150 },
    { id: 3, nome: 'Cadeira', categoria: 'Móveis', preco: 800 },
];

// Filtrar: pegar apenas os eletrônicos
const eletronicos = produtos.filter(p => p.categoria === 'Eletrônicos');

// Mapear: criar um novo array apenas com os nomes e preços
const nomesEPrecos = produtos.map(p => ({ nome: p.nome, preco: p.preco }));

// Reduzir: calcular o valor total do estoque
const valorTotal = produtos.reduce((total, p) => total + p.preco, 0);
console.log(valorTotal); // Saída: 5950
```

---

## 5. Pontos de Atenção (Armadilhas Comuns)

- **Sintaxe Rígida**: JSON exige aspas duplas `"` em chaves e strings. Vírgulas no final de listas ou objetos (`trailing commas`) são proibidas. Comentários não são permitidos.
- **Tipos de Dados Perdidos**: `JSON.stringify` omite `undefined`, funções e símbolos. `NaN` e `Infinity` são convertidos para `null`.
- **Datas viram Strings**: Objetos `Date` são convertidos para strings no formato ISO 8601. Para tê-los de volta como `Date`, você precisa convertê-los manualmente após o `JSON.parse`.
- **Clone Profundo Limitado**: `JSON.parse(JSON.stringify(obj))` é um truque para clonagem profunda, mas falha com os tipos de dados mencionados acima (Date, undefined, etc.). Use com cautela.
- **BigInt**: Não é suportado nativamente por JSON.
