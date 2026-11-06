# AGENTS.md — lei da casa (leia ANTES de qualquer coisa)

> Qualquer agente que abrir este repo lê este arquivo primeiro. Ele é o contrato: comandos, convenções e regras invioláveis. Preencha as seções [entre colchetes] no setup.

## O que estamos construindo

[1 frase: o produto, pra quem, e o golden path do demo]

## Stack

[linguagem, framework, banco, deploy — ex.: Next.js + Postgres/Supabase + Vercel]

## Comandos (o contrato de verificação)

```bash
# subir ambiente
[install cmd]              # ex.: pnpm install
[dev cmd]                  # ex.: pnpm dev — porta padrão 3000

# verificação — TUDO precisa estar verde antes de PR e depois de todo merge
[build cmd]                # ex.: pnpm build
[test cmd]                 # ex.: pnpm test
[lint cmd]                 # ex.: pnpm lint && pnpm typecheck
```

## As 7 leis (invioláveis)

1. Uma tarefa = um dono = uma branch = uma worktree. Nunca dois agentes no mesmo checkout. Nunca na `main` direto.
2. Marque "peguei" no `BOARD.md` ANTES de começar.
3. `main` SEMPRE demo-ready: só entra com CI verde + review. Main vermelha = prioridade zero.
4. Spec antes de código: cartão sempre aponta pra `specs/<slug>/spec.md`.
5. "Pronto" = teste do critério de aceite passando. Sem teste, não está pronto.
6. Só o Integrador mergia, em ordem de dependência, `--no-ff`. Rebase antes de pedir merge.
7. Decisão e dado têm fonte em `DECISOES.md`.

## Convenções

- **Branch**: `feature/tNNN-slug-curto` (ex.: `feature/t014-valida-cpf`)
- **Worktree**: `../<repo>-tNNN` — criar com `git worktree add ../<repo>-tNNN -b feature/tNNN-slug origin/main`
- **Porta dev por worktree**: `3000 + NNN` (T014 → porta 3014) — ajuste no `.env` local
- **Commits**: conventional — `feat:`, `fix:`, `test:`, `docs:`, `chore:` + referência ao cartão quando couber
- **PR**: usar `pull_request_template.md`, linkar o cartão (`Closes T014`), PR pequeno e revisável
- **`.env`**: nunca commitado. Copie do repo principal pra sua worktree. Secret vazado → rotaciona, não apaga commit.
- **Banco**: [schema/banco separado por worktree, ex.: `app_test_t014`] — migrations SEMPRE sequenciadas (um cartão por vez)
- **Deps**: [install cmd] em toda worktree nova. Nada de `latest` — versões fixas.

## Onde está o quê

- `BOARD.md` — quadro de tarefas (a fazer / fazendo / pronto). Estado do time mora aqui.
- `DECISOES.md` — decisões com motivo e fonte.
- `specs/` — spec → plan → tasks por feature.
- `design/` — specs de UX em markdown.

## Nunca

- Push direto na `main`, force-push, commit de secret, merge fora do Integrador
- Mexer em arquivo de outro cartão sem avisar o dono (protocolo de overlap no BOARD.md)
- `localhost`/porta hardcoded fora do `.env`, CORS `*`, stack trace em produção
