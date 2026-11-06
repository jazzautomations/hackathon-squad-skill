# hackathon-squad-skill

Metodologia de squad multi-agente pra hackathon — pra agentes de código (e humanos) não fazerem merda.

O fracasso padrão de hackathon com agentes é conhecido: vários agentes no mesmo checkout, conflito de merge generalizado, ninguém sabendo quem faz o quê, `main` quebrada na hora do demo e pitch improvisado em cima de um produto "quase pronto". Esta skill é o sistema operacional que evita isso — metodologia pura, git vanilla, nenhuma dependência de ferramenta externa.

## Instalação

**Global** (disponível em qualquer projeto):

```bash
git clone https://github.com/jazzautomations/hackathon-squad-skill ~/.config/devin/skills/hackathon
```

**Por projeto** (vai junto do repo — a equipe inteira opera a mesma metodologia):

```bash
git clone https://github.com/jazzautomations/hackathon-squad-skill .devin/skills/hackathon
```

Funciona em qualquer agente que lê `SKILL.md` — não é específico de uma ferramenta.

## Uso

```
/hackathon contexto   # MINUTO 0: lê o edital do SEU hacka → CONTEXTO.md
/hackathon aula       # mini-curso: conceitos + porquês + quiz (humanos novos e agentes)
/hackathon setup      # papéis, AGENTS.md, board, main protegida, baseline verde
/hackathon pesquisa   # multi-perspectiva → debate → proposta → red team
/hackathon spec       # spec/plan/tasks por feature aprovada
/hackathon dividir    # decomposição em cartões sem colisão + grafo de merge
/hackathon task       # executor: cartão → worktree → teste → PR → rebase
/hackathon merge      # integrador: merge em ordem de dependência, main verde
/hackathon audit      # gates com evidência: por merge e pré-demo
/hackathon pitch      # narrativa, demo script, Q&A, sabatina, submissão
/hackathon status     # radiografia do time em 10 linhas
```

## As 7 leis

0. **O edital manda; a metodologia adapta** — `CONTEXTO.md` parametriza tudo: rubrica, requisitos-gate, formato, duração.
1. **Uma tarefa = um dono = uma branch = uma worktree.**
2. **Marque "peguei" no board ANTES de começar.**
3. **A `main` está SEMPRE demo-ready** — CI verde + review, ou não entra.
4. **Spec antes de código** — cartão aponta pra spec com critérios de aceite.
5. **"Pronto" é testável** — critério de aceite vira teste; sem teste, não mergia.
6. **Só o Integrador mergia**, em ordem de dependência, `--no-ff`.
7. **Decisão e dado têm fonte** em `DECISOES.md` — "o agente falou" não é fonte.

## Estrutura

```
SKILL.md                    → o sistema operacional: leis, modelo mental, modos, cronograma
playbooks/
  decomposicao.md           → contrato primeiro, fatias verticais, mapa de arquivos, grafo
  redteam.md                → crítica adversarial: 4 perguntas, vereditos, sabatina
  audit.md                  → AUDIT-MERGE + AUDIT-DEMO com evidência e severidade P0–P3
  pitch.md                  → como a banca julga, cadeia narrativa, Q&A, erros fatais
  submissao.md              → pitch/vídeo/texto como workstream decomposto (cartões P001–P008)
templates/
  CONTEXTO.md               → perfil do hackathon específico (edital → metodologia)
  AGENTS.md                 → lei da casa do repo: stack, comandos, convenções, leis
  BOARD.md                  → quadro de tarefas versionado
  DECISOES.md               → ADR light: decisões com motivo e fonte
  spec.md / plan.md / tasks.md → spec-driven development por feature
  design-spec.md            → UX em markdown: estados, erros, empty states
  pull_request_template.md  → PR com evidência
```

## Filosofia

- **Metodologia-first, ferramenta-agnóstica** — git vanilla, arquivos markdown no repo. Funciona com qualquer agente.
- **Adaptativa** — cada hackathon é uma brisa: o `contexto` lê o edital e parametria cronograma, audit, pitch e o que o Demo keeper protege.
- **Aprendizado embutido** — o modelo mental explica o *porquê* de cada regra; agente que entende decide certo quando a regra não cobre.
- **Evidência, não "confia"** — "não sei" = "não feito"; teste verde é a única prova de pronto.

## Licença

MIT — use, adapte, ganhe hackathons.
