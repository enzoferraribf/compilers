# Autômatos Finitos

`M = (Q, Σ, P, q0, F)`

- `Q` Estados Internos
  - Conjunto de estados internos possíveis da MFE
  - Finito e não vazio
- `Σ` Alfabeto de Entrada
  - Conjunto de todos os símbolos a serem usados na formação de sentenças da linguagem
  - Finito e não vazio
- `P` Transição de Estado
  - Função de transição de estado
  - Mapeia `Q × (Σ ∪ {ε})` em `Q`
- `q0` Estado Inicial
  - Um dos elementos de `Q`, `(q0 ∈ Q)`
  - Estado único
- `F` Estados de aceitação
  - Conjunto de estados finais de aceitaçao
  - Subconjunto de `Q`, `(F ⊂ Q)`
  - Chamado também de estados finais

## Reconhecimento (autômato finito)

Processo de aplicação do conjunto de regras de teste para uma determinada cadeia

- Serve para determinar se esta cadeia pertence ou não a linguagem que está sendo definida
- A cadeia que passa pelos testes é _reconhecida_ como parte da linguagem
- A cadeia que não passa pelos testes não é aceita como parte da linguagem
- Equivalente ao processo de derivação nas gramáticas formais

### Funcionamento

- Coloca o autômato finito na configuração inicial:
  - Cursor apontando para a primeira posição do texto de entrada
  - Estado interno da máquina é o inicial `q0`
- Aplica regras de transição de estado `P` baseado no estado atual (elemento de `Q`) e no símbolo lido (elemento de `Σ` ou `ε`):
  - Determina um novo estado da máquina
  - Movimenta cursor para a posição seguinte no texto de entrada
- Aplica função de transição novamente até chegar na posição após o último elemento do texto de entrada (configuração final)
- Testa o estado que ficou na configuração final
  - Se for um dos estados `F` aceita a cadeia

## Exemplo

```
M = (Q, Σ, P, A, F)
Q = { A, B }
Σ = { 0, 1 }
P = {
  (A, 0) → A,
  (A, 1) → B,
  (B, 0) → B,
  (B, 1) → A
}
F = { B }
```
