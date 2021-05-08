# Ambiguidade

Toda produção gramatical pode ser expressa como uma **árvore sintática**.

```
Gramática
  <S> ::= <A><B>
  <A> ::= aa<A> | ε
  <B> ::= <B>bb | a

Geração da sentença "aaaaabb"
          S
      ┌───┴───┐
      A       B
    ┌─┼─┐   ┌─┼─┐
    a a A   B b b
      ┌─┼─┐ |
      a a A a
          |
          ε
```

Se for possível gerar uma mesma sentença com mais de uma árvore sintática, então a gramática é ambígua.

```
Gramática ambígua
  <S> ::= <A>1 | 0<B> | 11
  <A> ::= 0<A> | 0
  <B> ::= 00<B> | 11 | 1

Gerações da sentença ambígua "01"
   S          S
  ┌┴┐        ┌┴┐
  A 1   ou   0 B
  |            |
  0            1
```

Ambiguidade é um problema, e precisa ser consertado.

## Ambiguidade em Compiladores

- Não é bom que compiladores tenham gramáticas ambíguas
- Se houver ambiguidade na gramática, precisam haver regras claras que a resolva
- Quanto mais sucinta e enxuta é uma gramática, mais chances de ser ambígua

### Ambiguidade muda o significado

Dado a seguinte gramática

```
<exp> ::= <exp> + <exp> | <exp> - <exp> | <fator>
<fator> ::= 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9
```

Se formos gerar a sentença `8 - 5 + 7`, temos duas árvores possíveis

```
        exp                  exp
     ┌───┼───┐            ┌───┼───┐
    exp  +  exp          exp  -  exp
  ┌──┼──┐    |            |    ┌──┼──┐
 exp - exp fator   ou   fator exp + exp
  |     |    |            |    |     |
fator fator  7            8  fator fator
  |     |                      |     |
  8     5                      5     7
```

Cada árvore tem seu significado. A primeira, por exemplo, interpreta a sentença como `(8 - 5) + 7 = 10`, mas a segunda interpreta como `8 - (5 + 7) = -4`. Cada interpretação gerou um resultado diferente.

## Tipos de Ambiguidade

Para identificar um tipo de ambiguidade, é preciso comparar duas árvores sintáticas diferentes que geram uma mesma sentença

```
<S> ::= <A>1 | <B>1 | 01 | 0<C>
<A> ::= 0<A> | 0
<B> ::= <B>1 | 0
<C> ::= 0<C> | 1
```

### Estrutural

Quando as árvores são diferentes em sua estrutura

```
 S          S          S
┌┴┐        ┌┴┐        ┌┴┐
0 1   ou   A 1   ou   0 C
           |            |
           0            1
```

### Rótulos

Quando as árvores são iguais em estrutura, mas tem rótulos (não terminais) diferentes

```
 S          S
┌┴┐        ┌┴┐
A 1   ou   B 1
|          |
0          0
```

## Técnicas para Eliminar Ambiguidade

### Associatividade de operadores

Convenções para decidir qual operador vai ser efetuado primeiro para um determinado operando

#### Operadores associativos a esquerda

São resolvidos da esquerda para direita.

- É feito com recursão à esquerda
- A árvore sintática cresce para esquerda
- Ex.: operadores aritméticos

```
Gramática
  <exp> ::= <exp> + <fator> | <exp> - <fator> | <fator>
  <fator> ::= 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9

Sentença           ┌────────────┬─────────────────┐
                   │ Operadores | Associatividade |
  8 - 5 + 7        │     +      |    esquerda     |
                   |     -      |    esquerda     |
                   └────────────┴─────────────────┘

Árvore sintática
          exp
       ┌───┼───┐
      exp  + fator
    ┌──┼───┐   |
   exp - fator 7
    |      |
  fator    5
    |
    8
```

#### Operadores associativos a direita

São resolvidos da direita para esquerda.

- É feito com recursão à direita
- A árvore sintática cresce para direita
- Ex.: exponenciação, atribuição

```
Gramática
  <exp> ::= <fator> ^ <exp> | <fator>
  <fator> ::= 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9

Sentença           ┌────────────┬─────────────────┐
                   | Operadores | Associatividade |
  2 ^ 3 ^ 4        |     ^      |     direita     |
                   └────────────┴─────────────────┘

Árvore sintática
       exp
    ┌───┼───┐
  fator ^  exp
    |   ┌───┼──┐
    2 fator ^ exp
        |      |
        3      4
```

### Precedência de operadores

Regra de se aplica para operadores diferenciados

- Associatividade não resolve o problema
- Separa os operadores em classes distintas, onde cada classe tem prioridade sobre outra

```
Gramática
  <exp2> ::= <exp2> + <exp1> | <exp2> - <exp1> | <exp1>
  <exp1> ::= <exp1> * <fator> | <exp1> / <fator> | <fator>
  <fator> ::= 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9
```

```
Sentenças          ┌───────┬────────────┬─────────────────┐
                   | Nível | Operadores | Associatividade |
  8 * 5 - 3        |   1   |   * , /    |     esquerda    |
  8 - 5 * 3        |   2   |   + , -    |     esquerda    |
                   └───────┴────────────┴─────────────────┘

Árvores sintáticas
            exp2                    exp2
        ┌────┼───┐              ┌────┼───┐
       exp2  -  exp1          exp2   -  exp1
    ┌───┼───┐     |            |     ┌───┼───┐
   exp1 * fator fator   //    exp1  exp1 * fator
    |       |     |            |     |       |
  fator     5     3          fator fator     3
    |                          |     |
    8                          8     5
```
