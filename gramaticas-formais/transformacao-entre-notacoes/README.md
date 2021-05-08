# **Transformações**

```
PG  →  BNF
 ↑      ↓
BNF ← Wirth
```

## **PG -> BNF**

Para transformar da notação de **Produção Gramatical** para **BNF** deve-se seguir os seguintes passos:

```
G = (V, Σ, P, S)
V = { S, M, a, b }
Σ = { a, b }
P = {
  S -> Ma,
  M -> bM,
  M -> ε
}
```

**1º** - Identificar os símbolos não terminais e batizá-los na nova notação "<>"

```
<S> -> <M>a
<M> -> b<M>
<M> -> ε
```

**2º** Agrupar as regras da mesma cadeia geradora em uma única regra

```
<S> -> <M>a
<M> -> b<M> | ε
```

**3º** Substituir o sinal de atribuição para ::=

```
<S> ::= <M>a
<M> ::= b<M> | ε
```

## **BNF -> PG**

Para transformar da notação de **BNF** para **Produção Gramatical** deve-se seguir os seguintes passos:

```
<S> ::= <M>a
<M> ::= b<M> | ε
```

**1º** Identifica no BNF o símbolo inicial (primeiro símbolo) e monta a definição dos quatro elementos da gramática

```
G = ( , , , S)
``` 

**2º** Monta o vocabulário com todos os símbolos utilizados

```
V = { S, M, a, b }
```

**3º** Monta o alfabeto com os terminais

```
Σ = { a, b }
```

**4º** Monta o conjunto das produções com uma alternativa de substituição em cada regra

```
P = {
  S -> Ma,
  M -> bM,
  M -> ε
}
```

**5º** Define a produção gramatical completamente

```
G = (V, Σ, P, S)
V = { S, M, a, b }
Σ = { a, b }
P = {
  S -> Ma,
  M -> bM,
  M -> ε
}
```

## **Wirth -> BNF**

Para transformar da notação de **Wirth** para **BNF** deve-se seguir os seguintes passos:

```
W = A"x" | "y" (A "x" | B "y").
A = {"x"} "y".
B = ["x" "y" {A | "x" | "z"}]"x""x".
```

**1º** Rebatizam-se os não terminais e identifica-se os agrupamentos existentes

```
                   |--------1--------|
<W> = <A>"x" | "y" (<A> "x" | <B> "y").

      |-2-|
<A> = {"x"} "y".

               |-------4--------|
<B> = ["x" "y" {<A> | "x" | "z"}]"x""x".
      |------------3------------|
```

**2º** Criam-se não terminais adicionais para cada um dos agrupamentos e ajusta-se a sintaxe para BNF

Aqui, valem-se as regras:
- `( )`: opções
- `[ ]`: opções + cadeia vazia
- `{ }`: recursão da definição + opção do vazio

```
               |------1------|
<W> = <A>x | y (<A> x | <B> y)

      |2|
<A> = {x} y

           |-----4-----|
<B> = [x y {<A> | x | z}]xx
      |--------3--------|

<1> ::= <A>x | <B>y
<2> ::= <2>x | ε
<3> ::= xy<4> | ε
<4> ::= <4>(<A>|x|z) | ε
```

**3º** Substitui-se os novos não terminais em seus devidos locais

```
<W> ::= <A>x | y <1>
<A> ::= <2>y
<B> ::= <3>xx
<1> ::= <A>x | <B>y
<2> ::= <2>x | ε
<3> ::= xy<4> | ε
<4> ::= <4>(<A>|x|z) | ε
```

## **BNF -> Wirth**

Para cada lei de substituição, deve se aplicar as regras a seguir.

Sempre que houver alternativas (`|`), analise cada uma, buscando o seguinte:

- Se houver **recursão à direita**, elimine, e troque por `{ }` no ínicio da cadeia

```
          ↓
<S> ::= xy<S> | <S><A> | c<B> | <N>d | <S>xx | a<A> | ε | xx<S>z

S = {"x""y"} ...
```

- Se houver **recursão à esquerda**, elimine, e troque por `{ }` no final da cadeia

```
                  ↓                      ↓
<S> ::= xy<S> | <S><A> | c<B> | <N>d | <S>xx | a<A> | ε | xx<S>z

S = {"x""y"} ... {A | xx}
```

- Se **não** houver recursão, coloque no meio da cadeia entre `( )` (caso não haja `ε`), ou `[ ]` (caso haja)

```
                          ↓      ↓              ↓     ↓
<S> ::= xy<S> | <S><A> | c<B> | <N>d | <S>xx | a<A> | ε | xx<S>z

S = {"x""y"}["c"B | N"d" | "a"A]{A | xx}
```

- Se houver **recursão ao centro**, não é possível eliminar, então ficará no meio, junto com as não recursões

```
                                                            ↓
<S> ::= xy<S> | <S><A> | c<B> | <N>d | <S>xx | a<A> | ε | xx<S>z

S = {"x""y"}["c"B | N"d" | "a"A | xxSz]{A | xx}
```
