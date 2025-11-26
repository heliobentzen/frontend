# Introdução a JavaScript e Lógica de Programação

A linguagem JavaScript começou como um script de 10 dias para fazer botões piscarem em navegadores e agora... bem, agora ela domina o mundo. Do seu celular à sua geladeira, o JS está lá, silenciosamente julgando suas escolhas de lanches.

Prepare-se para uma jornada divertida através de lógica, esquisitices e um poder imenso. Vamos decifrar esses códigos juntos!

---

## 1. O que é JavaScript?
JavaScript é a linguagem de programação que dá vida à web. Originalmente para navegadores, hoje ela está em todos os lugares: servidores (Node.js), aplicativos de celular, e até em dispositivos inteligentes.

É uma linguagem **multiparadigma**, ou seja, flexível. Você pode escrever código de forma direta (imperativa), focada em transformações de dados (funcional) ou organizando tudo em "caixas" lógicas (orientada a objetos). O JavaScript moderno (ES6+) incentiva boas práticas, como usar `let`/`const` em vez de `var`, e criar código modular e reutilizável.

## 2. Ambiente Rápido para Testes
Você não precisa de nada complexo para começar. Use o console do seu navegador (F12) ou instale o Node.js e digite no seu terminal:
```bash
node
```
Isso abre um ambiente interativo (REPL) onde você pode digitar código JS e ver o resultado na hora.

---

## 3. Tipos de Dados: Os Blocos de Construção

### 3.1 Tipos Primitivos (Valores Imutáveis)
Pense neles como os "átomos" da informação: valores únicos que não podem ser alterados.

- `string`: Texto, sempre entre aspas. Ex: `"Olá, mundo!"`
- `number`: Qualquer número, inteiro ou com casas decimais. Ex: `42`, `3.14`
- `bigint`: Para números inteiros gigantescos. Ex: `9007199254740993n`
- `boolean`: Verdadeiro (`true`) ou falso (`false`).
- `null`: Representa a ausência intencional de um valor. É um "nada" definido por você.
- `undefined`: Uma variável que foi declarada, mas ainda não recebeu um valor.
- `symbol`: Um identificador único, útil para chaves de objeto especiais.

```js
const nome = "Ana";          // string
const idade = 28;            // number
const ativo = true;          // boolean
let itemSelecionado = null;  // null (intencionalmente vazio)
let preco;                   // undefined (ainda não definido)
```

### 3.2 Objetos (Valores de Referência)
Objetos são como "caixas" que agrupam dados. Eles são mutáveis e, quando você copia um objeto, na verdade está copiando a "referência" (o endereço) para a mesma caixa.

```js
// Um objeto literal que descreve uma pessoa
const pessoa = { nome: "Ana", idade: 28 };

// Um array (um tipo especial de objeto para listas)
const numeros = [1, 2, 3];

// Uma função (também é um objeto em JS!)
function somar(a, b) { return a + b; }

// Cuidado com a referência!
const objA = { valor: 1 };
const objB = objA; // objB aponta para o MESMO objeto que objA

objB.valor = 99;
console.log(objA.valor); // Saída: 99 (alterar objB afetou objA)
```

### 3.3 Verificando Tipos
```js
typeof "Olá";       // "string"
typeof 10;          // "number"
typeof false;       // "boolean"
Array.isArray([]);  // true (forma correta de checar arrays)

// Uma peculiaridade histórica do JS:
typeof null;        // "object" (cuidado, isso confunde!)
```

---

## 4. Conversão de Tipos (Coerção)
Às vezes, você precisa converter um tipo em outro.

**Conversão Explícita (Você no controle):**
```js
Number("42");    // Converte string para número -> 42
String(10);      // Converte número para string -> "10"
Boolean("");     // Strings vazias são 'falsy' -> false
Boolean("ok");   // Qualquer outra string é 'truthy' -> true
```
**Dica:** Evite a conversão implícita (automática), que pode gerar bugs. Por exemplo, `1 + "2"` resulta em `"12"`, não `3`.

