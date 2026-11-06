# Playbook — Audit (gates com evidência, não com "confia")

Você é um auditor cético. Sua missão não é recitar checklist: é produzir o diagnóstico que impede o time de ser pego de surpresa — no merge e na banca.

## Regras do auditor (invioláveis)

1. **"Não sei" = "não feito".** Incerteza conta contra. Registre como pendente e siga.
2. **Evidência, não "sim".** Item crítico se prova com fato: "o teste rodou quando?" vale mais que "tá passando". Sem evidência → status 🟡 parcial.
3. **Honestidade acima de agrado.** Produto exposto se diz com clareza e sem drama. Coisa bem-feita se reconhece — não invente problema pra parecer útil.
4. **Severidade vem da matriz**, não de adjetivo:

| Nível | Significado | Prazo |
|---|---|---|
| **P0 — mata o demo** | main quebrada, golden path não roda, secret commitado, submissão falhando | Agora. Tudo para. |
| **P1 — sangra na banca** | golden path instável, feature do pitch inexistente, README que não roda, dependência externa sem plano B | Antes do ensaio do pitch |
| **P2 — feio** | UI quebrada em fluxo secundário, código morto, porta colidindo | Se sobrar tempo |
| **P3 — pós-hackathon** | divida técnica consciente | Registra como risco aceito e segue |

5. **Risco aceito por escrito é gestão; risco ignorado é surpresa agendada.** Tudo que ficar de fora por decisão vai pra lista: "aceitamos o risco de ___ até ___ porque ___".

---

## AUDIT-MERGE — gate por merge (rode rápido, sempre)

Antes de cada merge na main, o Integrador confere — nesta ordem, parando no primeiro não:

- [ ] O cartão está `pronto` no board e a spec linkada bate com o diff (não tem escopo sorrateiro no meio)
- [ ] CI verde NA BRANCH (lint + typecheck + testes)
- [ ] Review por alguém que não é o autor — nem que seja review de 5min do diff
- [ ] Teste do critério de aceite existe e passa
- [ ] Sem secret, `.env`, chave ou credencial no diff (rode scanner se houver: gitleaks, truffleHog — ou pelo menos `git diff | grep -iE "key|secret|token|password"`)
- [ ] Sem `console.log`/debug esquecido, sem porta/porta-hardcode diferente do padrão, sem `localhost`/`127.0.0.1` hardcoded onde a demo vai rodar
- [ ] Diff de tamanho revisável — PR gigante demais volta pro dono cortar

Depois do merge: **teste inteiro na main**. Quebrou → `git revert -m 1 HEAD` imediato, reabre o cartão. Main vermelha nunca é "daqui a pouco resolve" — é agora ou reverte.

---

## AUDIT-DEMO — a auditoria grande (hora 20–22 e antes do pitch)

Audite por área, uma por vez, pedindo o FATO que comprova cada item. Placar parcial a cada área: ✅ / 🟡 / ❌.

### Área 0 — O gate do edital (vem ANTES de tudo, via `CONTEXTO.md`)

Abra o `CONTEXTO.md` e confira cada requisito-gate e cada `[VERIFICAR]`:

- [ ] **TODOS os requisitos-gate do edital cumpridos** — sponsor tech visível no produto E na submissão, tema respeitado, repo no formato exigido, elegibilidade ok. Falhou aqui = desclassificado antes de pontuar; é P0 absoluto.
- [ ] **Submissão testável no formato do julgamento** — link público abre em aba anônima? vídeo dentro do limite? credenciais de demo no texto se o jurado testa?
- [ ] **`[VERIFICAR]` resolvidos** — toda pendência do contexto tem resposta confirmada com fonte.
- [ ] **Rubrica coberta** — cada critério oficial tem trecho no pitch/submissão (critério sem trecho = ponto ao acaso).
- [ ] **Tracks mira** — se o CONTEXTO mapeou track de patrocinador, a evidência dela existe na submissão.

### Área 1 — O esqueleto (P0 direto se falhar)

- [ ] `build` + `test` verdes na main **agora** — evidência: quando rodou pela última vez? (rodou de novo na sua frente?)
- [ ] Golden path executado ponta a ponta **por alguém que não construiu** — evidência: quem rodou, e onde travou?
- [ ] Deploy/link de submissão **testado de fora** — abre no celular, em outra rede, em aba anônima?
- [ ] `git status` limpo na main; `git worktree list` sem worktree morta acumulando lixo
- [ ] `git log` da main legível — a banca técnica às vezes olha o histórico; commits `asdf`, `fix fix fix` contam contra

### Área 2 — O demo em si

