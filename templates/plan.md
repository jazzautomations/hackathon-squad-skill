# Plan: [nome da feature]

> O como — arquitetura, arquivos que toca, contrato que publica, riscos. Escrito depois do spec.md, antes dos cartões.

## Abordagem (2–4 linhas)

[a decisão técnica central e o porquê — é isso que vira a resposta pro "mostra a parte difícil" da banca]

## Arquivos/módulos que toca

[o mapa de propriedade — usado no board pra garantir zero overlap]

- `caminho/arquivo` — o que faz/muda
- ...

## Interface/contrato que publica

[o que outros cartões vão consumir: tipos, endpoints, eventos, componentes — com o shape exato]

```ts
// ex.: POST /api/dose-events { idoso_id, tipo, ts } → { status }
//      type Alerta = { id, tipo, status, criado_em }
```

## Consome (dependências do contrato)

[o que esta feature espera que já exista — define os "depende de" do board]

## Riscos e fallback

| Risco | Probabilidade | Fallback |
|---|---|---|
| [ex.: API externa lenta/fora] | [alta/média/baixa] | [ex.: mock do contrato, vídeo de backup] |

## O que faz se der errado no demo

[1 linha: o plano B desta feature especificamente]
