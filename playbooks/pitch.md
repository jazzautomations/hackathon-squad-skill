# Playbook — Pitch & demo (como a banca realmente decide)

O pitch não se improvisa: cada critério de julgamento já tem evidência gerada pelo pipeline. E a banca não avalia só o produto — avalia o processo: velocidade de resposta, coerência entre versões, como você reage a pergunta dura. **O pitch é a amostra grátis de como é trabalhar com vocês.**

## Como a banca realmente julga (a verdade operacional)

1. **Gate de requisitos ANTES de pontuar.** A primeira coisa que jurado experiente faz é conferir se a submissão cumpre o que o edital pede: ferramenta/API obrigatória visível, link funcionando, repo público, vídeo dentro do limite, tema respeitado. **Projeto forte morre aqui por detalhe burro** — link quebrado, repo privado, sponsor tech que ninguém usou. Os requisitos-gate DESTE hacka estão transcritos em `CONTEXTO.md` — é checklist de submissão, não sugestão.
2. **Poucos minutos por projeto.** Em julgamento estilo expo o jurado gasta ~4 minutos. A prova precisa ser visível rápido — ninguém caça qualidade escondida. Confira o formato exato em `CONTEXTO.md` (expo? stage? vídeo?).
3. **Uma seção por critério.** A rubrica oficial DESTE hacka está transcrita em `CONTEXTO.md` — escreva o roteiro **marcando cada trecho com o critério que ele responde**. Critério sem trecho é ponto deixado ao acaso.
4. **Jurado não é obrigado a testar seu app.** Se o `CONTEXTO.md` diz que ele não testa, vídeo e descrição carregam tudo; se testa, credenciais e onboarding viram P0.
5. **Tracks de patrocinador são prêmios extras.** Dá pra perder o geral e ganhar track — as tracks mira estão no `CONTEXTO.md`; a evidência delas entra na submissão.

## Mapa critério → evidência (o pipeline já gerou tudo)

| Critério da banca | Evidência que você já tem | Onde aparece no pitch |
|---|---|---|
| Inovação / qualidade da ideia | O ângulo que pesquisa+debate achou (e os concorrentes não) | O "insight" da cadeia narrativa |
| Implementação técnica | Demo rodando + a decisão técnica difícil nomeada | Demo + "como funciona" |
| Execução / completude | Golden path ponta a ponta, main verde, testes | O demo fluindo sem tropeço |
| Usabilidade / design | Spec de UX em `design/`, fluxo simples | O demo na perspectiva do usuário |
| Impacto real | Premissas que sobreviveram ao red team, com fonte | Problema quantificado + fechamento |
| Pitch / apresentação | Narrativa ensaiada + Q&A pronto | A performance inteira |
| Scope discipline (implícito) | "O que cortamos e por quê" — jurado pontua JULGAMENTO | Slide/fala do corte |

## A cadeia narrativa de 6 elos

Toda pitch boa é esta cadeia contada com prova. Elo fraco = cadeia fraca:

1. **Problema com dono e custo** — quem sofre, com que frequência, quanto custa. "Pessoas perdem tempo com X" é fraco; "clínicas perdem R$4 mil/mês em no-show" é forte. Faça a banca SENTIR o problema — se eles não sentem, nada do que você construiu aterrissa.
2. **Insight não-óbvio** — o que você sabe que a maioria não sabe? É a resposta implícita a "por que ninguém fez isso ainda?". Sem insight, sua tese é "vamos executar melhor" — a mais fraca que existe.
3. **Why now** — o que mudou (tech, regulação, custo de IA, comportamento) que torna isso possível AGORA e não há 5 anos.
4. **Solução como mecanismo, não feature-list** — em uma frase: o que o produto faz que elimina o custo do problema.
5. **Por que vocês** — a conexão entre o time e ESTE problema.
6. **Onde isso chega** — a ponte do demo de hoje pro produto grande.

**Teste da narrativa**: conte em 60s pra alguém de fora. Se não recontam problema e mecanismo com as palavras deles, simplifique.

## O roteiro do demo (demo-led, demo = metade do tempo)

Estrutura para 3 minutos (adapte as proporções, mantenha demo ≈ 50%):

| Tempo | Seção | Regra |
|---|---|---|
| 0:00–0:30 | Problema + solução em 1 linha | Abra com o usuário e a dor, NÃO com o nome do time nem a stack |
| 0:30–2:00 | **Demo ao vivo** | O golden path, na perspectiva do usuário. Pule login/cadastro mundano — copie texto no clipboard antes. Mostre o "oh, isso é possível agora" — o contraste antes/depois. |
| 2:00–2:30 | Como funciona | 1 diagrama ou 1 fala: **nomeie a decisão técnica mais difícil em voz alta** enquanto a tela roda — jurado técnico pontua isso. |
| 2:30–3:00 | O que cortamos + o que vem depois | "Cortamos X, Y porque Z" — scope discipline é evidência de julgamento. Feche com próximo passo concreto, não com "obrigado". |