---

## 5. Operadores Essenciais

### 5.1 Aritméticos
`+` (soma), `-` (subtração), `*` (multiplicação), `/` (divisão), `%` (resto da divisão), `**` (potência).
```js
2 ** 3; // 2 elevado a 3 = 8
10 % 3; // Resto de 10 dividido por 3 = 1
```

### 5.2 Atribuição
`=` (atribui valor), `+=` (soma e atribui), `-=` (subtrai e atribui), etc.
```js
let x = 10;
x += 5; // o mesmo que x = x + 5; agora x é 15
```

### 5.3 Comparação
Use sempre a comparação estrita (`===` e `!==`) para evitar surpresas com a conversão automática de tipos.

```js
// Comparação com coerção (EVITE)
0 == false;  // true (ruim, pois os tipos são diferentes)

// Comparação estrita (PREFIRA)
0 === false; // false (correto, pois um é number e outro é boolean)
10 === 10;   // true
```

### 5.4 Lógicos e Atalhos Modernos
`&&` (E), `||` (OU), `!` (NÃO).

```js
// Optional Chaining (?.) - Acessa propriedades de forma segura
const user = { perfil: { nome: "Ana" } };
const nome = user?.perfil?.nome; // "Ana"
const cep = user?.endereco?.cep; // undefined (não quebra o código)

// Nullish Coalescing (??) - Fornece um valor padrão APENAS para null ou undefined
const idade = user?.idade ?? 18; // Se user.idade for null/undefined, usa 18
```

---

## 6. Estruturas de Controle

### 6.1 Condicionais: `if / else`
Para tomar decisões no código.
```js
const nota = 85;
if (nota >= 90) {
    console.log("Ótimo (A)");
} else if (nota >= 80) {
    console.log("Bom (B)");
} else {
    console.log("Precisa melhorar (C)");
}
```

### 6.2 Condicionais: `switch`
Uma alternativa ao `if/else` para múltiplos casos baseados em um único valor.
```js
const nivelAcesso = "admin";
switch (nivelAcesso) {
    case "admin":
        console.log("Acesso total.");
        break;
    case "user":
        console.log("Acesso limitado.");
        break;
    default:
        console.log("Visitante.");
}
```

### 6.3 Laços de Repetição: `for` e `while`
Para executar um bloco de código várias vezes.
```js
// for: ideal quando você sabe o número de iterações
for (let i = 0; i < 3; i++) {
    console.log(`Contando: ${i}`);
}

// while: ideal quando a condição de parada é variável
let moedas = 5;
while (moedas > 0) {
    console.log("Gastou uma moeda.");
    moedas--;
}
```

### 6.4 Laços para Coleções: `for...of` e `for...in`
- `for...of`: Itera sobre os **valores** de um iterável (como um array). **(Preferido para arrays)**
- `for...in`: Itera sobre as **chaves** (ou índices) de um objeto.

```js
// for...of para valores
for (const cor of ["azul", "verde"]) {
    console.log(cor); // "azul", depois "verde"
}

// for...in para chaves
const carro = { marca: "Tesla", modelo: "Model 3" };
for (const chave in carro) {
    console.log(`${chave}: ${carro[chave]}`); // "marca: Tesla", "modelo: Model 3"
}
```

### 6.5 Iteração Funcional (O jeito moderno)
Métodos de array que são mais declarativos e evitam mutações.

```js
const numeros = [1, 2, 3, 4];

// map: transforma cada elemento em um novo valor
const dobrados = numeros.map(n => n * 2); // [2, 4, 6, 8]

// filter: cria um novo array com elementos que passam em um teste
const pares = numeros.filter(n => n % 2 === 0); // [2, 4]

// reduce: reduz o array a um único valor (ex: uma soma)
const soma = numeros.reduce((acumulador, n) => acumulador + n, 0); // 10
```

