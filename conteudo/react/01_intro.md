# Introdução ao React

Enfim, React! Este guia foi projetado para fornecer uma introdução clara e prática à biblioteca que revolucionou o desenvolvimento de interfaces de usuário (UI).

## O que é React?

React é uma biblioteca JavaScript de código aberto, criada pelo Facebook, para construir interfaces de usuário. Ele não é um framework completo (como Angular), mas sim uma biblioteca focada na camada de visualização (a "View" no padrão MVC).

Seu principal objetivo é facilitar a criação de UIs interativas, rápidas e reutilizáveis através de uma abordagem baseada em componentes.

## Por que usar React?

*   **Abordagem Declarativa:** Você descreve como sua UI deve se parecer em qualquer estado, e o React se encarrega de atualizar o DOM (Document Object Model) de forma eficiente quando os dados mudam.
*   **Baseado em Componentes:** Permite que você divida a UI em peças independentes e reutilizáveis chamadas "componentes". Isso torna o código mais organizado, manutenível e escalável.
*   **Performance:** Utiliza um "DOM Virtual" para minimizar as manipulações diretas e lentas no DOM do navegador, resultando em aplicações mais rápidas.

## Configuração do Ambiente e Primeiro "Olá, Mundo!"

Antes de mergulharmos nos conceitos, vamos colocar a mão na massa e criar nossa primeira aplicação React. A forma mais moderna e recomendada de iniciar um projeto React é usando um *build tool* como o **Vite**.

### Pré-requisitos

