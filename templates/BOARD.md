# BOARD — o quadro do time

> Estado do time mora aqui, versionado com o código. Regras: cartão sem dono não existe; "peguei" se marca ANTES de começar; "pronto" só com teste verde do critério.

## Roteiro do demo (o filtro do backlog)

[60–90s, 4–6 ações, na perspectiva do jurado. Só entra no board o que aparece aqui ou sustenta o que aparece.]

## Grafo de dependência → ordem de merge

```
[desenhar — ex.: T001 contrato → T002 seed → T003 api → {T004,T005,T006} → T007 e2e]
```

Ordem de merge: [T001 → T002 → ...]

## A fazer

<!-- copie o bloco de cartão abaixo -->

### [T001] Contrato: schema + tipos + shape de API
- Dono: [pessoa + agente]
- Worktree: ../[repo]-t001
- Branch: feature/t001-contrato
- Spec: specs/core/spec.md
- Arquivos: `db/schema`, `types/`, `api/routes.ts`
- Depende de: —
- Pronto quando: schema migrado, tipos exportados, rotas respondendo 501 com shape documentado, teste de contrato verde

### [T002] Seed de dados do demo
- Dono:
- Worktree:
- Branch:
- Spec:
- Arquivos: `db/seed.ts`
- Depende de: T001
- Pronto quando: cenário do demo popula o banco com 1 comando; dados bonitos o suficiente pra impressionar

## Fazendo

<!-- cartões em execução — mova pra cá quando marcar "peguei" -->

## Pronto (aguardando merge)

## Feito (merged)

## Travado / ajuda

<!-- o que está bloqueando, há quanto tempo, quem pode destravar -->