---

## 7. Funções: O Coração da Lógica

### 7.1 Declaração vs. Expressão
```js
// Declaração de Função (sofre "hoisting", pode ser chamada antes de ser definida)
function soma(a, b) {
  return a + b;
}

// Expressão de Função (não sofre "hoisting")
const multiplica = function(a, b) {
  return a * b;
};
```

### 7.2 Arrow Functions (`=>`)
Uma sintaxe mais curta e concisa, muito comum no JS moderno.
```js
// Função tradicional
const quadrado_tradicional = function(n) {
    return n * n;
}

// Arrow function equivalente
const quadrado_arrow = n => n * n;
```

### 7.3 Parâmetros Padrão
Defina valores padrão para os parâmetros de uma função, caso eles não sejam fornecidos.
```js
function conectar(host = "localhost", porta = 5432) {
    console.log(`Conectando em ${host}:${porta}`);
}

conectar(); // "Conectando em localhost:5432"
conectar("meu-banco.com"); // "Conectando em meu-banco.com:5432"
```

### 7.4 Funções Puras e Imutabilidade
Uma **função pura** é aquela que, para a mesma entrada, sempre produz a mesma saída e não tem efeitos colaterais (não modifica nada fora dela). Isso torna o código mais previsível e fácil de testar.

```js
// Função impura (muda o array original)
const adicionarItem_impuro = (lista, item) => {
    lista.push(item); // Efeito colateral: modifica a lista!
    return lista;
}

// Função pura (cria e retorna um novo array)
const adicionarItem_puro = (lista, item) => {
    return [...lista, item]; // Não modifica a lista original
}
```

---

## 8. Escopo: Onde as Variáveis Vivem
Escopo define a visibilidade ou acessibilidade de uma variável.

- **Escopo de Bloco (`{...}`):** Variáveis declaradas com `let` e `const` só existem dentro do bloco onde foram criadas.
- **Escopo de Função:** Variáveis declaradas dentro de uma função só são acessíveis dentro dela.
- **Escopo Global:** Variáveis declaradas fora de qualquer função. Evite poluir o escopo global.

```js
const xGlobal = 10; // Escopo Global

function testarEscopo() {
    const yFuncao = 20; // Escopo de Função
    if (true) {
        const zBloco = 30; // Escopo de Bloco
        console.log(xGlobal, yFuncao, zBloco); // 10 20 30
    }
    // console.log(zBloco); // Erro! zBloco não existe aqui.
}
// console.log(yFuncao); // Erro! yFuncao não existe aqui.
```
**Regra de ouro:** Use `const` por padrão. Se precisar reatribuir o valor, use `let`. **Evite `var`**, pois seu escopo é confuso e propenso a erros.

---

## 9. Manipulação Moderna de Arrays
Combine métodos de array para realizar operações complexas de forma elegante.

```js
const usuarios = [
    { id: 1, nome: "Ana", ativo: true },
    { id: 2, nome: "Bruno", ativo: false },
    { id: 3, nome: "Carla", ativo: true },
];

// Encontrar o primeiro usuário que corresponde a uma condição
const usuarioBruno = usuarios.find(u => u.nome === "Bruno");

// Criar uma lista com os nomes dos usuários ativos, em maiúsculas
const nomesAtivos = usuarios
    .filter(u => u.ativo) // 1. Filtra apenas os ativos
    .map(u => u.nome.toUpperCase()); // 2. Transforma o resultado em nomes maiúsculos

// Resultado: ["ANA", "CARLA"]
```

---

## 10. Imutabilidade em Objetos
Para atualizar um objeto sem modificá-lo diretamente (mutação), crie uma cópia com as alterações desejadas usando o operador spread (`...`).

