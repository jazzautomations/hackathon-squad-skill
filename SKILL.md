---
name: hackathon
description: "Metodologia adaptativa de squad multi-agente pra hackathon — lê o edital e o contexto do SEU hacka antes de tudo, decomposição de tarefas sem colisão, worktree por tarefa, spec antes de código, teste antes de merge, main sempre demo-ready, red team, audit e pitch. Uso: /hackathon [contexto|aula|setup|pesquisa|spec|dividir|task|merge|audit|pitch|status]"
argument-hint: "[contexto|aula|setup|pesquisa|spec|dividir|task|merge|audit|pitch|status] [contexto]"
allowed-tools:
  - read
  - edit
  - grep
  - glob
  - exec
  - web_search
triggers:
  - user
  - model
---

# Hackathon Squad — metodologia de operação

Você opera dentro de uma squad de hackathon com esta metodologia. Ela existe porque o fracasso padrão é conhecido: vários agentes no mesmo checkout, conflito de merge generalizado, ninguém sabendo quem faz o quê, main quebrada na hora do demo, e um pitch improvisado em cima de um produto "quase pronto".

**Arquivos desta skill** (mesma pasta deste SKILL.md): `playbooks/` tem os manuais de profundidade — `decomposicao.md`, `redteam.md`, `audit.md`, `pitch.md`, `submissao.md`. `templates/` tem os arquivos prontos pra copiar pro repo — `CONTEXTO.md`, `AGENTS.md`, `BOARD.md`, `spec.md`, `plan.md`, `tasks.md`, `DECISOES.md`, `pull_request_template.md`, `design-spec.md`. Quando um modo mandar, leia o playbook/template correspondente e siga como checklist.

## As 7 leis — invioláveis, em qualquer modo

0. **O edital manda; a metodologia adapta.** Antes de QUALQUER decisão, o `CONTEXTO.md` existe e está certo: formato, rubrica, requisitos, duração, submissão. Hackathon não é um só formato — o que ganha um expo de 8h mata um pitch stage de 48h. Todo modo consulta o contexto antes de agir.
1. **Uma tarefa = um dono = uma branch = uma worktree.** Nunca dois agentes no mesmo checkout. Nunca trabalhe direto na `main`.
2. **Marque "peguei" ANTES de começar.** Atualize seu cartão no `BOARD.md` antes da primeira linha de código.
3. **A `main` está SEMPRE demo-ready.** Nada entra sem teste verde + review de quem não é autor. Main vermelha = prioridade zero do time inteiro, acima de qualquer feature.
4. **Spec antes de código.** Cartão só existe apontando pra `specs/<slug>/spec.md` com critérios de aceite objetivos. Sem spec, não há tarefa.
5. **"Pronto" é testável.** Critério de aceite vira teste; teste verde é a única prova de pronto. "Quase pronto" não mergia.
6. **Só o Integrador mergia, em ordem de dependência, com `--no-ff`.** Dono de tarefa faz `git rebase origin/main` e resolve conflito na PRÓPRIA worktree antes de pedir merge.
7. **Decisão e dado têm fonte registrada** em `DECISOES.md`. "O agente falou" não é fonte. Número sem origem é número inventado.

## Modelo mental — o porquê de cada peça

Agente que entende o porquê decide certo quando a regra não cobre o caso. Leia antes de operar.

**Contexto primeiro — a metodologia é espinha dorsal, não camisa de força.** Cada hackathon é uma brisa: duração, formato, rubrica e requisitos mudam tudo. Por isso a skill roda `contexto` antes de qualquer coisa e produz `CONTEXTO.md` — o perfil DESTE hacka. A partir daí tudo adapta: o cronograma escala pela duração real; a rubrica oficial vira o mapa do pitch; os requisitos do edital viram o gate do audit; o formato de julgamento (expo? pitch stage? vídeo? jurado abre o app?) dita o que o Demo keeper protege; tracks de patrocinador informam escopo. O que não muda são as 7 leis — elas evitam o fracasso operacional em qualquer formato. O que muda é pra onde elas apontam.

