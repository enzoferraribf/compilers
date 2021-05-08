# Notações Gramaticais

São formatações para formalização de gramáticas.

- **Metalinguagem:** São linguagens que descrevem linguagens

## Produções Gramaticais

- Formato usado até então nas anotações
- Simbologia mais matemática
- Exige definição explícita dos 4 elementos formalizadores da gramática
- `G = (V, Σ, P, S)` **Gramática**
  - `V` **vocabulário**, o conjunto de átomos da gramática
    - `V = Σ U N` o vocabulário é a união do átomos terminais e não terminais
  - `Σ` **alfabeto**, o conjunto dos átomos terminais
  - `P` **produções**, o conjunto das regras de substituição
    - `α -> β` `α ∊ V*.N.V*` `β ∊ V*` uma cadeia `α` com pelo menos 1 não terminal gera uma cadeia `β`, que pode ter não terminais ou não
    - A derivação só finaliza quando `β` não tem mais não terminais
  - `S` **símbolo inicial**, o não terminal pelo qual a derivação deve começar
    - `S ∊ V` o vocabulário precisa ter esse símbolo inicial
- `N = V - Σ` **não terminais** são obtidos por dedução. Os átomos de `V` que `Σ` não possui são não terminais
- Permite **recursão**

| Simbologia |       Significado       |
| :--------: | :---------------------: |
|    `A`     |      não terminal       |
|    `b`     |        terminal         |
|            |       agrupamento       |
|            |       iteração 0+       |
|            |       iteração 1+       |
|            |   construção opcional   |
|    `->`    |  sinal de substituição  |
|            |           ou            |
|    `xy`    |      concatenação       |
|    `ε`     |      cadeia vazia       |
|            | delimitador de produção |

| Legenda  |                         |
| :------: | :---------------------: |
|   `A`    | elemento qualquer `∊ N` |
|   `b`    | elemento qualquer `∊ Σ` |
| `x`, `y` | cadeia qualquer `∊ V*`  |

### Exemplo

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

Gera `L = { a, ba, bba, bbba, ... }`

## BNF

- Formato mais popular para representação gramatical
- Cada produção é uma lei de substituição
- Permite **recursão**
- O **vocabulário** e o **alfabeto** são implicitamente declarados
- O **símbolo inicial** é o primeiro não terminal com lei de substituição declarada

| Simbologia |       Significado       |
| :--------: | :---------------------: |
|   `<X>`    |      não terminal       |
|    `X`     |        terminal         |
|   `(Ω)`    |       agrupamento       |
|            |       iteração 0+       |
|            |       iteração 1+       |
|            |   construção opcional   |
|   `::=`    |  sinal de substituição  |
|    `\|`    |           ou            |
|    `xy`    |      concatenação       |
|    `ε`     |      cadeia vazia       |
|            | delimitador de produção |

| Legenda  |                                  |
| :------: | :------------------------------: |
|   `X`    | elemento qualquer do vocabulário |
|   `Ω`    |   lei qualquer de substituição   |
| `x`, `y` |         cadeia qualquer          |

### Exemplo

```
<S> ::= <A>a | c
<A> ::= <A>b | ε
```

Gera `L = { c, a, ba, bba, bbba, ... }`

## Wirth (ou BNF Estendido)

- Variante do BNF
- Oferece mecanismos de substituição de recursões por iterações
- Permite **recursão**, mas é contraindicado (?)
- O **vocabulário** e o **alfabeto** são implicitamente declarados
- O **símbolo inicial** é o primeiro não terminal com lei de substituição declarada

| Simbologia |       Significado       |
| :--------: | :---------------------: |
|    `X`     |      não terminal       |
|   `"X"`    |        terminal         |
|   `(Ω)`    |       agrupamento       |
|   `{Ω}`    |       iteração 0+       |
|            |       iteração 1+       |
|   `[Ω]`    |   construção opcional   |
|    `=`     |  sinal de substituição  |
|   `Ω\|Ω`   |           ou            |
|    `xy`    |      concatenação       |
|            |      cadeia vazia       |
|    `.`     | delimitador de produção |

| Legenda  |                                  |
| :------: | :------------------------------: |
|   `X`    | elemento qualquer do vocabulário |
|   `Ω`    |   lei qualquer de substituição   |
| `x`, `y` |         cadeia qualquer          |

