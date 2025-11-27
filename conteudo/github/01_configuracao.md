# GitHub + GitHub Desktop + VS Code: guia prático

Antes de começar: termos essenciais
- **Repositório (repo)**: Pasta versionada do projeto, local e/ou no GitHub.
- **Branch**: Linha de desenvolvimento isolada (main é a principal).
- **Commit**: “Fotografia” das mudanças com mensagem descritiva.
- **Push**: Envia seus commits locais para o remoto (GitHub).
- **Pull**: Traz commits do remoto para sua cópia local.
- **Pull Request (PR)**: Pedido para revisar e mesclar uma branch em outra no GitHub.
- **Merge**: Integra mudanças de uma branch em outra.
- **Rebase**: Reaplica seus commits sobre a base atualizada, mantendo histórico linear.
- **Clone**: Cria uma cópia local de um repositório remoto.
- **Fork**: Copia um repositório para sua conta para contribuir sem acesso direto.
- **Remote**: Referência a um repositório remoto (origin: o seu; upstream: o original).
- **HEAD**: Ponteiro para o commit/branch atual.
- **Stage (index)**: Área onde você seleciona o que entra no próximo commit.
- **Stash**: Guarda alterações temporariamente sem commitar.
- **.gitignore**: Lista de arquivos/pastas que o Git deve ignorar.
- **Git LFS**: Suporte para armazenar arquivos grandes (mídia/datasets).
- **Issue**: Tarefa, bug ou sugestão rastreada no GitHub.

Este material mostra como criar, clonar, versionar e colaborar em projetos usando GitHub Desktop integrado ao Visual Studio Code (VS Code).

---

## 1) Pré‑requisitos
- Conta no GitHub.
- GitHub Desktop instalado.
- Visual Studio Code instalado.
- Git (instalado automaticamente com o GitHub Desktop ou separado).

---

## 2) Configuração inicial
- Abra o GitHub Desktop e faça login com a conta do GitHub (File > Options > Accounts).
- Em Options > Integrations, defina “External editor: Visual Studio Code”.
- Verifique nome e e‑mail do Git (Options > Git). Se preferir, no terminal do VS Code:
    ```bash
    git config --global user.name "Seu Nome"
    git config --global user.email "seu@email.com"
    ```

---

## 3) Criar ou clonar repositórios

### Criar do zero
1. No GitHub Desktop, vá em **File > New repository**.
2. Preencha os campos obrigatórios (nome, descrição, visibilidade).
3. Clique em **Create repository**.

### Clonar um repositório existente
1. No GitHub Desktop, vá em **File > Clone repository**.
2. Escolha o repositório na lista ou insira a URL.
3. Escolha a pasta local onde o repositório será salvo.

---

## 4) Pull Request: O que é e como criar

Um **Pull Request (PR)** é uma solicitação para mesclar mudanças de uma branch em outra. Ele é usado para revisar o código antes de integrá-lo ao projeto principal.

### Passo a passo para criar um Pull Request
1. **Crie uma branch**:
    - No GitHub Desktop, clique em **Current Branch > New Branch**.
    - Dê um nome descritivo à branch (ex.: `feature/login-page`).
2. **Faça alterações e commits**:
    - Edite os arquivos necessários no VS Code.
    - No GitHub Desktop, adicione as alterações ao stage e faça commits com mensagens claras.
3. **Publique a branch**:
    - Clique em **Publish Branch** no GitHub Desktop.
4. **Abra o Pull Request**:
    - No GitHub, acesse o repositório e clique em **Pull Requests > New Pull Request**.
    - Escolha a branch de origem e a branch de destino (ex.: `feature/login-page` para `main`).
    - Adicione um título e uma descrição explicando as mudanças.
    - Clique em **Create Pull Request**.

### Dicas para um bom Pull Request
- Escreva um título claro e objetivo.
- Descreva o que foi feito, por que foi feito e como testar.
- Divida mudanças grandes em PRs menores e mais fáceis de revisar.
- Resolva conflitos antes de solicitar a revisão.

---

## 5) Usando o Source Control do VS Code

O Visual Studio Code possui uma interface integrada para gerenciar repositórios Git. Veja como realizar as principais operações diretamente pelo VS Code:

### Criar ou Clonar Repositórios

#### Criar um Repositório Local
1. No VS Code, clique no ícone de **Source Control** (barra lateral esquerda).
2. Clique em **Initialize Repository**.
3. O VS Code criará um repositório Git na pasta atual.

#### Clonar um Repositório
1. No VS Code, pressione `Ctrl+Shift+P` (ou `F1`) para abrir a paleta de comandos.
2. Digite e selecione **Git: Clone**.
3. Insira a URL do repositório remoto.
4. Escolha a pasta local onde o repositório será salvo.

---

### Criar e Alternar Branches
1. No canto inferior esquerdo, clique no nome da branch atual.
2. Clique em **Create New Branch** e insira um nome descritivo (ex.: `feature/login-page`).
3. Para alternar entre branches, clique novamente no nome da branch e selecione a desejada.