**Worktree.** Uma pasta de repo só olha pra uma branch por vez. `git worktree` cria várias pastas do mesmo projeto, cada uma numa branch, compartilhando o mesmo `.git`. Cada agente trabalha na sua pasta sem ver (e sem estragar) o trabalho alheio. O conflito não desaparece — é **adiado pra hora controlada do merge**, em vez de explodir em tempo real. **Limite do isolamento:** worktree isola ARQUIVO, não porta de servidor, banco, container nem `.env`. Duas worktrees rodando dev na porta 3000 colidem; `.env` não é trackeado e precisa ser copiado na mão; dependências precisam ser instaladas em cada pasta.

**Decomposição.** Problemas independentes são a unidade de paralelismo. O trabalho real do orquestrador não é distribuir — é **desenhar fronteiras**: contrato/interface primeiro, um arquivo em um único cartão por vez, grafo de dependência determinando ordem de merge. Dois agentes no mesmo arquivo = conflito comprado à vista. Manual completo: `playbooks/decomposicao.md`.

**Spec.** A memória do agente é descartável — a próxima sessão não lembra da decisão desta. O que sobrevive é o que está escrito no repo. Spec é a fonte da verdade persistente entre sessões, agentes e turnos. Sem spec, cada sessão "reinventa" decisão fechada e o produto vira colcha de decisões contraditórias. Critério de aceite = unit test dos requisitos: se não dá pra testar, não está especificado.

**Board.** "Quem tá fazendo o quê" se responde pelo repo, não por reunião. `BOARD.md` versionado funciona pra humano E agente — qualquer um lê o estado do time em 5 segundos. "Marcar peguei antes" elimina sozinho a maior parte da duplicidade.

**Main demo-ready.** No hackathon o produto É o demo — não é o deck nem a promessa. Uma main que roda o golden path vale mais que três features pela metade. Toda decisão de escopo se responde com: "isso deixa a main mais demonstrável?"

**Teste na régua de hackathon.** Não é cobertura de produção — é seguro do demo: unitário na lógica crítica (a que valida, calcula, decide) + UM E2E do golden path (o fluxo que você vai mostrar na banca, ponta a ponta) + lint/typecheck no CI. Cobertura é sinal, não meta: cubra primeiro o que, se quebrar, quebra o demo.

**Contrato primeiro.** O único trabalho serializado do projeto é a fronteira: schema, tipos, shape de API, eventos. O contrato mergia, depois todos trabalham em paralelo CONTRA a interface — não contra o código um do outro. É o mesmo princípio da spec-first aplicado ao código.

**Papéis.** Orquestrador (dono do board, prioridade, corte de escopo — não decide implementação); Dono de tarefa (1 pessoa+agente por cartão, decide o COMO); Integrador rotativo (único que mergia, reveza a cada ciclo — não rejeita por gosto); Crítico adversarial (ataca a proposta antes dela virar código — NUNCA quem teve a ideia); Liaison (registra em DECISOES.md, garante que ninguém fica no escuro); **Demo keeper** (alguém — humano ou agente — cuja única métrica é a main demonstrável: roda o golden path, cuida do seed, vigia deploy). Em time de 2: um faz orquestração+crítica+liaison, o outro+agentes fazem build e revezam integração.

## Estrutura do repo

```
CONTEXTO.md          → perfil DESTE hackathon (template em templates/CONTEXTO.md): edital, rubrica, formato — parametriza tudo
AGENTS.md            → lei da casa (template em templates/AGENTS.md): stack, comandos, convenções, leis
BOARD.md             → quadro: a fazer / fazendo / pronto, um cartão por tarefa
DECISOES.md          → decisões com motivo e fonte (ADR light)
pull_request_template.md → template de PR
specs/<slug>/{spec,plan,tasks}.md → spec (o quê/por quê/aceite), plan (como), tasks (cartões)
design/              → specs de UX em markdown (estados, erro, empty state) — agente lê texto, não Figma
```

## Modos

Sem argumento → `status`.

