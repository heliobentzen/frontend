# Context API no React

A Context API é um recurso do React que permite compartilhar dados (estado) entre componentes sem a necessidade de passá-los manualmente por meio de props em cada nível da árvore de componentes.

## O Problema: "Prop Drilling"

Imagine uma árvore de componentes onde um estado, definido no componente mais alto (`App`), precisa ser usado por um componente muito abaixo na hierarquia (`Button`).

```
App (possui o estado)
└──> Toolbar
    └──> ThemedButton
        └──> Button (precisa do estado)
```

Sem a Context API, você teria que passar o estado como `prop` de `App` para `Toolbar`, de `Toolbar` para `ThemedButton`, e finalmente para `Button`. Isso é chamado de **"prop drilling"**. Os componentes intermediários (`Toolbar`, `ThemedButton`) não usam a prop, apenas a repassam, o que torna o código mais verboso e difícil de manter.

## A Solução: Context API

A Context API cria um "túnel" direto do componente que provê o dado (Provider) para o componente que o consome (Consumer), independentemente de quantos níveis existam entre eles.

### Os 3 Passos Essenciais

1.  **Criar o Contexto**: Use a função `React.createContext()` para criar um objeto de contexto. Você pode passar um valor padrão inicial.
2.  **Prover o Contexto**: Use o componente `Context.Provider` para "envelopar" a parte da sua árvore de componentes que precisará de acesso ao contexto. Ele aceita uma `prop` chamada `value`, que são os dados que você quer compartilhar.
3.  **Consumir o Contexto**: Em qualquer componente filho do `Provider`, use o hook `useContext()` para ler os dados do contexto.

---

## Exemplo Prático: Um Seletor de Tema (Claro/Escuro)

Vamos criar um exemplo simples onde o usuário pode alternar entre um tema claro e um escuro.

### Passo 1: Criar o Contexto

Crie um novo arquivo para o nosso contexto, por exemplo, `src/contexts/ThemeContext.js`.

```javascript
// src/contexts/ThemeContext.js
import React, { createContext, useState } from 'react';

// 1. Criar o Contexto com um valor padrão
export const ThemeContext = createContext({
  theme: 'light',
  toggleTheme: () => {},
});

// Componente Provedor que gerenciará o estado do tema
export const ThemeProvider = ({ children }) => {
  const [theme, setTheme] = useState('light');

  const toggleTheme = () => {
    setTheme(currentTheme => (currentTheme === 'light' ? 'dark' : 'light'));
  };

  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      {children}
    </ThemeContext.Provider>
  );
};
```

### Passo 2: Prover o Contexto na Aplicação

Agora, vamos usar o `ThemeProvider` para envolver nossa aplicação principal em `src/App.js`.

```javascript
// src/App.js
import React from 'react';
import { ThemeProvider } from './contexts/ThemeContext';
import Toolbar from './components/Toolbar';
import './App.css';

function App() {
  return (
    // 2. Prover o contexto para os componentes filhos
    <ThemeProvider>
      <Content />
    </ThemeProvider>
  );
}

// Um componente apenas para organizar o conteúdo
function Content() {
  // O hook useContext vai buscar o provider mais próximo na árvore
  const { theme } = React.useContext(ThemeContext);

  return (
    <div className={`App ${theme}`}>
      <header className="App-header">
        <h1>Bem-vindo à minha App</h1>
        <Toolbar />
      </header>
    </div>
  );
}

export default App;
```

### Passo 3: Consumir o Contexto

Finalmente, vamos criar um componente que consome o contexto para exibir um botão e permitir a troca de tema.

```javascript
// src/components/Toolbar.js
import React, { useContext } from 'react';
import { ThemeContext } from '../contexts/ThemeContext';

const Toolbar = () => {
  // 3. Consumir o contexto com o hook useContext
  const { theme, toggleTheme } = useContext(ThemeContext);

  const buttonText = theme === 'light' ? 'Mudar para Tema Escuro' : 'Mudar para Tema Claro';

  return (
    <div>
      <p>O tema atual é: {theme}</p>
      <button onClick={toggleTheme}>
        {buttonText}
      </button>
    </div>
  );
};

export default Toolbar;
```

### CSS para o Exemplo

Adicione este CSS em `src/App.css` para ver o efeito da troca de tema.

```css
/* src/App.css */
.App {
  text-align: center;
  transition: background-color 0.3s, color 0.3s;
}

.App.light {
  background-color: #ffffff;
  color: #282c34;
}

.App.dark {
  background-color: #282c34;
  color: #ffffff;
}

.App-header {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-size: calc(10px + 2vmin);
}

button {
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
  border-radius: 5px;
  border: 1px solid;
}
```

## Context API com useReducer

Para estados mais complexos, combine Context API com o hook `useReducer`.

### Exemplo

```javascript
import React, { createContext, useReducer, useContext } from 'react';

const ContadorContext = createContext();

function contadorReducer(state, action) {
    switch (action.type) {
        case 'incrementar':
            return { contador: state.contador + 1 };
        case 'decrementar':
            return { contador: state.contador - 1 };
        default:
            throw new Error(`A\u00e7\u00e3o desconhecida: ${action.type}`);
    }
}

export function ContadorProvider({ children }) {
    const [state, dispatch] = useReducer(contadorReducer, { contador: 0 });
    return (
        <ContadorContext.Provider value={{ state, dispatch }}>
            {children}
        </ContadorContext.Provider>
    );
}

export function useContador() {
    return useContext(ContadorContext);
}
```

## Quando Usar a Context API?

-   **Dados Globais**: Ideal para dados que são considerados "globais" para uma árvore de componentes, como informações do usuário autenticado, tema, ou idioma preferido.
-   **Evitar Prop Drilling**: Quando você se vê passando props por vários níveis de componentes que não as utilizam.

## Considerações de Performance

-   Toda vez que o valor do `Provider` muda, **todos** os componentes que consomem aquele contexto (`useContext`) serão re-renderizados.
-   Para otimizar, você pode dividir contextos grandes em contextos menores e mais específicos. Assim, uma atualização em um contexto não causa re-renderizações desnecessárias em componentes que consomem outros contextos.

A Context API é uma ferramenta poderosa e fundamental no ecossistema React para o gerenciamento de estado de forma limpa e eficiente.