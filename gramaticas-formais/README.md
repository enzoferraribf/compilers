# Gramáticas Formais

![Esquema](./esquema.png)

- [Formalização de Gramáticas](formalizacao-de-gramaticas)
- [Processo de Derivação](processo-de-derivacao)
- [Construção de Gramáticas Formais](construcao-de-gramaticas-formais)
- [Hierarquia de Chomsky](hierarquia-de-chomsky)
- [Exercícios](exercicios)
- [Notações Gramaticais](notacoes-gramaticais)
- [Transformação entre Notações](transformacao-entre-notacoes)

## Exemplo

gramática que descreve `(xy)+|zx*`

```
G = (V, Σ, P, S)
V = { S, A, B, x, y, z }
Σ = { x, y, z }
P = {
  S -> xyA,
  S -> zB,
  A -> xyA,
  A -> ε,
  B -> xB,
  B -> ε
}

L = { xy, xyxy, xyxyxy, ..., z, zx, zxx, zxxx, ... }
```