| Modo | Quem roda | O que faz |
|---|---|---|
| `contexto` | squad inteira, MINUTO 0 | Lê edital/regras do hacka → `CONTEXTO.md` que parametriza tudo |
| `aula` | todo mundo na hora 0 | Mini-curso: conceitos + o porquê das regras + quiz |
| `setup` | orquestrador | Papéis, AGENTS.md, board, repo protegido, baseline verde |
| `pesquisa` | squad inteira | Multi-perspectiva → debate → proposta → red team |
| `spec` | orquestrador+dev | spec/plan/tasks por feature aprovada |
| `dividir` | orquestrador | Decomposição em cartões + grafo + ordem de merge |
| `task` | executor | Pegar cartão → worktree → teste → PR → rebase |
| `merge` | integrador | Merge em ordem de dependência, main verde sempre |
| `audit` | auditor | Gate pré-merge e auditoria pré-demo com evidência |
| `pitch` | liaison+orquestrador | Narrativa, demo script, Q&A, sabatina |
| `status` | qualquer um | Radiografia do time em 10 linhas |

---

### `/hackathon contexto` — leitura do edital (MINUTO 0, antes de tudo)

Nenhum hackathon é igual ao outro. Este modo transforma o edital em `CONTEXTO.md` — o perfil que parametriza todos os outros modos. Rode com o edital/regras em mãos (link, PDF, página do Devpost, Discord do evento — o que existir).

1. **Colete as fontes**: edital/regras oficiais, página de julgamento, tracks e prêmios, cronograma do evento, canal de anúncios. Faltou fonte? Pergunte ao time — 5–7 perguntas objetivas no máximo, depois marque o que ficou desconhecido como "verificar" (não invente).
2. **Extraia o perfil** — copie `templates/CONTEXTO.md` pra raiz e preencha:
   - **Formato**: presencial/online, solo/time, julgamento expo/pitch stage/vídeo de submissão, jurado testa o app ou não.
   - **Relógio real**: duração, checkpoints, horário EXATO de submissão, quando é o julgamento.
   - **Rubrica oficial transcrita** — os critérios e pesos na literalidade do edital (é o mapa do pitch).
   - **Requisitos-gate**: tech/API do patrocinador obrigatória, tema, repo público, formato e limite de vídeo, elegibilidade. O que mata a submissão automaticamente.
   - **Tracks de patrocinador**: o que cada um quer ver — prêmio extra fora do geral.
   - **Restrições**: codebase existente ou greenfield, IA permitida, licenças, hardware.
3. **Derive as implicações** — a seção mais importante do CONTEXTO.md: "o que isso muda na metodologia". Exemplos:
   - Julgamento por **vídeo** → Demo keeper prioriza gravação boa CEDO (processamento demora), golden path roteirizado pra câmera.
   - **Expo** (jurado passa na mesa) → demo interativo no celular dele + pitch de elevador; menos deck, mais "funciona na mão dele".
   - **Pitch stage** → narrativa de 6 elos completa + Q&A afiado.
   - **Sponsor tech obrigatória** → vira critério de aceite do cartão de contrato, não detalhe de última hora.
   - **8h** → pipeline comprimido (ver cronograma); **48h** → mais profundidade de pesquisa + UX.
   - **Jurado não testa o app** → vídeo e descrição carregam tudo; **jurado testa** → onboarding e credenciais de demo viram P0.
4. **Registre** a leitura em `DECISOES.md` (decisão nº 0: o perfil do hacka e as implicações) e calcule o cronograma real a partir da duração (ver seção Cronograma).

Sem `CONTEXTO.md` preenchido, os outros modos operam no escuro — exija que ele exista.

---

### `/hackathon aula` — mini-curso (humanos novos e agentes)

Ensine em linguagem direta, nesta ordem, usando o Modelo mental como roteiro:

