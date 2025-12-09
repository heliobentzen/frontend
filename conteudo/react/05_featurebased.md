# Arquitetura Feature-Based em React

## Estrutura de Diretórios

```
src/
├── app/
│   ├── App.jsx
│   ├── index.jsx
│   └── routes.jsx
├── shared/                # Recursos reutilizáveis
│   ├── components/        # Componentes genéricos (Button, Input, Modal)
│   ├── hooks/             # Hooks globais (useFetch, useAuth)
│   ├── utils/             # Funções utilitárias
│   ├── services/          # Serviços globais (api.js)
│   ├── context/           # Contextos globais (ThemeContext, AuthContext)
│   ├── types/             # Tipos TypeScript compartilhados
│   └── constants/         # Constantes globais
├── features/              # Cada feature isolada
│   ├── auth/
│   │   ├── pages/
│   │   ├── components/
│   │   ├── hooks/
│   │   ├── services/
│   │   ├── types/
│   │   ├── constants/
│   │   └── index.js
│   ├── dashboard/
│   │   ├── pages/
│   │   ├── components/
│   │   ├── hooks/
│   │   ├── services/
│   │   ├── types/
│   │   ├── constants/
│   │   └── index.js
│   └── profile/
│       ├── pages/
│       ├── components/
│       ├── hooks/
│       ├── services/
│       ├── types/
│       ├── constants/
│       └── index.js
├── assets/                # Imagens, ícones, fontes, estilos globais
└── config/                # Configurações da aplicação (env, theme)
```

## Estrutura Interna de uma Feature

Cada pasta em `features/` segue este padrão:

```
features/auth/
├── pages/              # Páginas/containers da feature
│   ├── LoginPage.jsx
│   └── RegisterPage.jsx
├── components/         # Componentes específicos da feature
│   ├── LoginForm.jsx
│   ├── RegisterForm.jsx
│   └── AuthHeader.jsx
├── hooks/              # Hooks customizados da feature
│   ├── useAuthService.js
│   └── useAuthValidation.js
├── services/           # Serviços específicos da feature
│   └── authService.js
├── types/              # Tipos TypeScript da feature
│   └── auth.types.ts
├── constants/          # Constantes da feature
│   └── authConstants.js
└── index.js            # Barrel export
```

## Exemplos

### 1. **shared/components** - Componentes Base
```jsx
// shared/components/Button.jsx
export const Button = ({ 
    children, 
    variant = 'primary', 
    size = 'md',
    className = '',
    ...props 
}) => {
    const baseStyles = 'font-semibold rounded-lg transition-colors duration-200';
    const variants = {
        primary: 'bg-blue-600 hover:bg-blue-700 text-white',
        secondary: 'bg-gray-200 hover:bg-gray-300 text-gray-800',
        danger: 'bg-red-600 hover:bg-red-700 text-white',
    };
    const sizes = {
        sm: 'px-3 py-1 text-sm',
        md: 'px-4 py-2 text-base',
        lg: 'px-6 py-3 text-lg',
    };

    return (
        <button 
            className={`${baseStyles} ${variants[variant]} ${sizes[size]} ${className}`}
            {...props}
        >
            {children}
        </button>
    );
};
```

### 2. **shared/components** - Input com Validação
```jsx
// shared/components/Input.jsx
export const Input = ({ label, error, className = '', ...props }) => (
    <div className="flex flex-col gap-1">
        {label && <label className="text-sm font-medium text-gray-700">{label}</label>}
        <input 
            className={`px-4 py-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 ${
                error ? 'border-red-500' : 'border-gray-300'
            } ${className}`}
            {...props}
        />
        {error && <span className="text-xs text-red-500">{error}</span>}
    </div>
);
```

### 3. **shared/services** - API Client
```javascript
// shared/services/api.js
const BASE_URL = process.env.REACT_APP_API_URL || 'http://localhost:3001';

export const api = {
    get: (url) => fetch(`${BASE_URL}${url}`).then(r => r.json()),
    post: (url, data) => fetch(`${BASE_URL}${url}`, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(data)
    }).then(r => r.json()),
};
```

### 4. **features/auth/pages** - Login Feature
```jsx
// features/auth/pages/LoginPage.jsx
import { useState } from 'react';
import { LoginForm } from '../components/LoginForm';
import { useAuthService } from '../hooks/useAuthService';

export const LoginPage = () => {
    const { login, loading, error } = useAuthService();
    
    return (
        <div className="min-h-screen bg-gradient-to-br from-blue-50 to-blue-100 flex items-center justify-center p-4">
            <div className="bg-white rounded-xl shadow-lg p-8 w-full max-w-md">
                <h1 className="text-3xl font-bold text-gray-800 mb-6">Login</h1>
                <LoginForm onSubmit={login} loading={loading} error={error} />
            </div>
        </div>
    );
};
```

### 5. **features/auth/components** - Login Form
```jsx
// features/auth/components/LoginForm.jsx
import { useState } from 'react';
import { Input } from '../../../shared/components/Input';
import { Button } from '../../../shared/components/Button';

export const LoginForm = ({ onSubmit, loading, error }) => {
    const [formData, setFormData] = useState({ email: '', password: '' });
    const [errors, setErrors] = useState({});

    const handleSubmit = async (e) => {
        e.preventDefault();
        setErrors({});
        await onSubmit(formData);
    };

    return (
        <form onSubmit={handleSubmit} className="space-y-4">
            {error && <div className="p-3 bg-red-100 border border-red-400 rounded-lg text-red-700 text-sm">{error}</div>}
            
            <Input
                label="Email"
                type="email"
                value={formData.email}
                onChange={(e) => setFormData({ ...formData, email: e.target.value })}
                error={errors.email}
                placeholder="seu@email.com"
                required
            />
            
            <Input
                label="Senha"
                type="password"
                value={formData.password}
                onChange={(e) => setFormData({ ...formData, password: e.target.value })}
                error={errors.password}
                placeholder="••••••••"
                required
            />
            
            <Button type="submit" className="w-full" disabled={loading}>
                {loading ? 'Entrando...' : 'Entrar'}
            </Button>
        </form>
    );
};
```

### 6. **features/auth/hooks** - Custom Hook
```javascript
// features/auth/hooks/useAuthService.js
import { useState } from 'react';
import { useNavigate } from 'react-router-dom';
import { api } from '../../../shared/services/api';

export const useAuthService = () => {
    const [loading, setLoading] = useState(false);
    const [error, setError] = useState(null);
    const navigate = useNavigate();

    const login = async (credentials) => {
        setLoading(true);
        setError(null);
        try {
            const response = await api.post('/auth/login', credentials);
            localStorage.setItem('token', response.token);
            navigate('/dashboard');
        } catch (err) {
            setError(err.message || 'Erro ao fazer login');
        } finally {
            setLoading(false);
        }
    };

    return { login, loading, error };
};
```

### 7. **features/auth/index.js** - Barrel Export
```javascript
// features/auth/index.js
export { LoginPage } from './pages/LoginPage';
export { RegisterPage } from './pages/RegisterPage';
export { useAuthService } from './hooks/useAuthService';
```