---

### Fazer Commits
1. Após editar arquivos, clique no ícone de **Source Control**.
2. Os arquivos modificados aparecerão na seção **Changes**.
3. Clique no ícone de **+** ao lado de cada arquivo para adicioná-lo ao stage.
4. Insira uma mensagem de commit no campo de texto e clique no ícone de **✔** para confirmar.

---

### Fazer Push e Pull
- **Push**: Clique nos três pontos (`...`) no painel de Source Control e selecione **Push** para enviar os commits para o repositório remoto.
- **Pull**: Clique nos três pontos (`...`) e selecione **Pull** para trazer as alterações do repositório remoto.

---

### Criar um Pull Request
1. Certifique-se de que a extensão **GitHub Pull Requests and Issues** está instalada.
2. Após fazer o push da branch, clique em **Create Pull Request** no painel de Source Control.
3. Preencha o título e a descrição do PR diretamente no VS Code.
4. Clique em **Submit** para criar o Pull Request no GitHub.

---

### Criar um Pull Request 

Você pode criar um Pull Request diretamente pelo site do GitHub. Siga os passos abaixo:

1. **Faça o Push da Branch**:
    - Certifique-se de que suas alterações estão na branch correta.
    - Use o comando `git push` no terminal ou a interface do Source Control no VS Code para enviar a branch ao repositório remoto.

2. **Acesse o Repositório no GitHub**:
    - Abra o navegador e vá até o repositório no GitHub.

3. **Inicie o Pull Request**:
    - No topo da página do repositório, clique na aba **Pull Requests**.
    - Clique no botão **New Pull Request**.

4. **Selecione as Branches**:
    - Escolha a branch de origem (a que contém suas alterações) e a branch de destino (geralmente `main` ou `develop`).

5. **Preencha os Detalhes**:
    - Adicione um título descritivo e uma explicação clara das mudanças realizadas.
    - Inclua informações sobre como testar as alterações, se necessário.

6. **Crie o Pull Request**:
    - Clique em **Create Pull Request** para finalizar.

---

### Resolver Conflitos
1. Após um **Pull** ou **Merge**, o VS Code indicará os arquivos com conflitos.
2. Clique em um arquivo para abrir o editor de conflitos.
3. Use os botões **Accept Current Change**, **Accept Incoming Change** ou **Accept Both Changes** para resolver os conflitos.
4. Após resolver, adicione o arquivo ao stage e faça o commit.

---

## 6) Configurando múltiplos remotes

Se você trabalha com forks, configure o `upstream` para manter seu fork atualizado:

```bash
git remote add upstream https://github.com/usuario/original-repo.git
git fetch upstream
git merge upstream/main
```

## 7) Exemplo de .gitignore

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

## 8) Integração no VS Code
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

## 9) .gitignore, secrets e LFS
- Configure .gitignore ao criar o repositório (ex.: Node, Python, .NET).
- Nunca faça commit de segredos (.env, chaves). Use variáveis de ambiente e GitHub Secrets.
- Arquivos grandes (mídia/datasets): considere Git LFS.

## 10) Atualizar, sincronizar e colaborar
- Sincronizar com a origem:
    - Sempre “Fetch/Pull” antes de iniciar uma nova tarefa.
- Rebase/merge:
    - Para manter histórico linear, use “Rebase current branch” no Desktop quando aplicável.
- Revisão de código:
    - No VS Code (extensão GitHub PRs): confira diffs, comente por linha, aprove/reprove.
- Repositórios forkados:
    - Adicione “upstream” no Desktop (Repository > Repository Settings > Remotes) para acompanhar o repositório original.

## 11) Resolver conflitos
- Ao puxar/merger com conflitos, o Desktop indica os arquivos.
- Abra no VS Code, localize marcadores <<<<<<<, =======, >>>>>>> e escolha as mudanças corretas.
- Teste, marque como resolvido (stage), faça commit e finalize o merge/rebase pelo Desktop.

## 12) Boas práticas
- Commits pequenos e frequentes; um tema por commit.
- Pull Requests curtos com descrição clara, screenshots se visual.
- Proteja a branch main (branch protection, reviews obrigatórias, CI).
- Automatize checks (lint, testes) no GitHub Actions.
- Use Issues/Projects para planejar e rastrear trabalho.

## 13) Problemas comuns e soluções
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

## 14) Comandos úteis (opcional, via terminal do VS Code)
- Ver estado: git status
- Criar branch: git checkout -b feat/minha-branch
- Atualizar local: git pull
- Enviar commits: git push -u origin feat/minha-branch
- Corrigir último commit (mensagem): git commit --amend
- Stash rápido: git stash; voltar: git stash pop

Resumo: use o GitHub Desktop para orquestrar branches, commits, push/pull e PRs, e o VS Code para editar, revisar diffs e interagir com GitHub via extensões. Esse combo acelera o fluxo de trabalho com uma curva de aprendizado suave.