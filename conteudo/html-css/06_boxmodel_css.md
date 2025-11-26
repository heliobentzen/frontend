# 📦 Box Model - CSS

O **Box Model** é a base do layout web: todo elemento HTML é uma caixa composta por conteúdo, preenchimento, borda e margem. Dominar o Box Model é essencial para criar layouts responsivos e modernos.

---

## 1\. Anatomia da Caixa: Camadas do Box Model

Cada elemento tem quatro camadas principais:

- **Content:** O conteúdo real (texto, imagem, etc).
- **Padding:** Espaço interno entre o conteúdo e a borda.
- **Border:** Linha ao redor do padding e conteúdo.
- **Margin:** Espaço externo, separando a caixa de outros elementos.

### Exemplo

```css
.card {
    width: min(100%, 320px);
    padding: 1.5rem;
    border: 1px solid #e0e0e0;
    margin: 1rem auto;
    border-radius: 1rem;
    background: linear-gradient(135deg, #f9f9f9 80%, #e3f2fd 100%);
    box-shadow: 0 2px 8px #0001;
    transition: box-shadow 0.2s;
}
.card:hover {
    box-shadow: 0 10px 24px #0002;
}
```

## 🧩 Boas práticas

### 🔹 Use `rem` ou `em` para espaçamentos responsivos
- `rem`: baseado no tamanho da fonte do elemento raiz (`html`). Garante consistência em todo o layout.
- `em`: relativo ao tamanho da fonte do elemento pai. Permite que componentes se ajustem dinamicamente ao contexto.
- Ideal para margens, paddings e fontes que precisam se adaptar a diferentes resoluções sem perder proporção.

---

### As funções `min()` e `max()` permitem limitar tamanhos de elementos de forma flexível
- `min(a, b)`: escolhe o menor valor entre `a` e `b`. Evita que um elemento ultrapasse um limite.
- `max(a, b)`: escolhe o maior valor entre `a` e `b`. Garante que o elemento nunca fique menor que um certo tamanho.
- ✅ Perfeito para layouts fluidos que respeitam limites mínimos ou máximos sem media queries.

**Exemplo:**
```css
width: min(100%, 320px);
```

- Ou seja, em telas grandes: largura será **máximo 320px** e em telas pequenas: largura será **100% do espaço disponível**
---

## 2\. Tamanho e Cálculo: `width`, `height`, `box-sizing`

Por padrão, `width` e `height` afetam só o conteúdo. O padding e a borda são somados. Para facilitar, use:

```css
*,
*::before,
*::after {
    box-sizing: border-box;
}
```

Assim, o tamanho total do elemento inclui padding e borda, tornando o layout previsível.

### Novidades úteis

- **`aspect-ratio`:** Define proporção fixa da caixa.
- **`gap`:** Espaçamento entre itens em layouts flex/grid.
- **`container queries`:** Adapta estilos ao tamanho do contêiner (suporte crescente).

---

## 3\. Box Sizing

O `box-sizing` controla como o tamanho total de um elemento é calculado:

- **`content-box`**: Inclui apenas o conteúdo (padrão).
- **`border-box`**: Inclui padding e borda no cálculo.

### Exemplo
```css
* {
    box-sizing: border-box;
}
```

## 4\. Layouts Responsivos com Box Model

Combine o Box Model com propriedades como `max-width` e `media queries` para criar layouts flexíveis.

### Exemplo
```css
.container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 1rem;
}

@media (max-width: 768px) {
    .container {
        padding: 0.5rem;
    }
}
```

---

## 3\. Exemplo Prático

```html
<div class="cards">
    <article class="card">
        <h2>Starter</h2>
        <p>Ideal para projetos simples.</p>
    </article>
    <article class="card">
        <h2>Pro</h2>
        <p>Recursos avançados e suporte.</p>
    </article>
    <article class="card">
        <h2>Enterprise</h2>
        <p>Para grandes equipes e demandas.</p>
    </article>
</div>
```

```css
.cards {
    display: flex;
    gap: 2rem;
    flex-wrap: wrap;
    justify-content: center;
    padding: 2rem;
}
```

---

## 🚀 Atividade Prática 06

Crie uma página com:

1. Adicione um container com três `<article class="card">`.
2. No CSS, aplique:
    - `box-sizing: border-box` universal.
    - `.card` com largura máxima, padding, borda, margem, cor de fundo e borda arredondada.
    - Use `gap` no container para espaçamento.
    - Defina diferentes valores de `padding` e `margin` para experimentar o espaçamento interno e externo das caixas.
    - Adicione `border` com diferentes larguras, estilos e cores para cada card.
    - Utilize `outline` em um dos cards para destacar o foco (acessibilidade).
    - Experimente `min-width` e `max-width` para limitar o tamanho dos cards.
    - Teste `aspect-ratio` para manter proporções fixas.
    - Adicione `box-shadow` para um visual moderno.
    - Altere o `background` de cada card usando gradientes ou cores sólidas.
    - Faça um dos cards ter `margin: auto` para centralizá-lo no container.
3. Observe como cada propriedade do Box Model afeta o layout e a aparência dos elementos.

> Dica: Use as ferramentas de inspeção do navegador para visualizar as camadas do Box Model em cada elemento.

Abra no navegador e veja cards responsivos, bonitos e alinhados com as melhores práticas atuais.

## Referências e Recursos
- [MDN Web Docs: Box Model](https://developer.mozilla.org/pt-BR/docs/Learn/CSS/Building_blocks/The_box_model)
- [MDN Web Docs: box-sizing](https://developer.mozilla.org/pt-BR/docs/Web/CSS/box-sizing)
- [CSS Tricks: CSS Box Model](https://css-tricks.com/the-css-box-model/)
- [W3Schools: CSS Box Model](https://www.w3schools.com/css/css_boxmodel.asp)
- [MDN Web Docs: aspect-ratio](https://developer.mozilla.org/pt-BR/docs/Web/CSS/aspect-ratio)
- [MDN Web Docs: gap](https://developer.mozilla.org/pt-BR/docs/Web/CSS/gap)
- [MDN Web Docs: min(), max(), clamp()](https://developer.mozilla.org/pt-BR/docs/Web/CSS/min)