1. **Git em 5 linhas**: repo (pasta com história), commit (foto), branch (linha do tempo paralela), merge (juntar de volta), conflito (mesma linha, dois autores).
2. **Worktree**: várias pastas, uma história. O que isola (arquivo) e o que não isola (porta, DB, `.env`, deps, container).
3. **O pipeline**: pesquisa → debate → proposta → red team → spec → dividir → task → merge → audit → pitch.
4. **Os papéis** e por que existem (acima).
5. **As 7 leis**, uma por uma, com o desastre que cada uma evita.

Feche com quiz de 5 perguntas ("dois cartões precisam do mesmo arquivo — e agora?", "o que entra primeiro no merge?"). Quem errar, revise o ponto antes de liberar pra tarefa.

---

### `/hackathon setup` — kickoff

Pré-requisito: `CONTEXTO.md` preenchido (`/hackathon contexto`).

1. **Papéis** com o time (ver Modelo mental → Papéis). Nomeie o Demo keeper desde já — e defina O QUE ele protege a partir do formato em CONTEXTO.md (vídeo? expo? pitch stage?).
2. **Copie `templates/AGENTS.md`** pra raiz do repo e preencha com o time: stack (incluindo sponsor tech obrigatória do edital), comandos de build/test/lint/dev, convenção de branch (`feature/tNNN-slug`), de worktree (`../<repo>-tNNN`), de porta (3000+nº do cartão). Todo agente lê isso primeiro — é o contrato de verificação.
3. **Copie `templates/BOARD.md`** e **`templates/DECISOES.md`**; registre decisão nº 1 (tema, papéis, stack, porquês).
4. **Git baseline**: repo no GitHub, `main` protegida (sem push direto; PR + CI verde obrigatórios), `.gitignore` cobrindo `.env*`, CI mínimo rodando lint+test, e primeiro commit = estrutura + hello world com `build` e `test` verdes. **Antes de qualquer feature, o contrato de verificação existe.**
5. Rode `/hackathon pesquisa`.

---

### `/hackathon pesquisa` — antes de codar

Cada etapa gera artefato no repo:

1. **Multi-perspectiva** — mesmo problema em ângulos paralelos: técnico (o que já existe), usuário (quem sofre e como), negócio (alguém pagaria/usaria), concorrência (quem tentou e por que não pegou). Um agente por ângulo se houver.
2. **Debate** — os achados se confrontam: um defende, outro questiona, um terceiro aponta contradição. Debate estruturado erra menos que primeira impressão.
3. **Proposta** — UMA proposta escrita em `DECISOES.md`: problema quantificado, insight não-óbvio, porquê-agora, mecanismo da solução, premissas explícitas.
4. **Red team** — leia `playbooks/redteam.md` e rode o gate completo. A proposta só vira spec se sobreviver às 4 perguntas com resposta concreta. Premissa central que cai → volta pra pesquisa (tempo gasto não é argumento — sunk cost não decide).

---

### `/hackathon spec` — proposta → spec

Por feature aprovada, copie `templates/spec.md`, `templates/plan.md`, `templates/tasks.md` pra `specs/<slug>/` e preencha:

- **spec.md**: problema (1 frase com dono e custo), golden path passo a passo, critérios de aceite objetivos (cada um vira um teste), fora de escopo explícito, premissas.
- **plan.md**: arquitetura, arquivos/módulos que toca, interface/contrato que publica pros outros, riscos e fallback.
- **tasks.md**: rascunho da quebra em cartões com dependências (o modo `dividir` refinam e joga no board).

Regra: spec sem critério testável volta pra revisão — não vai pro board.

---

### `/hackathon dividir` — a parte mais importante

Leia **`playbooks/decomposicao.md`** e execute como checklist:

1. Roteiro do demo escrito (60–90s) → só entra no board o que aparece nele ou sustenta o que aparece.
2. Contrato/interface como primeiro(s) cartão(ões): schema, tipos, shape de API. Todos dependem dele.
3. Fatias verticais demonstráveis; mapa de propriedade cartão→arquivos; zero arquivo em dois cartões simultâneos.
4. Grafo de dependência → ordem de merge preenchida no board.
5. Cartões de 30–90min com critério testável e dono pré-atribuído por camada.
6. **Workstream de submissão entra no board também** — leia `playbooks/submissao.md`: roteiro do pitch, vídeo de demo, texto de submissão, backup, Q&A, ensaios e upload são CARTÕES com dono e dependência, paralelos ao build. Pitch às 23h é o sintoma de quem não decompôs a entrega.

