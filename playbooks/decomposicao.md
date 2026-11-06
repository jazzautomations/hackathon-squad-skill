# Playbook — Decomposição de tarefas (a parte que decide o hackathon)

> **Regra de ouro**: problemas independentes são a unidade de paralelismo. Dois agentes no mesmo arquivo = conflito comprado à vista. O trabalho do orquestrador não é distribuir tarefa — é **desenhar fronteiras** que fazem a colisão ser impossível por construção.

Isso se faz em 6 passos. Não pule nenhum: o tempo que você "economiza" pulando o grafo você paga triplicado resolvendo merge às 23h.

---

## Passo 0 — O demo decide o backlog

Antes de cortar tarefa, escreva **o roteiro do demo**: 60–90 segundos, 4–6 ações/telas, na perspectiva do jurado assistindo.

Exemplo: "abro o app → cadastro em 10s → simulo a ação principal → mostro o resultado → fecho com o número que impressiona".

**Só entra no board**: (a) o que aparece no roteiro, (b) o que sustenta tecnicamente o que aparece. Tudo mais é v2 — anota num `BACKLOG-V2.md` e esquece até sobrar tempo. Esse é o filtro que impede a feature brilhante-que-ninguém-vê de comer as horas do demo.

## Passo 1 — O contrato entra primeiro (sempre)

A fronteira entre as fatias precisa existir antes das fatias. O **contrato** é o conjunto de coisas que duas ou mais tarefas consomem mas nenhuma deveria inventar sozinha:

- Schema do banco (tabelas, colunas, relações)
- Tipos/interfaces compartilhados (TypeScript types, schemas de validação, protobuf)
- Shape das APIs (rota, método, request, response — mesmo que ainda 501)
- Eventos/mensagens entre módulos
- Convenções visuais (tokens, componentes-base)

O contrato vira o(s) primeiro(s) cartão(ões) do board — T001 (às vezes T001–T003) — e é **o único trabalho serializado do projeto**. Todo mundo espera ele mergiar; depois cada um trabalha em paralelo **contra a interface congelada**, não contra o código um do outro.

É o mesmo princípio do spec-first aplicado ao código: fronteira congelada é o que torna o paralelo sem colisão possível. E cuidado: contrato que muda depois é o gerador silencioso de conflitos — mudança de contrato passa pelo orquestrador e vira decisão registrada, nunca edição sorrateira dentro de outro cartão.

## Passo 2 — Fatie vertical demonstrável, não por camada gigante

**Errado**: "um faz o backend, um faz o frontend". Duas tarefas gigantes, integração só no fim — a caixa de surpresa clássica: na hora de juntar, nada conversa.

**Certo**: cada cartão entrega uma **fatia vertical pequena** — um pedaço do golden path de ponta a ponta (endpoint + a tela/handler que o consome), ou uma camada inteira **cuja fronteira é o contrato**.

Em hackathon com equipe pequena: prefira fatia vertical quando todos mexem na stack inteira; prefira divisão por camada quando cada pessoa só opera uma camada (um só front, um só back — aí a fronteira natural é a API do contrato).

## Passo 3 — Mapa de propriedade (ownership)

Tabela explícita: **cartão → arquivos/pastas que ele pode escrever**.

**Regra operacional**: nenhum arquivo aparece em dois cartões ao mesmo tempo. Se dois cartões precisam do mesmo arquivo:

- **Fundir** — vira um cartão só; ou
- **Sequenciar** — `depende de` no board, um entra antes do outro; ou
- **Extrair pro contrato** — a parte compartilhada sobe pro Passo 1 e os dois consomem.

Fronteira bem desenhada = merge sem conflito **por construção**, não por sorte.

## Passo 4 — Grafo de dependência → ordem de merge

Com os cartões cortados, liste o grafo: `T0xx → depende de → T0yy`.

- Merge = **travessia topológica**: quem não depende de nada entra primeiro.
- Dependência circular = erro de corte → refatore o corte, não o merge.
- Desenhe o grafo ANTES de soltar os agentes — é ele que dá a ordem da fila do Integrador.

```
contrato (T001)
 ├─→ seed/fixtures (T002)
 ├─→ endpoint principal (T003) ─→ tela que consome (T005)
 ├─→ lógica de negócio core (T004) ─→ tela de resultado (T006)
 └─→ auth mínima (T007) ─→ proteção de rotas (T008)
```

Ordem de merge resultante: T001 → T002 → T003/T004/T007 (paralelo) → T005/T006 → T008.

## Passo 5 — Regras do cartão

- **Tamanho**: 30–90 minutos de trabalho de agente. Maior que isso, corte de novo.
- **Critério**: um "pronto quando" testável — cada critério de aceite da spec vira um teste. Não cabe num teste? Critério vago → spec volta.
- **Um dono** por cartão (pessoa+agente). Sem dono = duplicidade garantida.
- **Spec linkada** — o cartão aponta pra `specs/<slug>/`, nunca pra "o que eu acho que é".
- **Deps explícitas** — "depende de" preenchido ou declarado "sem dependência".

