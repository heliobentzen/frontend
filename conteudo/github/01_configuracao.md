# GitHub + GitHub Desktop + VS Code: guia prático

Antes de começar: termos essenciais
- Repositório (repo): pasta versionada do projeto, local e/ou no GitHub.
- Branch: linha de desenvolvimento isolada (main é a principal).
- Commit: “fotografia” das mudanças com mensagem descritiva.
- Push: envia seus commits locais para o remoto (GitHub).
- Pull: traz commits do remoto para sua cópia local.
- Pull Request (PR): pedido para revisar e mesclar uma branch em outra no GitHub.
- Merge: integra mudanças de uma branch em outra.
- Rebase: reaplica seus commits sobre a base atualizada, mantendo histórico linear.
- Clone: cria uma cópia local de um repositório remoto.
- Fork: copia um repositório para sua conta para contribuir sem acesso direto.
- Remote: referência a um repositório remoto (origin: o seu; upstream: o original).
- HEAD: ponteiro para o commit/branch atual.
- Stage (index): área onde você seleciona o que entra no próximo commit.
- Stash: guarda alterações temporariamente sem commitar.
- .gitignore: lista de arquivos/pastas que o Git deve ignorar.
- Git LFS: suporte para armazenar arquivos grandes (mídia/datasets).
- Issue: tarefa, bug ou sugestão rastreada no GitHub.
- CI/CD (GitHub Actions): automação de build, testes e deploy.

Este material mostra como criar, clonar, versionar e colaborar em projetos usando GitHub Desktop integrado ao Visual Studio Code (VS Code).

## 1) Pré‑requisitos
- Conta no GitHub.
- GitHub Desktop instalado.
- Visual Studio Code instalado.
- Git (instalado automaticamente com o GitHub Desktop ou separado).

## 2) Configuração inicial
- Abra o GitHub Desktop e faça login com a conta do GitHub (File > Options > Accounts).
- Em Options > Integrations, defina “External editor: Visual Studio Code”.
- Verifique nome e e‑mail do Git (Options > Git). Se preferir, no terminal do VS Code:
    - git config --global user.name "Seu Nome"
    - git config --global user.email "seu@email.com"

## 3) Criar ou clonar repositórios
- Criar do zero:
    - GitHub Desktop > File > New repository.
    - Escolha pasta local, nome do repositório, adicione README, .gitignore e licença se necessário.
    - Clique “Create repository” e depois “Publish repository” para enviar ao GitHub.
- Clonar existente:
    - GitHub Desktop > File > Clone repository.
    - Selecione da sua conta ou informe a URL.
    - Defina a pasta local e conclua.
- Abrir no VS Code:
    - No GitHub Desktop, Use “Open in Visual Studio Code” para trabalhar no editor.

## 4) Fluxo básico de trabalho (Desktop + VS Code)
1) Atualize sua branch:
     - GitHub Desktop: “Fetch origin” e “Pull origin”.
2) Crie uma branch de feature:
     - Branch > New branch... (ex.: feat/login-pagina).
     - Publique a branch (“Publish branch”) para colaborar.
3) Edite no VS Code:
     - Faça alterações, rode e teste localmente.
4) Selecione arquivos e faça commit:
     - GitHub Desktop: marque os arquivos alterados, escreva uma mensagem objetiva (ex.: feat: adiciona formulário de login) e clique “Commit to [sua-branch]”.
     - Opcional no VS Code: use o painel Source Control para stage/commit.
5) Envie ao remoto:
     - “Push origin” no Desktop (ou “Sync Changes” no VS Code).
6) Abra um Pull Request (PR):
     - GitHub Desktop: “Create Pull Request”.
     - Descreva o que mudou, relacione issues e solicite revisão.
7) Faça o merge e atualize:
     - Após aprovações e checks, faça merge no GitHub.
     - De volta ao Desktop: mude para main, “Pull origin” e delete a branch antiga se desejar.

## 4) GitHub Actions: CI/CD Simplificado

O GitHub Actions permite automatizar tarefas como build, testes e deploy. Para configurar:

1. Crie um arquivo `.github/workflows/ci.yml` no repositório.
2. Exemplo de workflow para Node.js:

