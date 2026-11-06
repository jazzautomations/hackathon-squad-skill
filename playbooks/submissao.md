# Playbook — Submissão como workstream (pitch, vídeo, texto = produto também)

O erro clássico: o time constrói 20 horas e começa o pitch às 23h. A entrega — roteiro, vídeo de demo, texto de submissão, Q&A — é um **workstream paralelo ao build**, com cartões no board, donos, dependências e critérios testáveis como qualquer feature. Um demo de 3min bom é um produto de ~4h distribuídas, não um improviso de 40min.

## Quando entra no board

No `dividir`, depois dos cartões de produto: os cartões de submissão entram com as dependências certas — o roteiro depende da proposta (red team), os clipes do vídeo dependem das features mergeando, a montagem final depende da main estável. **Assim o pitch amadurece junto com o produto em vez de nascer morto na madrugada.**

## Os cartões de submissão (copie pro board, ajuste ao CONTEXTO.md)

### [P001] Roteiro do pitch — narrativa de 6 elos + script
- **Depende de**: proposta aprovada no red team
- **Dono**: liaison ou quem apresenta
- **Pronto quando**: cadeia de 6 elos escrita (problema com dono/custo → insight → why now → mecanismo → por que vocês → onde chega); roteiro com cada trecho MARCADO com o critério da rubrica oficial (CONTEXTO.md) que ele responde; versões 30s/tempo-oficial/longa; lido em voz alta cabendo no tempo
- **Por quê**: critério da rubrica sem trecho = ponto ao acaso. O roteiro é o spec do pitch.

### [P002] Vídeo de submissão — gravado, editado, dentro do limite
- **Depende de**: P001 + features do golden path mergeadas (mas começa a captar ANTES — ver B-roll abaixo)
- **Dono**: 1 pessoa de captura/edição (pode ser agente se houver tooling de vídeo)
- **Pronto quando**: uma seção por critério da rubrica; primeira frame = nome + 1 frase; demo ao vivo ≈ metade do tempo; dentro do limite com ≥20s de folga; áudio legível; legendas se couber; assistido do zero por alguém de fora que reproduz o que o produto faz
- **Estrutura pra ~3min (mire 2:40, os 20s são margem)**:

| Trecho | Tempo | Critério que serve | Na tela |
|---|---|---|---|
| Problema com dono | 0:00–0:20 | impacto | nome + 1 frase, depois quem sofre |
| Solução + o que é novo | 0:20–0:35 | ideia | a frase-mecanismo |
| **DEMO** | 0:35–2:00 | implementação + design | o golden path, zoom legível, sem cadastro mundano |
| Como funciona | 2:00–2:20 | técnica | 1 diagrama; nomeie a decisão difícil |
| O que cortamos + o que vem depois | 2:20–2:40 | julgamento + viabilidade | corte com motivo, próximo passo |

### [P003] Vídeo de backup (o mesmo fluxo, "contingência")
- **Depende de**: golden path estável na main
- **Pronto quando**: gravação curta do golden path funcionando, salva LOCAL na máquina de apresentação + segundo lugar (pendrive/nuvem), testada abrindo o arquivo
- **Por quê**: Wi-Fi morre na hora errada. Time que cai pro vídeo parece preparado; time que congela no spinner, não.

### [P004] Texto de submissão + README de jurado
- **Depende de**: P001 (reusa a narrativa)
- **Pronto quando**: descrição com problema → o que faz → stack e o porquê da decisão difícil → o que vem depois; README roda o projeto pra quem nunca viu; credenciais de demo incluídas e testadas; OG image/favicon ok

### [P005] Deck / one-pager (só se o formato pedir)
- **Pronto quando**: 7 slides máx — problema nas palavras do usuário, usuário e custo, demo (troca pro app), como funciona (1 diagrama), o que cortamos e por quê, o que vem depois, time. Sem logo wall, sem market size de faz-de-conta.

### [P006] Banco de Q&A respondido + sabatina
- **Depende de**: P001
- **Pronto quando**: as perguntas do banco de Q&A (playbooks/pitch.md) respondidas por extenso + sabatina rodada com jurado cético e respostas fracas reescritas

### [P007] Ensaios na máquina de apresentação
- **Depende de**: tudo acima
- **Pronto quando**: click path do demo rodado 3x na máquina que vai apresentar, com seed carregado; tempo cronometrado cabendo com folga; quem fala o quê decidido se for time

### [P008] Upload/submissão com folga
- **Depende de**: P002–P005
- **Pronto quando**: submetido com horas de antecedência (processamento de vídeo pode demorar); verificado DEPOIS do upload (abrindo como jurado: aba anônima, outra rede); print/registro da confirmação

## B-roll incremental — o truque de paralelização

Quando uma feature do demo merge na main, o dono do vídeo **grava o clipe dela na hora** (10–20s, mesma resolução/zoom final). Na hora da montagem, o vídeo é costura de clipes verificados + narração, não uma sessão desesperada de captura em produto instável. Regra: clipe só se grava de main verde — feature de branch não aparece no vídeo (se quebrar no merge, o clipe mente).

## Gravação — checklist operacional

- [ ] Resolução e zoom fixos (texto legível em tela pequena — jurado assiste no notebook/celular)
- [ ] Seed de dados bonito carregado; conta de demo logada; clipboard com os textos a digitar
- [ ] Notificações off, abas limpas, cursor visível; sem dados reais/pessoais na tela
- [ ] Narração lendo o roteiro (P001), não improvisando — uma seção por critério
- [ ] Take único do golden path > edição pesada; corte só entre seções
- [ ] Exporta e ASSISTE o arquivo final inteiro — vídeo corrompido descoberto no upload é clássico

**Ferramenta**: tanto faz — OBS, gravador nativo, ou skill de vídeo por código (`video-forge`, se disponível no agente) pra zoom/legenda/redaction automático. A metodologia não depende da ferramenta; depende de roteiro por critério, clipe de main verde e margem de tempo.

## Quem faz o quê (mapa de papéis)

| Papel | Cartões |
|---|---|
| Quem apresenta | P001 (dono), P006, P007 |
| Editor/captura | P002, P003 — pode ser um agente com tooling de vídeo |
| Liaison | P004, P005 — reusa narrativa do P001 |
| Demo keeper | garante main estável + seed pros clipes; roda P007 junto |

Em time pequeno, uma pessoa acumula — mas os cartões continuam separados porque as DEPENDÊNCIAS são separadas: roteiro não espera vídeo, vídeo não espera deck, backup não espera nada além de main verde.
