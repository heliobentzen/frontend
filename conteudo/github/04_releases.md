# 📦 GitHub Releases

Criar e gerenciar releases no GitHub é essencial para controle de versão e distribuição de projetos. Este guia o orienta passo a passo, desde a preparação até a publicação, incluindo automação com GitHub Actions.

---

## 🔧 Passo a passo

### 1️⃣ Preparação
Antes de criar a release, prepare o projeto:

- **Instale dependências:**  
    ```bash
    npm install
    ```

- **Execute testes:**  
    ```bash
    npm test
    ```

- **Gere build de produção:**  
    ```bash
    npm run build
    ```
    ✅ Resultado: pasta `build/` com artefatos otimizados

---

### 2️⃣ Versionamento
Use **SemVer** (Semantic Versioning) para versionamento:
- Formato: `v1.2.0` (Maior.Menor.Patch)
- Atualize automaticamente com:
    ```bash
    npm version minor
    ```
    ✅ Isso cria automaticamente um commit e tag

---

### 3️⃣ Crie tag no GitHub
Se não usou `npm version`, crie manualmente:
```bash
git tag -a v1.2.0 -m "Release v1.2.0"
git push origin v1.2.0
```

---

### 4️⃣ Publique release no GitHub
1. Vá para **Releases → Rascunhar nova release**
2. Selecione a tag (`v1.2.0`)
3. Preencha os campos:
     - **Título:** `v1.2.0 – Nova versão estável`
     - **Descrição:** detalhe as alterações
     - **Anexos:** inclua `build.zip` se necessário

---

### 5️⃣ Estrutura recomendada de notas de release
```markdown
# v1.2.0 — 2025-12-18

## Destaques
- Novo modo offline com cache inteligente.
- Redução de 30% no tempo de build.

## Adicionado
- Novo componente `Button` com suporte a tema.

## Alterado
- React atualizado para 18.3.0.

## Corrigido
- Corrigido bug no formulário de login (#45).

## Mudanças incompatíveis
- Removido suporte ao hook `useLegacyAuth`.

## Segurança
- Atualizações de dependências com correções de CVE.

## Migração
- Execute `app migrate --from 1.2.0`.
```

---

### 6️⃣ Automação com GitHub Actions (opcional)
Configure um workflow para compilar e publicar automaticamente ao criar uma tag:

```yaml
name: Release React App

on:
  push:
    tags:
      - 'v*'

jobs:
  build-and-release:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: '18'
      - run: npm ci
      - run: npm run build
      - run: zip -r build.zip build
      - uses: softprops/action-gh-release@v1
        with:
          files: build.zip
```

---

## 📋 Lista de verificação pré-publicação
- ✅ Testes passando  
- ✅ Lint sem erros  
- ✅ Documentação atualizada  
- ✅ Changelog completo  
- ✅ Mudanças incompatíveis destacadas  
- ✅ Artefatos compilados e verificados  
- ✅ Checksums inclusos (SHA256)  
- ✅ Comunicação clara (README, site, feed de release)

---

## 🎯 Boas práticas
- **Pré-release para testes:** use `--prerelease` para versões beta/RC.  
- **Assinaturas e checksums:** forneça SHA256 e assinatura (GPG, assinatura de código).  
- **Changelog contínuo:** atualize com cada PR usando categorias padronizadas.  
- **Automação:** use GitHub Actions para CI/CD.  
- **Referências:** mencione issues e PRs com `Closes #123` e credite com @mentions.