**Versões ensaiadas**: 30s (elevador), o tempo oficial, e a conversa longa. O erro padrão é só ter a versão longa.

**Regras do demo ao vivo:**
- Defina o **happy path exato** — sequência de cliques testada que não quebra — e proteja-o. As partes que a banca vê funcionam limpo; as que não vê podem ser duct tape.
- **Backup gravado** (vídeo curto do mesmo fluxo) + screenshots — Wi-Fi morre na hora errada; time que cai pro vídeo parece preparado, time que congela no spinner não.
- Ensaie **na máquina que apresenta**, 3x o click path, com o dado de seed carregado.
- Seja honesto sobre o que é gerado por IA — jurado pergunta, e "tudo nosso" desmascarado queima tudo.

## Banco de Q&A — as que sempre caem

Escreva as respostas por extenso, ensaie em voz alta:

- **"Qual premissa, se falhar, quebra o plano?"** — a pergunta que separa quem construiu de quem montou. Você sabe: passou no red team.
- **"E se [incumbente/big tech] fizer isso?"** — resposta boa: foco, distribuição, velocidade, custo de oportunidade do gigante. Resposta ruim: "eles são lentos".
- **"É produto ou wrapper de API?"** — o que é seu vs. o que o modelo faz; onde mora a defensabilidade.
- **"Quanto custa de IA por usuário?"** — número estimado com a conta, nem que seja de ordem de grandeza.
- **"O que falta pra produção?"** — liste honesto com prioridade (o AUDIT-DEMO já te deu essa lista).
- **"Escala onde quebra primeiro?"** — resposta com o gargalo nomeado mostra que você pensou o sistema, não só a feature.
- **"Mostra o código / a parte difícil."** — tenha o trecho pronto pra abrir.
- **"Por que vocês e não outro time?"** — founder-market fit: a conexão específica do time com o problema.
- **"Qual foi o maior erro do hackathon?"** — honestidade específica ganha; "somos perfeccionistas" perde.

**"Não sei" honesto + "te respondo já"** vale mais que enrolação — e cumprir o follow-up rápido é dos sinais mais fortes que você emite.

## Os erros que matam pitch de hackathon

1. Abrir com o time/stack em vez do problema — a banca não sente a dor, nada aterrissa.
2. Feature tour em vez do momento "oh, isso é possível" — cinco coisas pela metade < uma coisa inteira.
3. Demo que não cumpre o requisito do edital (sponsor tech invisível, tema tangencial).
4. Número diferente entre deck, demo e conversa — contamina a confiança em tudo.
5. Número sem fonte — "o mercado é X" sem origem é número contra você.
6. Não saber o que foi cortado nem por quê — sinal de que construíram no impulso.
7. Escopo ambicioso demais: nada funciona ponta a ponta. Se o demo tá longo, o problema é escopo, não pacing — corte.
8. Demo ao vivo sem backup — o spinner congelado é a imagem que o jurado lembra.
9. Fingir que a parte fraca não existe — descoberta custa mais que admissão com plano.
10. Terminar em "obrigado" — os últimos 10s são seus: feche com o próximo passo.

## Modo sabatina (rodar antes de "finalizar")

Simule 20–30 minutos de jurado cético (agente ou pessoa que não construiu): as perguntas do banco de Q&A + as específicas do caso, uma por vez. Avalie cada resposta; reescreva as fracas junto com o time. É mais barato apanhar aqui do que na banca. Rode no mínimo: uma vez depois do roteiro pronto, uma vez na reta final.

## Checklist de submissão (rode junto com AUDIT-DEMO, Área 0)

- [ ] Requisitos-gate do `CONTEXTO.md` relidos e conferidos: elegibilidade, tech obrigatória visível, links públicos, limites de vídeo/formato
- [ ] Vídeo de submissão: primeira frame = nome + 1 frase; uma seção por critério da rubrica oficial; dentro do limite com folga (processamento pode demorar horas — suba cedo)
- [ ] Descrição escrita: problema, o que faz, stack e POR QUÊ da decisão difícil, o que vem depois
- [ ] Link do demo testado em aba anônima + celular + outra rede
- [ ] Repo público, README que roda, licença se o edital pedir
- [ ] Credenciais de demo no texto de submissão, testadas
