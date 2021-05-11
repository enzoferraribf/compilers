# Formalização de Gramáticas

Uma gramática é uma quádrupla ordenada `G = (V, Σ, P, S)`, sendo:

- `V` vocabulário
- `Σ` alfabeto
- `P` produções gramaticais
- `S` símbolo inicial

## Vocabulário `V`

Conjunto de todos os elementos simbólicos utilizados para definir as leis de formação da gramática

- Contém todos os elementos terminais e não terminais necessários para descrever a gramática

## Alfabeto `Σ`

Conjunto de todos os elementos simbólicos utilizados para definir as sentenças da linguagem

- É o conjunto dos símbolos terminais
- **Obs.:** Todos os símbolos que `V` tem que `Σ` não tem compõem o conjunto dos não-terminais `N`, que não é declarado imperativamente, mas sim deduzido.

## Produções Gramaticais `P`

Conjunto das leis de formação de sentenças

- Principal conjunto da gramática
- Os elementos deste conjunto são chamados de `leis de formação` ou `produções gramaticais`
- **Formato:** `α -> β`
  - cadeia `α` gera cadeia `β`
  - `α ∊ V*.N.V*`: `α` precisa ter ao menos 1 elemento não terminal
  - `β ∊ V*`: `β` precisa ser formado de qualquer combinação de elementos do conjunto `V`

## Símbolo Inicial `S`

Símbolo que inicia todo o processo de produção de sentenças da linguagem.

- `S ∊ V`: Pertence ao vocabulário `V`