**Cartão de seed é obrigatório**: os dados bonitos do demo (usuários, registros, o cenário que impressiona) são uma tarefa com dono — não um pensamento das 22h.

## Passo 6 — Protocolo de overlap

Precisou escrever em arquivo fora do seu mapa? PARE.

1. Avise o dono daquele arquivo/cartão.
2. Combine: ou ele faz o trecho, ou ele te cede um ponto de extensão, ou vira subtarefa sequenciada.
3. **Nunca edite calado** — é exatamente assim que nasce o conflito que ninguém esperava.

Edição de emergência em arquivo compartilhado (bug bloqueando dois cartões): o orquestrador autoriza, registra no board, e quem edita avisa no sync seguinte.

---

## Anti-cortes clássicos (erros de divisão que sempre voltam)

| Erro | Por que quebra | Correção |
|---|---|---|
| Util compartilhado criado em paralelo por 2 cartões | Dois `helpers.ts` divergentes → conflito certo | Sobe pro contrato (Passo 1) |
| Migrations de 2 cartões em paralelo | Ordem de migration ambígua, schema corrompido | Migrations sempre sequenciadas — um cartão por vez, ou todas no contrato |
| Cartão "integração" no fim | Integração acumulada = caixa de surpresa | Integre desde o primeiro merge; merge a cada 1–2h |
| Frontend esperando backend "de verdade" | Bloqueio em cascata | Front consome o contrato com mock — o shape já está congelado |
| Ninguém dono do seed | Demo com banco vazio | Cartão explícito com dono |
| Cartão "arrumar tudo"/"polish" | Sem fronteira = mexe em tudo = colide com todos | Polish vira cartões específicos por arquivo |
| Refatoração "de passagem" | Diff gigante, review impossível, conflito com cartões ativos | Refatoração é cartão próprio ou não acontece |

## Exemplo completo — do roteiro aos cartões

**Produto** (hackathon saúde): familiar recebe alerta quando idoso não confirma dose do remédio. Sensor simulado abre/fecha a caixa de remédio.

**Roteiro do demo (Passo 0)**: abro o painel do familiar → mostro o idoso "Carlos, 78" com o remédio das 14h → simulo a caixa não abrindo → alerta chega no painel do familiar em tempo real → mostro o histórico de adesão da semana → fecho com "87% das doses esquecidas viram esquecimento resolvido quando um familiar sabe".

**Contrato (Passo 1)** — T001: schema `idoso`, `medicacao`, `evento_dose{horario_previsto, horario_abertura, status}`, `alerta{tipo, status, destinatario}`; tipos TS; `POST /dose-events`, `GET /alertas`, `GET /adesao`; WebSocket/poll de alertas.

**Fatias + mapa (Passos 2–3)**:

| Cartão | Escopo de arquivos | Depende de |
|---|---|---|
| T001 contrato | `db/schema`, `types/`, `api/routes.ts` | — |
| T002 seed demo | `db/seed.ts`, dados do Carlos | T001 |
| T003 ingestão de eventos | `api/dose-events.ts`, lógica de status | T001 |
| T004 motor de alerta | `lib/alerta.ts` (timeout→alerta) | T001, T003 (contrato) |
| T005 painel familiar | `app/painel/*` | T001 (API mockada até T003/T004 entrarem) |
| T006 simulador da caixa | `tools/simulador.ts` (botão "abrir caixa") | T001, T003 |
| T007 histórico/adesão | `app/adesao/*`, `lib/metricas.ts` | T001, T003 |
| T008 auth mínima | `api/auth.ts`, middleware | T001 |
| T009 golden path E2E | `tests/e2e.spec` | T003–T007 |
| T010 demo hardening | `design/`, empty states, erro | T005+ |

**Ordem de merge**: T001 → T002 → T003 → {T004, T005 (mock→real), T006} → {T007, T008} → T009 → T010.

Repare: T005 trabalha contra a API mockada do contrato desde o minuto 1 — não espera T003. Isso é o contrato pagando: paralelo real, sem espera.

---

## Checklist do `/hackathon dividir`

- [ ] Roteiro do demo escrito e compartilhado
- [ ] T001 = contrato, definido com o time inteiro
- [ ] Todo cartão tem: dono, spec, mapa de arquivos, "pronto quando" testável, deps
- [ ] Zero arquivo em dois cartões simultâneos (conferido cartão a cartão)
- [ ] Grafo desenhado em DECISOES.md e ordem de merge no board
- [ ] Cartão de seed existe e tem dono
- [ ] Tudo que não aparece no roteiro do demo foi pro BACKLOG-V2
