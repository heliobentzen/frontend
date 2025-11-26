# React Router: Navegação em Aplicações React

React Router é a biblioteca padrão para roteamento em aplicações React. Ela permite a criação de Single-Page Applications (SPAs) com navegação entre diferentes "páginas" ou views, sem a necessidade de recarregar a página inteira, proporcionando uma experiência de usuário mais fluida e rápida.

## 1. Instalação

Para começar, adicione o `react-router-dom` ao seu projeto.

```bash
# Usando npm
npm install react-router-dom

# Usando yarn
yarn add react-router-dom
```

## 2. Configuração Básica

A configuração inicial envolve envolver sua aplicação principal com o componente `<BrowserRouter>`.

**`src/index.js` ou `src/main.jsx`**

```jsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import { BrowserRouter } from 'react-router-dom';
import App from './App';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
    <React.StrictMode>
        <BrowserRouter>
            <App />
        </BrowserRouter>
    </React.StrictMode>
);
```

## 3. Componentes Essenciais

### `<Routes>` e `<Route>`

-   **`<Routes>`**: É o contêiner para todas as suas rotas. Ele analisa a URL atual e renderiza a primeira `<Route>` que corresponde ao caminho.
-   **`<Route>`**: Mapeia um caminho de URL (`path`) para um componente React (`element`).

### `<Link>`

-   **`<Link>`**: É usado para criar links de navegação. Ele renderiza uma tag `<a>` no HTML, mas previne o comportamento padrão de recarregamento da página, permitindo que o React Router controle a navegação.

---

## Exemplo 1: Roteamento Básico

Vamos criar uma aplicação simples com três páginas: Home, Sobre e Contato.

**Estrutura de arquivos:**

```
src/
|-- components/
|   |-- Home.jsx
|   |-- Sobre.jsx
|   |-- Contato.jsx
|   |-- Navbar.jsx
|-- App.jsx
|-- ...
```

**`src/components/Home.jsx`**

```jsx
import React from 'react';

function Home() {
    return <h1>Página Inicial</h1>;
}

export default Home;
```

**`src/components/Sobre.jsx`**

```jsx
import React from 'react';

function Sobre() {
    return <h1>Sobre Nós</h1>;
}

export default Sobre;
```

**`src/components/Contato.jsx`**

```jsx
import React from 'react';

function Contato() {
    return <h1>Página de Contato</h1>;
}

export default Contato;
```

**`src/components/Navbar.jsx` (Barra de Navegação)**

```jsx
import React from 'react';
import { Link } from 'react-router-dom';

function Navbar() {
    return (
        <nav>
            <Link to="/">Home</Link> |{' '}
            <Link to="/sobre">Sobre</Link> |{' '}
            <Link to="/contato">Contato</Link>
        </nav>
    );
}

export default Navbar;
```

**`src/App.jsx` (Configuração das Rotas)**

```jsx
import React from 'react';
import { Routes, Route } from 'react-router-dom';
import Home from './components/Home';
import Sobre from './components/Sobre';
import Contato from './components/Contato';
import Navbar from './components/Navbar';

function App() {
    return (
        <div>
            <Navbar />
            <hr />
            <Routes>
                <Route path="/" element={<Home />} />
                <Route path="/sobre" element={<Sobre />} />
                <Route path="/contato" element={<Contato />} />
            </Routes>
        </div>
    );
}

export default App;
```

---

## Exemplo 2: Rotas Dinâmicas com Parâmetros (useParams)

É muito comum ter rotas que dependem de um ID, como `produtos/1` ou `usuarios/ana`.

O hook `useParams` nos permite acessar esses parâmetros dinâmicos da URL.

**`src/components/Produto.jsx`**

```jsx
import React from 'react';
import { useParams } from 'react-router-dom';

// Dados de exemplo
const produtos = {
    '1': { nome: 'Notebook Gamer', preco: 'R$ 5.000,00' },
    '2': { nome: 'Mouse sem fio', preco: 'R$ 150,00' },
};

function Produto() {
    // O nome 'id' deve corresponder ao parâmetro na rota: path="/produtos/:id"
    const { id } = useParams();
    const produto = produtos[id];

    if (!produto) {
        return <h2>Produto não encontrado!</h2>;
    }

    return (
        <div>
            <h1>Detalhes do Produto</h1>
            <h2>{produto.nome}</h2>
            <p>Preço: {produto.preco}</p>
            <p>ID do Produto: {id}</p>
        </div>
    );
}

export default Produto;
```

**`src/App.jsx` (Adicionando a nova rota)**

```jsx
// ... imports
import Produto from './components/Produto';

function App() {
    return (
        <div>
            <Navbar />
            {/* Adicione links para os produtos na Navbar ou em outra página */}
            <hr />
            <Routes>
                <Route path="/" element={<Home />} />
                <Route path="/sobre" element={<Sobre />} />
                <Route path="/contato" element={<Contato />} />
                {/* Rota dinâmica */}
                <Route path="/produtos/:id" element={<Produto />} />
            </Routes>
        </div>
    );
}
```

Agora, ao acessar `/produtos/1` ou `/produtos/2`, o componente `Produto` será renderizado com os dados correspondentes.

---

## Exemplo 3: Navegação Programática (useNavigate)

Às vezes, você precisa redirecionar o usuário após uma ação, como o envio de um formulário. O hook `useNavigate` é perfeito para isso.

**`src/components/Login.jsx`**

