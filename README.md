# hackathon-squad-skill

Metodologia de squad multi-agente pra hackathon, empacotada como skill de
agente (Devin/agents/Claude-compatible). Ela existe porque o fracasso padrão
de hackathon é conhecido: vários agentes no mesmo checkout, conflito de
merge generalizado, ninguém sabendo quem faz o quê, main quebrada na hora
do demo, e pitch improvisado em cima de um produto "quase pronto".

## O que ela faz

Transforma o caos em pipeline:

```
pesquisa → debate → proposta → red team → spec → dividir → task → merge → audit → pitch
```

- **Lê o edital do SEU hacka antes de tudo** (`CONTEXTO.md`) — duração,
  rubrica e formato de julgamento mudam tudo; a metodologia adapta em cima.
- **Decompõe sem colisão** — um cartão, um dono, uma branch, uma worktree,
  um mapa de arquivos.
- **Spec antes de código** — critério de aceite testável ou não vira tarefa.
- **Main sempre demo-ready** — nada entra sem teste verde + review.
- **Red team e audit com evidência** — "não sei" = "não feito".
- **Submissão decomposta como workstream** — roteiro, vídeo, Q&A e upload
  são cartões com dono, não surto de 23h.

## Instalação

Copie a pasta pro seu diretório de skills:

```bash
git clone https://github.com/jazzautomations/hackathon-squad-skill
cp -r hackathon-squad-skill ~/.config/devin/skills/hackathon
# ou .agents/skills/hackathon no repo do projeto
```

## Uso

```
/hackathon contexto   # MINUTO 0: edital → CONTEXTO.md (parametriza tudo)
/hackathon aula       # mini-curso dos conceitos pras pessoas/agentes novos
/hackathon setup      # papéis, AGENTS.md, board, repo protegido, baseline
/hackathon pesquisa   # multi-perspectiva → debate → proposta → red team
/hackathon spec       # proposta → spec/plan/tasks com aceite testável
/hackathon dividir    # cartões + grafo de dependência + ordem de merge
/hackathon task       # executor: worktree → teste → PR → rebase
/hackathon merge      # integrador: merge em ordem, main verde sempre
/hackathon audit      # gates P0/P1/P2 com evidência
/hackathon pitch      # narrativa, demo script, Q&A, sabatina de jurado
/hackathon status     # radiografia do time em 10 linhas
```

Sem argumento → `status`.

## Estrutura

| Pasta | Conteúdo |
|---|---|
| `SKILL.md` | A metodologia: 7 leis, modelo mental, modos, cronograma |
| `playbooks/` | `decomposicao.md`, `redteam.md`, `audit.md`, `pitch.md`, `submissao.md` |
| `templates/` | `CONTEXTO.md`, `AGENTS.md`, `BOARD.md`, `spec.md`, `plan.md`, `tasks.md`, `DECISOES.md`, `pull_request_template.md`, `design-spec.md` |

## As 7 leis (resumo)

0. O edital manda; a metodologia adapta.
1. Uma tarefa = um dono = uma branch = uma worktree.
2. Marque "peguei" ANTES de começar.
3. A `main` está SEMPRE demo-ready.
4. Spec antes de código.
5. "Pronto" é testável.
6. Só o Integrador mergia, em ordem de dependência.
7. Decisão e dado têm fonte registrada em `DECISOES.md`.

## Quando usar / não usar

- **Use**: hackathons com 2+ pessoas/agentes, qualquer duração (a skill
  escala: 8h comprimido, 48h completo, 30 dias em cadência).
- **Não precisa**: projeto solo de um agente só num checkout — as leis
  continuam valendo, mas worktree/integrador é cerimônia a mais.

Feito pra Hack Brasil 2026 — mas serve em qualquer hacka com entrega de
software. PRs bem-vindos.
