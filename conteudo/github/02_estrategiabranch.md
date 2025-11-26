# Guia de Branches (Git) usando o Source Control do VS Code (logado no GitHub)

Este guia adapta o fluxo para usar o painel Source Control do VS Code com a conta do GitHub conectada.  
Objetivo: operar branches, commits, push e PRs pela interface do VS Code.

Pré-requisitos:
- Git instalado e configurado (nome e e‑mail).
- VS Code atualizado.
- Conecte sua conta GitHub: Accounts (canto inferior esquerdo) > Sign in to GitHub.
- Opcional: extensão “GitHub Pull Requests and Issues” para criar/gerenciar PRs dentro do VS Code.

---

## Começo rápido (clonar/publicar)

- Clonar do GitHub: Source Control > Clone Repository… > selecione o repo > escolha pasta.
- Iniciar repo local: Source Control > Initialize Repository > Publish to GitHub (cria repo remoto e configura “origin”).

---

## Estrutura de Branches

- main
    - Estável e liberável.
    - Só recebe código revisado/testado.
- feature/…
    - Uma por tarefa (ex.: feature/login).
    - Após concluir, abrir PR para main.

Dica: alterne a branch pelo seletor na status bar (canto inferior esquerdo).

---

## Fluxo no Source Control (VS Code + GitHub)

1) Atualizar a main
     - Troque para main na status bar.
     - Source Control > botão “Sync Changes” (faz fetch/pull/push) ou “…” > Pull.
     - Use “…” > Fetch para buscar atualizações sem integrar.

2) Criar a branch de feature
     - Clique no nome da branch (status bar) > Create new branch… (a partir de main).
     - Nomeie como feature/nome-da-tarefa.

3) Trabalhar e commitar
     - Source Control:
         - Selecione arquivos e use “+” para Stage.
         - Escreva a mensagem (ex.: feat(login): formulário inicial) > Commit.
         - Use stage parcial por hunk/linha no diff (botões no editor).
         - “Timeline” mostra histórico do arquivo.

4) Publicar a branch
     - Clique em Publish Branch (após criar) ou use Push/Sync Changes.
     - Confirme o remoto “origin” se solicitado.

5) Abrir Pull Request (PR)
     - Após o push, o VS Code exibe um toast “Create Pull Request”.
     - Também disponível em Source Control > “…” > Create Pull Request (requer extensão do GitHub).
     - Sem extensão: use “Open on GitHub” no toast/Status Bar e crie o PR no navegador.
     - Base: main | Compare: sua feature/…
     - Preencha título/descrição, adicione reviewers e verifique os Checks (Actions).

6) Merge para main
     - No GitHub: prefira “Squash and merge” para histórico limpo.
     - Depois do merge:
         - Volte para main (status bar) e faça Pull/Sync Changes.
         - Opcional: “…” > Delete Branch para remover a branch local já mesclada.

7) Excluir branch de feature
     - No GitHub: “Delete branch” após o merge.
     - Local: Source Control > “…” > Delete Branch.
     - Se necessário remover no remoto: “…” > Push… (apaga branch remota) ou menu Branches na aba Source Control.

---

## Estratégias de Branching

### Git Flow

O Git Flow é uma estratégia popular para gerenciar branches em projetos colaborativos.

- **main**: Contém o código pronto para produção.
- **develop**: Branch principal para desenvolvimento.
- **feature/**: Branches para novas funcionalidades.
- **release/**: Preparação para uma nova versão.
- **hotfix/**: Correções urgentes em produção.

### Trunk-Based Development

Uma abordagem mais simples, onde todos os desenvolvedores trabalham diretamente na `main` ou em branches curtas.

- Ideal para equipes pequenas.
- Requer integração contínua (CI) para evitar conflitos.

---

## Resolvendo Conflitos no VS Code

1. Ao tentar fazer merge, o Git pode indicar conflitos.
2. No VS Code, os arquivos conflitantes aparecem no Source Control.
3. Clique em um arquivo para abrir o editor de conflitos.
4. Escolha entre as mudanças ou combine-as manualmente.
5. Após resolver, marque o arquivo como resolvido:

```bash
git add arquivo-conflito
```

6. Finalize o merge:

```bash
git commit
```

---

## Boas Práticas

- Nomes claros: feature/, bugfix/, docs/.
- Commits pequenos e atômicos: feat:, fix:, docs:. Use stage seletivo.
- Proteja a main: rode testes antes do PR (Terminal integrado: npm test, pnpm test, pytest…).
- PR obrigatório com pelo menos 1 reviewer.
- Atualize sempre: Fetch/Pull antes de começar.
- Evite temporários: confira .gitignore; não faça stage de node_modules, .env etc.

---

## Visual do fluxo

```
main ──►───────────────┐──────────────
                                                                                         │
feature/login ──► PR ──┘
feature/upload ──► PR ─┐
                                                                                                └────► main
```

---

## Checklist de PR

- [ ] Build/execução local sem erros (Terminal integrado).
- [ ] Testes passam localmente e nos Checks do PR.
- [ ] Sem temporários em “Changes” (node_modules, .env).
- [ ] Commits claros e atômicos.
- [ ] Revisado por 1+ colega.

Dicas rápidas (Source Control):
- Alternar branch: clique na branch na status bar.
- Ver diffs/inline: clique no arquivo em Changes.
- Resolver conflitos: abra “Merge Changes” e use Accept Current/Incoming/Both.
- Stash: “…” > Stash / Apply Stash para trocar de branch sem commitar.
- Sincronizar fork: “…” > Fetch de upstream (se configurado) e Pull conforme necessário.
