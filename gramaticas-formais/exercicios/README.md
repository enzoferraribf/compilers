## Lista de Gramáticas

Pessoal,

Segue lista de exercícios de gramática para treinar construção de gramáticas formais e outros assuntos e habilidades relacionadas. Neste momento conseguimos fazer as ações 01, 02, 03 e 04. Não precisa entregar esta lista.

Estou à disposição para dúvidas na resolução dos exercícios.

# Lista de Exercícios para Treinamento de Gramáticas

Para as seguintes linguagens abaixo, escritas na notação de `expressões regulares`, execute cada uma das ações pedidas.

- Alfabeto: `Σ = { 0, 1, 2, 3, 4, 5, 6, 7 }`

## Linguagens

a) `01*2`

b) `2*10*`

c) `1*0*2*`

d) `(01)*2`

e) `(01)*2*`

f) `(01)*(02)*`

g) `01+2+`

h) `2+10*`

i) `1+0+2+`

j) `(01)+2`

k) `(01)+(02)+`

l) `(0|1)2+`

m) `(0|1)2(0|1)3(0|1)`

n) `(0|1)*`

o) `(0*|1*)`

p) `(0|1)+2`

q) `(0|1)*(2|1)+`

r) `01 | 2* 3`

s) `(01|2)* 3`

t) `(01|23)* 4`

u) `(0+|1*) 3`

v) `(01|23*)4+`

w) `(01|(23)*)4+`

x) `(01|23+)* 4+`

y) `(01*2|34+5) 6`

z) `(0+12|34+5)+ (67)*`

## Ações

1. Escreva uma gramática na notação de produções gramaticais que defina esta linguagem
2. Classifique a gramática segundo Chomsky (mais restritiva)
3. Crie outra gramática na notação de produções gramaticais que seja classificada de forma mais restrita em outra classificação de Chomsky diferente da primeira.
4. Modifique a gramática gerada na notação de produções gramaticais de forma a passar a gerar um outro conjunto de sentenças e tente identificar qual a linguagem que passa a ser gerada.
5. Transforme a gramática modificada para a notação BNF seguindo o método visto em sala
6. Escreva uma gramática na notação BNF que defina a linguagem original
7. Escreva uma gramática na notação de Wirth que defina a linguagem original
8. Transforma a gramática gerada na notação de Wirth para a notação BNF usando o modo canônico visto em sala de aula.
9. Escreva uma gramática na notação ferroviária que defina a linguagem original

## Respostas

### a.1

```
G = (V, Σ, P, S)
V = { S, A, 0, 1, 2 }
P = {
  S -> 0A2,
  A -> 1A,
  A -> ε
}
```

### a.2

`Irrestrita`

- [x] `α -> β` `α ∊ V*.N.V*` `β ∊ V*` Configura uma gramática válida
- [ ] `α -> β` `|α| <= |β|` A derivação não encurta a cadeia
- [ ] <del>`α -> β` `α ∊ N`: `α` Apenas não terminais isolados geram derivações</del>
- [ ] <del>`α -> β` `β = δπ` `δ ∊ Σ*` `π ∊ N ou π = ε` Não gera novas derivações à esquerda</del>
- [ ] <del>`α -> β` `β = πδ` `δ ∊ Σ*` `π ∊ N ou π = ε` Não gera novas derivações à direita</del>

### a.3

```
G = (V, Σ, P, S)
V = { S, A, 0, 1, 2 }
P = {
  S -> 0A,
  0A -> 01A,
  0A -> 02,
  1A -> 11A,
  1A -> 12
}
```

`Sensível ao Contexto`

- [x] `α -> β` `α ∊ V*.N.V*` `β ∊ V*` Configura uma gramática válida
- [x] `α -> β` `|α| <= |β|` A derivação não encurta a cadeia
- [ ] `α -> β` `α ∊ N`: `α` Apenas não terminais isolados geram derivações
- [ ] <del>`α -> β` `β = δπ` `δ ∊ Σ*` `π ∊ N ou π = ε` Não gera novas derivações à esquerda</del>
- [ ] <del>`α -> β` `β = πδ` `δ ∊ Σ*` `π ∊ N ou π = ε` Não gera novas derivações à direita</del>

### a.4

```
G = (V, Σ, P, S)
V = { S, A, 0, 1, 2 }
P = {
  S -> 0A,
  0A -> 10A,
  0A -> 02,
  1A -> 11A,
  1A -> 12
}
```

`L = { 02, 102, 1102, 11102, ... }`

### a.5

```
S ::= 0<A>
0<A> ::= 10<A>|02
1<A> ::= 11<A>|12
```

### a.6

```
S ::= 0<A>2
A ::= 1<A>|ε
```

### a.7

```
S = "0"{"1"}"2"
```

### a.8

```
S ::= 0<A>2
A ::= 1<A>|ε
```

### a.9

```
  0       2
o-------o--->
    ↑   |
    |___|
      1
```
