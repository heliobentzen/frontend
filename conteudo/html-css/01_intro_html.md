# Estrutura Essencial de uma Página HTML

HTML (HyperText Markup Language) é a linguagem fundamental da web. Com ela, estruturamos o conteúdo das páginas — textos, imagens, links, listas — para que os navegadores possam exibi-los corretamente aos usuários.

-----

## 1. O Ponto de Partida: `<!DOCTYPE html>`

A primeira linha de qualquer página HTML moderna é a declaração `<!DOCTYPE html>`. Ela informa ao navegador que o documento está usando a versão mais recente do HTML, o **HTML5**. Sem essa declaração, o navegador pode interpretar o código de forma inesperada, causando problemas de layout.

Exemplo de declarações:

```html
<!DOCTYPE html> <!-- HTML5 (moderna e recomendada) -->
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd"> <!-- HTML 4.01 (antiga) -->
```

-----

## 2. O Contêiner Principal: `<html>`

Após o `DOCTYPE`, todo o conteúdo da página é envolvido pelo elemento `<html>`, que é o elemento raiz do documento.

### O atributo `lang`

É comum adicionar o atributo `lang` à tag `<html>` para indicar o idioma principal da página, por exemplo: `lang="pt-BR"`. Isso auxilia ferramentas de acessibilidade e mecanismos de busca.

Exemplo:

```html
<html lang="pt-BR">
    <!-- Conteúdo da página -->
</html>
```

-----

## 3. Divisão Fundamental: `<head>` e `<body>`

Dentro do `<html>`, a página se divide em duas partes principais:

### `<head>`: Informações sobre a página

A seção `<head>` contém metadados e configurações importantes, como:

- `<meta charset="UTF-8">`: Define o conjunto de caracteres como UTF-8, garantindo a exibição correta de acentos e símbolos especiais.
- `<title>`: Define o texto exibido na aba do navegador.
- Outras tags `<meta>`: Como `description` e `keywords`, que ajudam na otimização para buscadores (SEO).

Exemplo:

```html
<head>
    <meta charset="UTF-8">
    <title>Minha Primeira Página Estruturada</title>
</head>
```

### `<body>`: Conteúdo visível

A seção `<body>` contém todo o conteúdo que será exibido ao usuário: textos, títulos, imagens, links, listas, tabelas, etc.

Exemplo:

```html
<body>
    <h1>Meu Primeiro Título</h1>
    <p>Este é um parágrafo dentro do corpo da página.</p>
</body>
```

-----

## 4. Comentários em HTML

Comentários servem para deixar notas no código, facilitando a compreensão para você e outros desenvolvedores. Eles são ignorados pelo navegador.

Sintaxe:

```html
<!-- Este é um comentário -->
<h1>Meu Site Incrível</h1>
```

-----

## 4. Acessibilidade com HTML

A acessibilidade \\(a11y\\) garante que todos os usu\u00e1rios, incluindo aqueles com defici\u00eancias, possam navegar e interagir com a web. Use atributos `aria-*` para melhorar a experi\u00eancia:

- **`aria-label`**: Adiciona descri\u00e7\u00f5es a elementos.
- **`role`**: Define o papel de um elemento (ex.: `role="button"`).

### Exemplo
```html
<button aria-label="Fechar janela">&times;</button>
```

## 5. Metadados no `<head>`

Metadados ajudam navegadores e mecanismos de busca a entenderem sua p\u00e1gina. Inclua:

- **`<meta charset>`**: Define a codifica\u00e7\u00e3o de caracteres.
- **`<meta name="viewport">`**: Torna a p\u00e1gina responsiva.

### Exemplo
```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Minha P\u00e1gina</title>
</head>
```

-----

## 6. Principais Elementos HTML

### Títulos e Parágrafos

```html
<h1>Título Principal</h1>
<h2>Subtítulo</h2>
<p>Este é um parágrafo de texto.</p>
```

- `<h1>` até `<h6>`: Títulos, do mais importante ao menos importante.
- `<p>`: Parágrafo.

### Links e Imagens

```html
<a href="https://www.exemplo.com">Visite o site</a>
<img src="imagem.jpg" alt="Descrição da imagem">
```

- `<a>`: Cria um link (`href` define o destino).
- `<img>`: Exibe uma imagem (`src` é o caminho, `alt` é o texto alternativo).

### Listas

```html
<ul>
    <li>Item de lista não ordenada</li>
    <li>Outro item</li>
</ul>
<ol>
    <li>Primeiro item de lista ordenada</li>
    <li>Segundo item</li>
</ol>
```

- `<ul>`: Lista não ordenada.
- `<ol>`: Lista ordenada.
- `<li>`: Item da lista.

### Tabelas

```html
<table>
    <tr>
        <th>Nome</th>
        <th>Idade</th>
    </tr>
    <tr>
        <td>Ana</td>
        <td>25</td>
    </tr>
    <tr>
        <td>João</td>
        <td>30</td>
    </tr>
</table>
```

- `<table>`: Cria uma tabela.
- `<tr>`: Linha da tabela.
- `<th>`: Cabeçalho.
- `<td>`: Célula de dados.

-----

## 7. Boas Práticas

- Sempre feche as tags corretamente.
- Use indentação para facilitar a leitura.
- Utilize o atributo `alt` em imagens para acessibilidade.
- O conteúdo do `<head>` não aparece na página, mas é essencial para SEO e funcionamento adequado.

-----

## 🚀 Atividade Prática 01

**Objetivo:** Criar seu primeiro arquivo HTML, aplicando os conceitos de estrutura essencial.

**Passos:**

1. Abra o **Visual Studio Code**.
2. Crie um novo arquivo e salve como `pratica1.html`.
3. Digite toda a estrutura básica apresentada acima.
4. Altere o `<title>` para "Meu Primeiro Site".
5. No `<body>`, adicione:
    - Um `<h1>` com seu nome completo.
    - Um `<p>` descrevendo o que achou mais interessante na aula.
6. Adicione um comentário em HTML acima do `<h1>` explicando o que aquela linha faz.
7. Salve e abra o arquivo no navegador para ver o resultado.
8. Envie o arquivo conforme as instruções da atividade.

**Desafio (Opcional):**  
Pesquise sobre a meta tag `description` e adicione uma ao `<head>`, descrevendo o conteúdo da sua página.

## Referências e Recursos
- [MDN Web Docs: HTML Básico](https://developer.mozilla.org/pt-BR/docs/Learn/Getting_started_with_the_web/HTML_basics)
- [W3Schools: HTML Tutorial](https://www.w3schools.com/html/)
- [Guia de Referência HTML (em português)](https://www.devmedia.com.br/guia/html/38111)
- [HTML Living Standard (WHATWG)](https://html.spec.whatwg.org/)