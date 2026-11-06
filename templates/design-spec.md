# Componente/fluxo: [nome]

> Spec de UX em texto — o agente de design escreve, o agente de dev implementa direto, sem ninguém "traduzir" Figma. Estados e erros são obrigatórios: é neles que o demo morre ou parece amador.

## Quando usar / fluxo

[quando esse componente ou fluxo aparece; o passo a passo incluindo decisões de UX]

## Estados (TODOS obrigatórios)

- **Vazio/empty state**: [o que aparece antes de ter dado — com exemplo e CTA, nunca tela branca. É a primeira coisa que usuário novo vê.]
- **Carregando**: [skeleton > spinner > nada. Botão desabilita pra evitar duplo-clique.]
- **Erro**: [mensagem específica embaixo do campo/no contexto — nunca alerta genérico no topo. Diz o que aconteceu e o que fazer.]
- **Sucesso**: [confirmação clara antes de navegar]
- **Hover/focus/disabled**: [foco visível sempre — acessibilidade]

## Validação e formato

- [o que valida em campo, quando valida (ao sair do campo, não a cada tecla), e formato brasileiro quando couber: CPF com dígito verificador, data, moeda em centavos nunca float, horário em UTC no banco]

## Acessibilidade mínima

- Todo campo com `label` associado (nunca só placeholder)
- Contraste ≥ 4.5:1 texto, alvo de toque ≥ 24px, navegável por teclado
- Confirmação destrutiva proporcional: irreversível pede digitar o nome, não "ok" reflexo

## Microcopy dos pontos de fricção

- [cadastro/checkout/cancelamento: as frases exatas — "algo deu errado" é proibido]