- [ ] **Seed/dados bonitos** — o cenário do demo existe no banco (cartão de seed fechado, com dono)
- [ ] **Plano B ensaiado** — se o Wi-Fi cair ou a API externa morrer: ambiente local funciona? vídeo de backup existe? dado de fallback?
- [ ] **Roteiro ensaiado em tempo real** — coube no tempo oficial com folga?
- [ ] **Empty states e erros** não são telas brancas nem stack trace — erro genérico com código de referência, nunca detalhe interno vazando
- [ ] Loading/feedback em toda ação assíncrona; botão desabilita pra não duplicar ação no nervoso do demo
- [ ] Mobile/responsivo do que vai ser mostrado (a banca pode abrir no próprio celular)

### Área 3 — A camada invisível mínima (o que o jurado cutuca)

Destilado do checklist de produção — em hackathon não é compliance, é **não passar vergonha técnica ao vivo**:

- [ ] **Nenhum secret no repo** — scanner rodou; e lembre: secret commitado está comprometido pra sempre → rotacione, não apague o commit
- [ ] **`.env` não é servido pela web** — teste literal: `seudominio/.env` retorna 404/403?
- [ ] **Validação no servidor, não só no front** — o jurado que abre o devtools e manda request na mão é clássico
- [ ] **Nada de mass assignment** — endpoint que grava o body inteiro aceita `role: "admin"` junto; whitelist de campos
- [ ] **Valor crítico calculado no servidor** — preço, permissão, status nunca confiados ao payload do cliente
- [ ] **Erros sem stack trace** em produção — página 500 com nome de tabela e versão de framework é mapa pro atacante e feio na banca
- [ ] **CORS com origem explícita** — `*` com credencial é falha, não conveniência
- [ ] **Rate limit mínimo** nas rotas caras (a de IA principalmente) — um loop com bug no demo gera fatura ou quota esgotada AO VIVO
- [ ] **Dependências fixadas** — nada de `latest`/range solto quebrando o build no dia
- [ ] **Rollback = `git revert` ensaiado** — se o último deploy quebrar, volta em 1 comando, não em pânico

### Área 4 — Se usa IA no produto (quase todo mundo usa)

- [ ] **Prompt injection pensado** — texto de usuário/documento pode conter instrução maliciosa; o modelo não tem ferramenta cujo abuso você não aceitaria
- [ ] **Saída do modelo sanitizada ao renderizar** — output que vira HTML sem sanitização é XSS ao vivo na banca
- [ ] **Limite de custo/tokens por usuário e por conta**, com degradação graciosa — sem isso, um loop no demo estoura a quota na frente do jurado
- [ ] **Golden path da feature de IA testado com eval mínimo** — as 5–10 entradas do roteiro do demo rodadas e verificadas; "melhorar o prompt" sem eval é aposta
- [ ] **Fallback quando o modelo falha/demora** — timeout, retry, ou resposta elegante; provedor de IA cai sem aviso
- [ ] **Resposta para "quanto custa de IA por usuário"** — número estimado existe, nem que seja de guarda-chuva (pergunta padrão de banca em 2026)

### Área 5 — A embalagem

- [ ] **README que roda o projeto** — escrito pra quem nunca viu: o que é, como sobe, o que demonstrar. É o que o jurado abre.
- [ ] **OG image + favicon** — o link compartilhado no WhatsApp da banca não pode parecer link quebrado
- [ ] **Credenciais de demo funcionando** — login de teste pronto e TESTADO (nada de criar conta ao vivo)
- [ ] **Bus factor lite** — repo/deploy não dependem da conta pessoal de uma pessoa só; segundo admin existe
- [ ] **Analytics/prints de prova** — se o pitch afirma número, o número tem fonte registrada (Lei 7)

## Entregável do AUDIT-DEMO

1. **Placar por área** ✅/🟡/❌
2. **Os P0** em linguagem de dono: "se a internet do jurado for 4G, a tela X trava porque depende de Y"
3. **Plano até o pitch**: cada P0/P1 com primeiro passo concreto (30min), dono e horário-limite
4. **Riscos aceitos** por escrito
5. **Go/no-go honesto**: se o golden path não está P0-livre, a recomendação é cortar feature e proteger o demo — diga isso sem suavizar.

## Os furos clássicos de hackathon (a lista da vergonha)

Adaptado dos furos que todo mundo descobre tarde — versão banca:

1. O demo depende de internet/API externa e ninguém testou o plano B.
2. O banco está vazio porque o seed era "detalhe".
3. `.env` commitado "só por enquanto" — e é hackathon público no GitHub.
4. `localhost:3000` hardcoded no link de submissão.
5. A feature que o pitch promete existe "na branch do João, quase mergeada".
6. O login de demo expirou/ninguém testou desde ontem.
7. O prompt de IA foi "melhorado" às 23h e ninguém re-rodou o golden path.
8. Conta pessoal do deploy + pessoa no banho na hora da banca.
9. A dependência `latest` resolveu uma versão nova na madrugada e quebrou o build.
10. O vídeo de backup existe — corrompido, em 4K, no notebook que ficou em casa.