### Exemplo

```
S = {X"a"} | "c".
X = ["c"]"a" | {"b"}"a".
```

Gera `L = { ε, c, aa, caa, baa, bbaa, bbbaa, ... }`

## Expressão Regular

- Popular em textos mais teóricos
- São descritos em uma linha só
- Não possuem não terminais
- Não há **recursão**
- O **vocabulário** e o **alfabeto** são implicitamente declarados
- Não há **símbolo inicial**

| Simbologia  |       Significado       |
| :---------: | :---------------------: |
|             |      não terminal       |
|     `a`     |        terminal         |
|    `(Ω)`    |       agrupamento       |
|    `Ω*`     |       iteração 0+       |
|    `Ω⁺`     |       iteração 1+       |
|             |   construção opcional   |
|             |  sinal de substituição  |
|   `Ω\|Ω`    |           ou            |
| `x y`, `xy` |      concatenação       |
|     `ε`     |      cadeia vazia       |
|             | delimitador de produção |

| Legenda  |                               |
| :------: | :---------------------------: |
|   `a`    | elemento qualquer do alfabeto |
|   `Ω`    | lei qualquer de substituição  |
| `x`, `y` |        cadeia qualquer        |

### Exemplo

```
a* (b c)⁺ | a b b*
```

Gera `L = { bc, abc, aabc, aabcbc, ab, abb, abbb, ... }`

## Expressão Regular Estendida

- Adiciona os não terminais na notação de Expressões Regulares
- **Não terminais** são definidos quando há lei que o substitua
- Permite **recursão**
- O **vocabulário** e o **alfabeto** são implicitamente declarados
- Não há **símbolo inicial**

| Simbologia  |       Significado       |
| :---------: | :---------------------: |
|     `X`     |      não terminal       |
|     `a`     |        terminal         |
|    `(Ω)`    |       agrupamento       |
|    `Ω*`     |       iteração 0+       |
|    `Ω⁺`     |       iteração 1+       |
|             |   construção opcional   |
|     `=`     |  sinal de substituição  |
|   `Ω\|Ω`    |           ou            |
| `x y`, `xy` |      concatenação       |
|     `ε`     |      cadeia vazia       |
|             | delimitador de produção |

| Legenda  |                                  |
| :------: | :------------------------------: |
|   `X`    | elemento qualquer do vocabulário |
|   `a`    |  elemento qualquer do alfabeto   |
|   `Ω`    |   lei qualquer de substituição   |
| `x`, `y` |         cadeia qualquer          |

### Exemplo

```
S = a* (b c)⁺ X
X = a b | b* | c+ b
```

Gera `L = { bc, bcbc, bcab, bcb, bcbcbb, abc, aabcbccccb, ... }`

## Diagrama de Sintaxe (ou Notação Ferroviária)

- Usada na definição de Pascal
- Notação gráfica
- Necessário seguir o fluxo dos trilhos
- Separa-se cadeias com um ponto `•`

### Exemplos

```
expressão regular: ε

--->
```

```
expressão regular: a

-a->
```

```
expressão regular: ba

-b-•-a->
```

```
expressão regular: a⁺

---a-•->
 ↑   |
 └---┘
```

```
expressão regular: b(ab)* ou (ba)*b

---b-•->
 ↑   |
 └-a-┘
```

```
expressão regular: a*

-----•->
 ↑   |
 └-a-┘
```

```
expressão regular: a*b

-----•-b->
 ↑   |
 └-a-┘
```

```
expressão regular: b(acb)* ou (bac)*b

-----b---•->
 ↑       |
 └-c-•-a-┘
```

```
expressão regular: b(cab)*

----b--•->
 ↑     |
 └-c-a-┘
```

```
expressão regular: (a|b|c)*(d|e|f|ε)a

-----•-•-----b->
 ↑   | |   ↑
 └-a-• •-d-┘
 ↑   | |   ↑
 └-b-• •-e-┘
 ↑   | |   ↑
 └-c-• •-f-┘
```

```
expressão regular: a(b(c(dc)*b)*a)*

-----a---•->
 ↑       |   -> a (Y a)*
 └•--b---┘
  |     ↑   -> Y = b (X b)*
  └--c-•┘
   ↑   |   -> X = c (d c)*
   └-d-┘
```
