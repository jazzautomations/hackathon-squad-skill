## Cartão

Closes T___ — [título do cartão]
Spec: `specs/[slug]/spec.md`

## O que mudou

[2–4 linhas: o que entra neste merge e nada mais. Se tem coisa fora do escopo do cartão, explica por quê.]

## Como testar (o critério de aceite)

1. [passo reproduzível]
2. [o que deve acontecer]

## Evidência

- [ ] `[test cmd]` verde na minha worktree
- [ ] `[lint cmd]` verde
- [ ] Teste do critério de aceite: [nome do teste]
- [ ] `git rebase origin/main` feito, conflitos resolvidos, teste verde depois
- [ ] Sem secret/.env/debug no diff
- [ ] [screenshot/output se UI]

## Risco pro merge

[arquivos que outros cartões podem estar tocando? migrations? contrato mudou? → se mudou contrato, o orquestrador aprovou?]

## Depende de

[PRs que precisam entrar antes — ou "nenhum, entra quando o Integrador chamar"]