```jsx
import React, { useState } from 'react';
import { useNavigate } from 'react-router-dom';

function Login() {
    const [user, setUser] = useState('');
    const navigate = useNavigate();

    const handleLogin = (e) => {
        e.preventDefault();
        // Lógica de autenticação aqui...
        // Se o login for bem-sucedido, redireciona para o dashboard
        if (user) {
            // O segundo argumento { state: ... } é opcional para passar dados
            navigate('/dashboard', { state: { user: user } });
        } else {
            alert('Por favor, insira um nome de usuário.');
        }
    };

    return (
        <form onSubmit={handleLogin}>
            <h2>Login</h2>
            <input
                type="text"
                placeholder="Nome de usuário"
                value={user}
                onChange={(e) => setUser(e.target.value)}
            />
            <button type="submit">Entrar</button>
        </form>
    );
}

export default Login;
```

**`src/components/Dashboard.jsx`**

```jsx
import React from 'react';
import { useLocation } from 'react-router-dom';

function Dashboard() {
    const location = useLocation();
    const user = location.state?.user || 'Visitante';

    return <h1>Bem-vindo ao Dashboard, {user}!</h1>;
}

export default Dashboard;
```

**`src/App.jsx` (Adicionando as rotas de login e dashboard)**

```jsx
// ... imports
import Login from './components/Login';
import Dashboard from './components/Dashboard';

function App() {
    return (
        <div>
            {/* ... */}
            <Routes>
                {/* ... outras rotas */}
                <Route path="/login" element={<Login />} />
                <Route path="/dashboard" element={<Dashboard />} />
            </Routes>
        </div>
    );
}
```

---

## Exemplo 4: Rotas Aninhadas e Layouts (Outlet)

Para criar layouts compartilhados (como um painel de administração com uma barra lateral fixa), usamos rotas aninhadas e o componente `<Outlet>`.

-   **Rota Pai**: Define o layout compartilhado.
-   **`<Outlet />`**: Marca o local onde os componentes das rotas filhas serão renderizados.

**`src/components/PainelLayout.jsx`**

```jsx
import React from 'react';
import { Link, Outlet } from 'react-router-dom';

function PainelLayout() {
    return (
        <div style={{ display: 'flex' }}>
            <aside style={{ width: '200px', borderRight: '1px solid #ccc', padding: '1rem' }}>
                <h3>Painel</h3>
                <nav>
                    <ul>
                        <li><Link to="/painel/perfil">Meu Perfil</Link></li>
                        <li><Link to="/painel/configuracoes">Configurações</Link></li>
                    </ul>
                </nav>
            </aside>
            <main style={{ flex: 1, padding: '1rem' }}>
                {/* Componentes filhos serão renderizados aqui */}
                <Outlet />
            </main>
        </div>
    );
}

export default PainelLayout;
```

**Componentes filhos:**

```jsx
// src/components/Perfil.jsx
export const Perfil = () => <h2>Informações do Perfil</h2>;

// src/components/Configuracoes.jsx
export const Configuracoes = () => <h2>Configurações da Conta</h2>;
```

**`src/App.jsx` (Configurando as rotas aninhadas)**

```jsx
// ... imports
import PainelLayout from './components/PainelLayout';
import { Perfil, Configuracoes } from './components/Perfil'; // Exemplo

function App() {
    return (
        <div>
            {/* ... */}
            <Routes>
                {/* ... outras rotas */}
                
                {/* Rota de Layout Aninhada */}
                <Route path="/painel" element={<PainelLayout />}>
                    {/* Rota Index: o que é renderizado em /painel */}
                    <Route index element={<h2>Bem-vindo ao seu painel!</h2>} />
                    {/* Rotas Filhas */}
                    <Route path="perfil" element={<Perfil />} />
                    <Route path="configuracoes" element={<Configuracoes />} />
                </Route>
            </Routes>
        </div>
    );
}
```

---

## Exemplo 5: Página "Não Encontrado" (404)

Para capturar qualquer URL que não corresponda a nenhuma rota definida, use `path="*"`.

**`src/components/NotFound.jsx`**

```jsx
import React from 'react';
import { Link } from 'react-router-dom';

function NotFound() {
    return (
        <div>
            <h1>404 - Página Não Encontrada</h1>
            <p>A página que você está procurando não existe.</p>
            <Link to="/">Voltar para a Home</Link>
        </div>
    );
}

export default NotFound;
```

**`src/App.jsx` (Adicionando a rota 404)**

A rota `*` deve ser a **última** rota dentro de `<Routes>`.

```jsx
// ... imports
import NotFound from './components/NotFound';

function App() {
    return (
        <div>
            {/* ... */}
            <Routes>
                <Route path="/" element={<Home />} />
                <Route path="/sobre" element={<Sobre />} />
                <Route path="/contato" element={<Contato />} />
                <Route path="/produtos/:id" element={<Produto />} />
                
                {/* ... outras rotas */}

                {/* Rota "Catch-all" para 404 */}
                <Route path="*" element={<NotFound />} />
            </Routes>
        </div>
    );
}
```

---

## 4. Rotas Dinâmicas e Aninhadas

O React Router permite criar rotas dinâmicas e aninhadas para aplicações mais complexas.

### Rotas Dinâmicas
Use o `useParams` para acessar parâmetros dinâmicos na URL.
```jsx
import { useParams } from 'react-router-dom';

function Usuario() {
    const { id } = useParams();
    return <h1>Detalhes do Usuário {id}</h1>;
}
```

### Rotas Aninhadas
Defina rotas dentro de outras rotas usando o componente `<Outlet>`.
```jsx
import { Outlet } from 'react-router-dom';

function Painel() {
    return (
        <div>
            <h1>Painel</h1>
            <Outlet />
        </div>
    );
}
```