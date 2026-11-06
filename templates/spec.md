# Spec: [nome da feature]

> O quê e por quê — SEM stack (stack vai no plan.md). Cada critério de aceite vira um teste; se não dá pra testar, não está especificado.

## Problema

[1 frase: quem sofre, com que frequência, quanto custa. Com dono e com custo — "clínicas perdem R$4 mil/mês" não "pessoas perdem tempo".]

## Usuário e golden path

[Quem usa e o fluxo principal passo a passo, incluindo o que aparece na tela em cada passo. É o fluxo que vai pro demo.]

1. Usuário abre [tela X] e vê [estado inicial]
2. Usuário faz [ação] → sistema [comportamento] → vê [resultado]
3. ...

## Critérios de aceite

[objetivos e testáveis — cada um vira um teste]

- [ ] [comportamento observável, ex.: "CPF válido passa, inválido rejeita com mensagem específica no campo"]
- [ ] [estado de erro, ex.: "falha da API mostra erro com ação de retry, nunca tela branca"]
- [ ] [empty state, ex.: "sem registros → estado vazio com exemplo e CTA"]

## Fora de escopo (explícito)

[o que NÃO vamos fazer — protege contra scope creep no meio do build]

- [ex.: edição de perfil, esqueci-senha, dark mode]

## Premissas que precisam ser verdade

[da pesquisa/red team — com fonte]

- [premissa + fonte do dado que a sustenta]

## Ligações

- Depende de: [outras specs/contrato]
- Publica para os outros: [interface/contrato que esta feature expõe]
- UX: `design/[arquivo].md` se houver