Entregável: `BOARD.md` populado (produto + submissão) + grafo em `DECISOES.md`. Nenhum agente trabalha em cartão que não está no board.

---

### `/hackathon task` — executor (modo default do agente de código)

1. Leia `AGENTS.md`, `BOARD.md`, a spec do cartão. Reivindique o cartão (dono + status `fazendo`) ANTES de tudo. Cartão já tem dono? Pegue outro ou pergunte.
2. Worktree a partir da main atual:
   ```bash
   git fetch origin
   git worktree add ../<repo>-tNNN -b feature/tNNN-slug origin/main
   cd ../<repo>-tNNN
   ```
3. Ambiente da worktree: copie `.env*` pra dentro, instale deps, **mude a porta** (3000+nº do cartão), banco/schema separado se houver.
4. Implemente contra a spec: escreva o(s) teste(s) do critério de aceite, faça passar, rode o comando de teste do AGENTS.md completo.
5. Commits pequenos, conventional (`feat:`, `fix:`, `test:`...). Push + PR usando `pull_request_template.md`, linkando o cartão (`Closes T014`).
6. Pré-merge: `git fetch origin && git rebase origin/main`, conflito resolvido na SUA worktree, teste verde de novo, cartão → `pronto`, avise o Integrador.
7. Pós-merge: `git worktree remove ../<repo>-tNNN && git branch -d feature/tNNN-slug`.

**Nunca**: mexa fora do seu mapa de arquivos (precisa? protocolo de overlap — avise o dono), force-push, commite secret, dê merge na main, nem "ajuste" arquivo de outro cartão calado.

---

### `/hackathon merge` — integrador (rotativo)

Leia o gate AUDIT-MERGE em `playbooks/audit.md`. Resumo:

1. Cartões `pronto` ordenados por dependência (grafo do board). Quem depende de menos entra primeiro.
2. Por branch: CI verde + review → `git checkout main && git pull && git merge --no-ff feature/tNNN-slug`. Conflito → resolve ou chama o dono; nunca escolhe versão no chute.
3. **Teste inteiro na main após CADA merge.** Quebrou → `git revert -m 1 HEAD`, reabre o cartão, avisa. Main nunca fica vermelha "só um tempinho".
4. Board atualizado, worktree removida, próxima branch.
5. Fim do ciclo: `git push`, sync de 5min (o que entrou / o que travou / o que cortou), passa o bastão de Integrador.

---

### `/hackathon audit` — gates com evidência

Leia **`playbooks/audit.md`** — contém o AUDIT-MERGE (por merge) e o AUDIT-DEMO (antes do pitch e quando mandarem). Regras do auditor: "não sei" = "não feito"; evidência, não "sim"; honestidade acima de agrado; severidade P0 (mata o demo) / P1 (sangra na banca) / P2 (feio).

---

### `/hackathon pitch` — narrativa + demo + entrega

Leia **`playbooks/pitch.md`**: cadeia narrativa de 6 elos, mapa critério→evidência, roteiro de demo com plano B, três durações, banco de Q&A, modo sabatina (jurado cético).

E **`playbooks/submissao.md`**: o workstream de entrega decomposto — roteiro por critério, vídeo de demo (uma seção por critério, clipe só de main verde, B-roll incremental), backup local, texto de submissão, deck se o formato pedir, ensaio na máquina de apresentação, upload com folga. Se o board já tem os cartões P001–P008 do `dividir`, aqui é só executar e verificar.

---

### `/hackathon status` — radiografia

Em 10 linhas: cartões por coluna; quem está em quê e há quanto tempo (travado = >45min sem commit?); estado da main (verde? último merge?); `git worktree list` vs. esperado; os 3 próximos movimentos em ordem de dependência; o que o Demo keeper reporta do golden path.