```js
const estadoInicial = { usuario: { nome: "Ana", pontos: 10 }, tema: "claro" };

// Atualizando os pontos do usuário de forma imutável
const novoEstado = {
    ...estadoInicial, // 1. Copia todas as propriedades do estado antigo
    usuario: {
        ...estadoInicial.usuario, // 2. Copia as propriedades do usuário aninhado
        pontos: estadoInicial.usuario.pontos + 5 // 3. Sobrescreve apenas a propriedade 'pontos'
    }
};
// estadoInicial permanece inalterado.
// novoEstado é { usuario: { nome: "Ana", pontos: 15 }, tema: "claro" }
```

---

## 11. Tratamento de Erros com `try...catch`
Código pode falhar. Antecipe e trate os erros de forma graciosa para que sua aplicação não quebre.

```js
function dividir(a, b) {
    if (b === 0) {
        // Lança um erro se a condição for atendida
        throw new Error("Divisão por zero não é permitida.");
    }
    return a / b;
}

try {
    // Tenta executar o código que pode falhar
    const resultado = dividir(10, 0);
    console.log(resultado);
} catch (erro) {
    // Captura o erro se ele for lançado
    console.error("Ocorreu um erro:", erro.message);
} finally {
    // Este bloco é executado sempre, com ou sem erro.
    console.log("Operação finalizada.");
}
```

---

## 12. Boas Práticas para um Código Limpo
- **`const` > `let` > `var`:** Use `const` sempre que possível. Evite `var`.
- **Funções Pequenas e Puras:** Crie funções que façam uma única coisa e evitem efeitos colaterais.
- **Nomes Claros:** Nomeie variáveis e funções de forma descritiva. `usuariosAtivos` é melhor que `ua`.
- **Prefira Métodos Funcionais:** Use `.map`, `.filter`, `.reduce` em vez de laços `for` quando o código ficar mais legível.
- **Imutabilidade:** Não modifique dados diretamente. Crie cópias com as alterações.
- **Comente a Intenção:** Seu código deve dizer *o que* faz. Comentários devem dizer *por que* faz.

---

## 13. Próximos Passos na sua Jornada
- **DOM e Eventos:** Aprenda a manipular HTML e responder a ações do usuário.
- **Assincronicidade:** Entenda como lidar com operações que levam tempo (ex: chamadas de API) com `async/await` e `Promises`.
- **Testes:** Escreva testes para garantir que seu código funciona como esperado (Jest, Vitest).
- **Ferramentas Modernas:** Explore bundlers (Vite, Webpack) e transpilers (Babel).
- **TypeScript:** Adicione tipos estáticos ao seu JavaScript para pegar erros mais cedo e melhorar a organização.

**Resumo:** Você viu as bases sólidas do JavaScript moderno. O segredo agora é praticar. Crie pequenos projetos, resolva desafios e, o mais importante, divirta-se!

---

## 4. Recursos Modernos do ES6+

O ES6 trouxe melhorias significativas para o JavaScript. Aqui estão alguns recursos essenciais:

### Destructuring
Permite extrair valores de arrays ou objetos de forma mais simples.
```javascript
const pessoa = { nome: 'Ana', idade: 28 };
const { nome, idade } = pessoa;
console.log(nome, idade); // Ana 28
```

### Spread e Rest Operators
- **Spread (`...`)**: Expande elementos de arrays ou objetos.
- **Rest (`...`)**: Coleta o restante dos elementos.
```javascript
const numeros = [1, 2, 3];
const maisNumeros = [...numeros, 4, 5];
console.log(maisNumeros); // [1, 2, 3, 4, 5]
```

### Funções Arrow
Funções mais curtas e com escopo de `this` léxico.
```javascript
const soma = (a, b) => a + b;
console.log(soma(2, 3)); // 5
```

### Módulos
Organize seu código em arquivos separados.
```javascript
// arquivo.js
export const saudacao = 'Olá';

// main.js
import { saudacao } from './arquivo.js';
console.log(saudacao);
```
