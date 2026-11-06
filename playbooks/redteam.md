# Playbook — Red team / crítica adversarial

A etapa que separa "produto que resolve problema real" de "produto bonito e vazio" — e a que mais gera material pro pitch, porque **toda pergunta que o jurado faria, você já se fez antes**.

## Quem faz

Uma pessoa OU um agente configurado pra isso — mas **nunca quem teve a ideia**. Quem criou a proposta tem viés de defendê-la; o papel de atacar precisa vir de fora.

Se for um agente, o prompt dele é essencialmente: *"Sua única função é atacar esta proposta. Você não ajuda a construir, você tenta derrubar — com motivo concreto, não retórica. Se a proposta sobreviver, ela é forte de verdade."*

## As 4 perguntas (o gate completo)

### 1. Checagem de premissas

Liste TODA premissa que precisa ser verdadeira pra ideia funcionar. Depois separe cada uma em três baldes:

- **Desejável**: alguém realmente quer isso? (não "eu acho que sim" — quer de verdade)
- **Viável**: isso sustenta produto/negócio depois do hackathon?
- **Factível**: dá pra construir a tempo, com ESSA equipe e ESSAS ferramentas?

Exemplo que mata direção: premissa "idosos vão instalar um app novo" — desejável? Provavelmente não. Essa única premissa derrubada na hora 5 economiza 15 horas de build na direção errada.

### 2. Contra-argumento ativo

Pra cada premissa sobrevivente, argumente o lado oposto **com motivo concreto** — não "será que dá certo?", mas "por que isso pode estar errado?". A pergunta certa nunca é "você concorda?", é "qual o cenário onde isso falha?".

### 3. Qualidade da informação

Todo dado que sustenta decisão tem origem rastreável. A pergunta é literal: **"esse número/fato veio de onde?"** — se a resposta é "o agente falou" sem fonte, é alerta vermelho. Agente inventa informação com total confiança (alucinação); dado crítico pra decisão se checa contra fonte real antes de virar base.

### 4. Furo em produção/demo

Onde isso quebra? Com usuário real? Na frente do jurado que pergunta "e se X acontecer?"? Imagine o pior caso — é o exercício que evita ser pego de surpresa no pitch.

## Vereditos possíveis

| Veredito | Significado |
|---|---|
| **PASSA** | Sobreviveu às 4 perguntas com resposta concreta → vira spec |
| **VOLTA COM X** | Premissa não-central fraca → ajusta a proposta e re-roda só o ponto |
| **MORRE** | Premissa central caiu → volta pra pesquisa/debate. Tempo gasto não é argumento — sunk cost não decide. |

## Formato de saída

```markdown
## Red team — <proposta>
### Premissas
| Premissa | Desejável | Viável | Factível | Veredito |
### Contra-argumentos fortes
### Dados sem fonte (expulsos ou verificados)
### Cenários de quebra em demo
### VEREDITO: PASSA / VOLTA COM X / MORRE
### O que muda na proposta
```

Registre em `DECISOES.md` — o registro do red team é evidência de impacto pro critério "impacto real" da banca.

## Rodada extra: sabatina de jurado

Antes do pitch, o red team vira **jurado cético simulado** (ver `playbooks/pitch.md`, modo sabatina): 15–30 min de perguntas difíceis, uma por vez, avaliando cada resposta e reescrevendo as fracas junto com o time. É mais barato apanhar aqui do que na banca.