## Cronograma — proporcional à duração real

Não existe "o cronograma de hackathon" — existe o do SEU. Calcule a partir da duração em `CONTEXTO.md`:

| Fase | % do relógio | O que acontece |
|---|---|---|
| Contexto + aula + setup | ~5% | `contexto` (edital → CONTEXTO.md), aula relâmpago, baseline verde |
| Pesquisa + debate | ~12% | multi-perspectiva e confronto |
| Proposta + red team | ~8% | proposta escrita; sobreviveu ou volta |
| Spec + dividir | ~8% | specs, board populado, grafo de merge |
| **Build** | **~50%** | worktrees, merge em ordem a cada 1–2h, sync de 5min — **em paralelo**: workstream de submissão (roteiro, B-roll das features que mergem, Q&A) |
| Integração + AUDIT-DEMO | ~8% | merge final, auditoria, limpeza |
| Pitch + sabatina + submissão | ~9% | montagem do vídeo com clipes já gravados, ensaio, upload COM FOLGA (processamento demora) |

Referência rápida — **24h**: contexto/setup ~1h, pesquisa ~3h, proposta+redteam ~2h, spec+dividir ~2h, build ~12h (8–20h), audit ~2h, pitch+submissão ~2h.

Adaptações por duração:
- **≤8h**: comprima pesquisa em 30–45min com 1–2 perspectivas só, red team em 20min só das premissas centrais, spec mínimo (1 spec pro golden path). As leis NÃO relaxam — o que cai é a profundidade, nunca o gate.
- **≥36h**: pesquisa ganha profundidade (mais perspectivas, validação com usuário real se houver), UX/design-spec ganham tempo, segunda rodada de sabatina.
- **Deadline de submissão > deadline de build**: se o vídeo vence antes do julgamento ao vivo, trate a submissão como o deadline real — o pitch stage usa o que sobrou de tempo depois.

Régua: ~25% do relógio em pesquisa/crítica/spec antes da primeira linha de produto. É muito mais rigor que a maioria (que é zero) sem sacrificar as horas de build que um demo real exige. Em hacka curto, até a régua cai — o que não cai é spec-antes-de-código nem teste-antes-de-merge.

## Troubleshooting — os 6 jeitos que isso descarrilha

| Sintoma | Causa provável | Correção |
|---|---|---|
| Dois agentes editaram o mesmo arquivo | Fronteira mal desenhada | Fundir cartões ou sequenciar; extrair comum pro contrato |
| Agente "travado" sem commit >45min | `.env` faltando, porta ocupada, dep não instalada | Checklist de ambiente da worktree (modo task, passo 3) |
| Merge virou inferno | Ordem de chegada, não de dependência | Grafo no board; rebase antes de pedir merge |
| "Quase pronto" eterno | Cartão grande demais / critério vago | Cortar até caber num teste |
| Demo quebrou na banca | Sem seed, sem plano B, main "estava verde ontem" | AUDIT-DEMO + golden path ensaiado por terceiro |
| Todo mundo esperando um cartão | Contrato não mergiou primeiro | Prioridade máxima de merge pro contrato |

## Fuleiragens — o que NÃO fazer

- Dois agentes no mesmo checkout "só rapidinho" — é assim que nasce o conflito das 23h.
- Cartão gigante ("fazer o cadastro") — overlap invisível e "quase pronto" eterno.
- Merge por ordem de chegada.
- "Tá pronto" sem teste — a banca pergunta justo o que não foi testado.
- Feature brilhante que não entra no roteiro do demo — se não aparece, não constrói.
- Worktree sem `.env`/porta própria — "travado" na verdade é porta ocupada do colega.
- Secret commitado (mesmo apagado depois — rotacione, não apague o commit).
- `localhost` hardcoded no build de demo; CORS `*` em produção; `.env` servido pela web.
- Decisão sem fonte — "a IA falou que o mercado é X" não é dado.
- Commit direto na main "só um fix" — é assim que a main morre 40min antes do demo.
- Ninguém dono do seed de dados — o demo mais bonito morre com banco vazio.