```yaml
name: CI

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout código
        uses: actions/checkout@v3

      - name: Configurar Node.js
        uses: actions/setup-node@v3
        with:
          node-version: 16

      - name: Instalar dependências
        run: npm install

      - name: Rodar testes
        run: npm test
```

## 5) Configurando múltiplos remotes

Se você trabalha com forks, configure o `upstream` para manter seu fork atualizado:

```bash
git remote add upstream https://github.com/usuario/original-repo.git
git fetch upstream
git merge upstream/main
```

## 6) Exemplo de .gitignore

Adicione um arquivo `.gitignore` para evitar versionar arquivos desnecessários:

```
node_modules/
.env
*.log
```

Para projetos com arquivos grandes, use o Git LFS:

```bash
git lfs install
git lfs track "*.psd"
```

## 7) Integração no VS Code
- Controle de versão:
    - Ícone “Source Control” (Ctrl+Shift+G): visualizar mudanças, stage, commit, push/pull.
- Extensões recomendadas:
    - GitHub Pull Requests and Issues (revisar/gerenciar PRs e issues).
    - GitLens (histórico, blame, insights).
    - EditorConfig (padronização de formatação).
- Autenticação:
    - Ao usar GitHub PRs, faça login no GitHub dentro do VS Code quando solicitado.
- Convenções:
    - Mensagens curtas e descritivas; adote Conventional Commits (feat, fix, chore, docs).
    - Padrões de branch: feat/, fix/, chore/, hotfix/.

## 8) .gitignore, secrets e LFS
- Configure .gitignore ao criar o repositório (ex.: Node, Python, .NET).
- Nunca faça commit de segredos (.env, chaves). Use variáveis de ambiente e GitHub Secrets.
- Arquivos grandes (mídia/datasets): considere Git LFS.

## 9) Atualizar, sincronizar e colaborar
- Sincronizar com a origem:
    - Sempre “Fetch/Pull” antes de iniciar uma nova tarefa.
- Rebase/merge:
    - Para manter histórico linear, use “Rebase current branch” no Desktop quando aplicável.
- Revisão de código:
    - No VS Code (extensão GitHub PRs): confira diffs, comente por linha, aprove/reprove.
- Repositórios forkados:
    - Adicione “upstream” no Desktop (Repository > Repository Settings > Remotes) para acompanhar o repositório original.

## 10) Resolver conflitos
- Ao puxar/merger com conflitos, o Desktop indica os arquivos.
- Abra no VS Code, localize marcadores <<<<<<<, =======, >>>>>>> e escolha as mudanças corretas.
- Teste, marque como resolvido (stage), faça commit e finalize o merge/rebase pelo Desktop.

## 11) Boas práticas
- Commits pequenos e frequentes; um tema por commit.
- Pull Requests curtos com descrição clara, screenshots se visual.
- Proteja a branch main (branch protection, reviews obrigatórias, CI).
- Automatize checks (lint, testes) no GitHub Actions.
- Use Issues/Projects para planejar e rastrear trabalho.

## 12) Problemas comuns e soluções
- Solicitação de senha ao fazer push:
    - Com Desktop, autenticação é integrada. No CLI, use Personal Access Token em vez de senha.
- Nome/e‑mail incorretos no histórico:
    - Ajuste git config e faça novos commits; histórico antigo só muda com reescrita (evite em main pública).
- Permissão negada:
    - Confirme acesso no GitHub (colaborador, organização) e URL correta (HTTPS/SSH).
- Não consegue push na main:
    - Verifique regras de proteção ou crie PR a partir de uma branch de feature.
- Arquivos indesejados no commit:
    - Atualize .gitignore e remova-os do index:
        - git rm -r --cached pasta-ou-arquivo
        - git commit -m "chore: limpa artefatos versionados por engano"

## 13) Comandos úteis (opcional, via terminal do VS Code)
- Ver estado: git status
- Criar branch: git checkout -b feat/minha-branch
- Atualizar local: git pull
- Enviar commits: git push -u origin feat/minha-branch
- Corrigir último commit (mensagem): git commit --amend
- Stash rápido: git stash; voltar: git stash pop

Resumo: use o GitHub Desktop para orquestrar branches, commits, push/pull e PRs, e o VS Code para editar, revisar diffs e interagir com GitHub via extensões. Esse combo acelera o fluxo de trabalho com uma curva de aprendizado suave.