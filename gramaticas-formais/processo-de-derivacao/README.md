# Processo de Derivação

- Sempre é iniciado pelo símbolo inicial da gramática `S`
- Obedecendo as leis de formação, tenta-se chegar à cadeia em questão. Se for possível, então a cadeia é sentença
- A linguagem é o conjunto de todas as sentenças possíveis de serem formadas pelas leis de formação

Uma cadeia `ω` será sentença se:

- Existir uma sequencia de substituições definidas na gramática que permita partir do simbolo inicial `S` e chegar até a cadeia `ω`

`S => ω1 => ω2 => ω3 => ... => ωn => ω`: Processo de derivação da sentença `ω`

## Representação

- `=>`: Representa passos de derivação (não confundir com `->`)
  - `->`: Usado para construir as regras de substituição
- `=+>` **Derivação direta:** indica que houve apenas 1 passo de derivação (aplicação de apenas 1 produção gramatical)
- `=*>` **Derivação não trivial:** indica que, de uma cadeia para outra, houve 1 ou mais substituições
- `=>` **Derivação (pura e simples):** Indica a derivação completa, partindo do primeiro símbolo, chegando até a cadeia final (pula todas as etapas intermediárias)
- `=n>` **Comprimento:** É a quantidade de regras de produção gramatical que foram utilizadas em um passo de substituição.
