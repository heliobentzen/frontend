# Introdução ao CSS

CSS é o que transforma páginas HTML simples em experiências visuais modernas e atraentes. Com ele, você controla cores, fontes, espaçamentos, layouts responsivos, animações e muito mais. Vamos aprender como dar vida às suas páginas!

---

## 1\. Contêineres Genéricos: `div` e `span`

No HTML, usamos `div` (bloco) e `span` (linha) para agrupar e estilizar elementos:

- **`<div>`**: Agrupa grandes blocos de conteúdo. Sempre começa em nova linha.
- **`<span>`**: Destaca partes pequenas dentro de um texto. Não quebra linha.

**Exemplo:**

```html
<div id="cabecalho">
    <h1>Meu Site</h1>
</div>
<p>CSS é <span class="destaque">essencial</span> para web moderna.</p>
```

---

## 2\. Identificando Elementos: `id` e `class`

- **`id`**: Identificador único por página. Use para seções exclusivas.
- **`class`**: Pode ser reutilizada em vários elementos. Ideal para estilos compartilhados.

**Exemplo:**

```html
<div id="menu"></div>
<div class="card"></div>
<div class="card destaque"></div>
```

---

## 3\. Como Adicionar CSS

Três formas principais:

1. **Inline** (não recomendado):  
     `<p style="color: blue;">Texto</p>`

2. **Interno** (para páginas pequenas ou testes):  
     ```html
     <style>
         .destaque { color: red; }
     </style>
     ```

3. **Externo** (profissional):  
     ```html
     <link rel="stylesheet" href="estilos.css">
     ```

---

## 4\. Sintaxe e Seletores CSS

```css
.seletor {
    propriedade: valor;
}
```

- **Classe**: `.nome`
- **ID**: `#nome`
- **Tag**: `tagname`

**Exemplo:**

```css
#cabecalho { background: #222; color: #fff; }
.destaque { color: #e63946; font-weight: bold; }
```

---

## 4\. Seletores Avançados

CSS oferece seletores poderosos para estilizar elementos de forma precisa:

- **`:nth-child(n)`**: Seleciona o n-ésimo filho.
- **`:not(selector)`**: Exclui elementos que correspondem ao seletor.

### Exemplo
```css
li:nth-child(odd) {
    background-color: #f0f0f0;
}
li:not(.ativo) {
    color: #ccc;
}
```

## 5\. Variáveis CSS

Variáveis CSS tornam os estilos mais reutilizáveis e fáceis de manter.

### Exemplo
```css
:root {
    --cor-primaria: #3498db;
    --padding-padrao: 1rem;
}

button {
    background: var(--cor-primaria);
    padding: var(--padding-padrao);
}
```

---

## 6\. Cores Modernas em CSS

- **Nomes**: `red`, `blue`, `tomato`
- **HEX**: `#ff5733`
- **RGB**: `rgb(255, 87, 51)`
- **RGBA** (com transparência): `rgba(255,87,51,0.7)`
- **HSL**: `hsl(12, 100%, 60%)`

**Exemplo:**

```css
body { background: #f5f6fa; color: #222; }
h1 { color: hsl(210, 90%, 40%); }
```

---

## 7\. Fundos Modernos

- **Cor sólida**: `background-color: #fff;`
- **Imagem**: `background-image: url('img.jpg');`
- **Gradiente**:  
    ```css
    background: linear-gradient(90deg, #6a11cb, #2575fc);
    ```

- **Responsivo**:  
    ```css
    @media (max-width: 600px) {
        body { font-size: 16px; }
    }
    ```

---

## 8\. Exemplo Moderno e Compacto

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <title>Exemplo CSS Moderno</title>
    <style>
        body {
            font-family: system-ui, sans-serif;
            background: linear-gradient(120deg, #f0f2f5, #d9e7fa);
            margin: 0; color: #222;
        }
        #cabecalho {
            background: #222; color: #fff; padding: 1.5rem; text-align: center;
        }
        .card {
            background: #fff; border-radius: 8px; box-shadow: 0 2px 8px #0001;
            margin: 2rem auto; max-width: 400px; padding: 1.5rem;
        }
        .destaque { color: #e63946; }
        #rodape {
            background: #222; color: #fff; text-align: center; padding: 1rem;
            font-size: 0.9rem;
        }
    </style>
</head>
<body>
    <div id="cabecalho"><h1>Meu Site Moderno</h1></div>
    <div class="card">
        <h2>Bem-vindo!</h2>
        <p>Aprenda <span class="destaque">CSS moderno</span> e crie páginas incríveis.</p>
    </div>
    <div id="rodape">&copy; 2025 - Todos os direitos reservados.</div>
</body>
</html>
```

---

## 🚀 Atividade Prática 05

Crie uma página com:

- Um cabeçalho (`id="cabecalho"`)
- Dois blocos de conteúdo (`class="card"`)
- Um rodapé (`id="rodape"`)
- Destaque uma palavra usando `<span class="destaque">`
- Use CSS interno para estilizar conforme o exemplo acima

Abra no navegador e experimente mudar cores, gradientes e fontes!

## Referências e Recursos
- [Documentação oficial do CSS (MDN)](https://developer.mozilla.org/pt-BR/docs/Web/CSS)
- [W3Schools CSS Tutorial](https://www.w3schools.com/css/)
- [Guia CSS Tricks](https://css-tricks.com/snippets/css/)
- [Can I use (compatibilidade CSS)](https://caniuse.com/)
- [Google Fonts](https://fonts.google.com/)
- [Color Hunt (paletas de cores)](https://colorhunt.co/)
- [CSS Gradient Generator](https://cssgradient.io/)