Para começar, você precisa ter o **Node.js** e o **npm** (Node Package Manager) instalados em sua máquina. O npm é instalado automaticamente com o Node.js. Você pode baixá-los em [nodejs.org](https://nodejs.org/).

### Criando a Aplicação com Vite

O Vite é uma ferramenta de construção extremamente rápida que oferece uma experiência de desenvolvimento superior.

1.  **Abra seu terminal** (ou prompt de comando) e execute o seguinte comando para criar um novo projeto:

    ```bash
    npm create vite@latest meu-primeiro-app -- --template react
    ```
    Isso iniciará um assistente. Escolha `React` como framework e `JavaScript` como variante.

2.  **Navegue até a pasta do projeto**, instale as dependências e inicie o servidor de desenvolvimento:

    ```bash
    cd meu-primeiro-app
    npm install
    npm run dev
    ```

    Este comando iniciará a aplicação e mostrará um endereço local no terminal (geralmente `http://localhost:5173`). Abra esse endereço no seu navegador para ver a página padrão do Vite com React.

### Modificando para o "Olá, Mundo!"

Agora, vamos alterar o código para exibir nossa própria mensagem.

1.  Abra a pasta do projeto no seu editor de código preferido (como o VS Code).
2.  Navegue até a pasta `src` e abra o arquivo `App.jsx`.
3.  Substitua todo o conteúdo do arquivo pelo seguinte código:

    ```jsx
    function App() {
      return (
        <h1>Olá, Mundo!</h1>
      );
    }

    export default App;
    ```

4.  Salve o arquivo. O navegador deve atualizar automaticamente, exibindo a mensagem "Olá, Mundo!". Parabéns, você rodou sua primeira aplicação React!

---

# Conceitos Fundamentais

Vamos mergulhar nos dois conceitos mais importantes para começar: JSX e Componentes.

## JSX: JavaScript eXtension

JSX é uma extensão de sintaxe para JavaScript que se parece muito com HTML. Ele permite que você escreva a estrutura da sua UI diretamente no código JavaScript, tornando-o mais visual e intuitivo.

O navegador não entende JSX nativamente. Ferramentas como o Babel (que vem configurado no Vite) transpilam o código JSX para chamadas de função `React.createElement()` que o JavaScript puro entende.

**Exemplo Prático:**

Em vez de escrever isso (JavaScript puro):

```javascript
React.createElement('h1', {className: 'greeting'}, 'Olá, Mundo!');
```

Você escreve isso (com JSX):

```jsx
<h1 className="greeting">Olá, Mundo!</h1>
```

Ambos os códigos produzem o mesmo resultado, mas a versão com JSX é muito mais legível.

### Regras importantes do JSX:

1.  **Expressões JavaScript com `{}`:** Você pode embutir qualquer expressão JavaScript válida dentro de chaves.

    ```jsx
    const name = "Maria";
    const element = <h1>Olá, {name}!</h1>; // Renderiza: <h1>Olá, Maria!</h1>
    ```

2.  **Atributos como `camelCase`:** Atributos HTML como `class` e `for` se tornam `className` e `htmlFor` em JSX, pois são palavras reservadas em JavaScript.

    ```jsx
    // Errado
    // <div class="profile">...</div>

    // Correto
    <div className="profile">...</div>
    ```

3.  **Um Único Elemento Raiz:** Um componente deve sempre retornar um único elemento. Se precisar retornar múltiplos elementos, envolva-os em um elemento pai, como uma `div`, ou use um Fragment (`<>...</>`).

    ```jsx
    // Correto
    function UserInfo() {
      return (
        <>
          <h2>João Silva</h2>
          <p>Desenvolvedor Frontend</p>
        </>
      );
    }
    ```

## Componentes Funcionais

Componentes são os blocos de construção de uma aplicação React. Eles são como funções JavaScript que aceitam entradas (chamadas "props") e retornam elementos React que descrevem o que deve aparecer na tela.

O tipo mais comum de componente hoje é o **Componente Funcional**.

**Exemplo Prático:**

Vamos criar um componente funcional simples que exibe uma mensagem de boas-vindas.

```jsx
// Arquivo: Welcome.jsx

// 1. É uma função JavaScript simples.
// 2. O nome começa com letra maiúscula (convenção do React).
// 3. Retorna JSX.
function Welcome() {
  return <h1>Bem-vindo ao nosso site!</h1>;
}

// Para usá-lo em outro lugar (como em um componente App):
function App() {
  return (
    <div>
      <Welcome />
      <p>Explore nosso conteúdo.</p>
    </div>
  );
}
```

Neste exemplo, `<Welcome />` é como chamamos e renderizamos nosso componente. Essa capacidade de "compor" componentes é um dos maiores poderes do React.

---

# Exercícios Práticos

Agora é sua vez! Tente resolver os exercícios abaixo para fixar o conhecimento.

### Exercício 1: Seu Primeiro Componente

Crie um componente funcional chamado `Header`. Este componente deve renderizar um elemento `header` contendo um `h1` com o texto "Minha Primeira Aplicação React" e um `p` com seu nome.

<details>
  <summary>Clique para ver a solução</summary>

  ```jsx
  function Header() {
    return (
      <header>
        <h1>Minha Primeira Aplicação React</h1>
        <p>Criado por: [Seu Nome]</p>
      </header>
    );
  }
  ```
</details>

### Exercício 2: Tornando seu Componente Dinâmico com Props

Modifique o componente `Header` do exercício anterior para que ele aceite uma `prop` chamada `title` e outra chamada `author`. O componente deve usar essas props para renderizar o título e o autor dinamicamente.

**Dica:** As props são recebidas como um objeto no primeiro argumento da função. Ex: `function Header(props) { ... }`. Você pode acessá-las com `props.title`.

<details>
  <summary>Clique para ver a solução</summary>

  ```jsx
  function Header(props) {
    return (
      <header>
        <h1>{props.title}</h1>
        <p>Criado por: {props.author}</p>
      </header>
    );
  }

  // Exemplo de como usar:
  // <Header title="Blog de Tecnologia" author="Ana" />
  ```
</details>

### Exercício 3: Compondo a Aplicação

Crie um componente principal chamado `App`. Dentro dele, renderize o componente `Header` (criado no exercício 2) duas vezes, com títulos e autores diferentes. Adicione também um componente `Footer` simples que você mesmo criará, contendo um parágrafo com o texto "© 2024 - Todos os direitos reservados.".

<details>
  <summary>Clique para ver a solução</summary>

  ```jsx
  // Componente Header (do exercício anterior)
  function Header(props) {
    return (
      <header>
        <h1>{props.title}</h1>
        <p>Criado por: {props.author}</p>
      </header>
    );
  }

  // Novo componente Footer
  function Footer() {
    return (
      <footer>
        <p>© 2024 - Todos os direitos reservados.</p>
      </footer>
    );
  }

  // Componente principal App
  function App() {
    return (
      <>
        <Header title="Artigo sobre React" author="Carlos" />
        <Header title="Artigo sobre JavaScript" author="Beatriz" />
        <main>
          <p>Conteúdo principal da página aqui...</p>
        </main>
        <Footer />
      </>
    );
  }
  ```
</details>

## Hooks no React

Os Hooks foram introduzidos no React 16.8 e permitem que você use estado e outros recursos do React sem escrever uma classe. Os principais Hooks incluem:

- **useState**: Para gerenciar estados locais.
- **useEffect**: Para lidar com efeitos colaterais, como chamadas à API.
- **useContext**: Para consumir Context API de forma mais simples.

### Exemplo com useState e useEffect
```jsx
import React, { useState, useEffect } from 'react';

function Contador() {
    const [contador, setContador] = useState(0);

    useEffect(() => {
        console.log(`O contador foi atualizado para: ${contador}`);
    }, [contador]);

    return (
        <div>
            <p>Contador: {contador}</p>
            <button onClick={() => setContador(contador + 1)}>Incrementar</button>
        </div>
    );
}
```

### Usando TypeScript com React
O TypeScript melhora a experiência de desenvolvimento ao adicionar tipagem estática. Para configurar um projeto React com TypeScript, use:
```bash
npm create vite@latest meu-projeto -- --template react-ts
```