# Reconhecedores

Sua função é indicar se uma determinada cadeia pertence ou não a uma linguagem através da aplicação de um conjunto de regras de teste.

```
               ┌-----------------┐
 Cadeia a   -→ |  reconhecedor   | -→ true | false
ser testada    |┌---------------┐|
               └┘ conf. inicial └┘
```

É um dispositivo testador de cadeias

- Obs: Gramática era um dispositivo **gerador** de cadeias
- A **linguagem** é o conjunto de _todas_ as cadeias que passam pelo teste
- Um reconhecedor deve aprovar todas as sentenças da linguagem e somente elas

## Elementos Internos

```
                    2
... ┬-┬-┬-┬-┬-┬-┬-┬-┬-┬-┬-┬- ...
  1 ┴-┴-┴-┴-┴-┴-┴-┴-┴-┴-┴-┴-
     ↑
     | 3     ┌---┐
     └-------┤ 4 |
             └┬-↑┘
             ┌↓-┴┐
             | 5 | 6
             └---┘
```

- `1` **Texto de Entrada:** cadeia que será testada pelo reconhecedor.

- `2` **Linguagem de Entrada:** linguagem a qual a cadeia pertence.

- `3` **Cursor:** aponta para o átomo da cadeia que está sendo analisado no momento.

- `4` **MFE (Máquina de Finitos Estados):** coração do reconhecedor. Possui um estado interno, e sabe para qual estado mudar, dependendo do átomo que o cursor está apontando e o seu estado atual.

  - Movimenta o cursor pelo texto de entrada
  - Lê uma posição do texto de entrada por vez
  - Armazena o conteúdo na memória auxiliar
  - Lê o conteúdo da memória auxiliar
  - Muda o estado interno da máquina

- `5` **Memória Auxiliar:** repositório que guarda informações que o MFE achar necessário.

- `6` **Linguagem da Memória Auxiliar:** linguagem a qual a memória auxiliar pertence.

## Configuração

Registra a situação da MFE em um determinado momento.

- Para que haja esse registro, deve ser informada uma série de informações que definam tal situação.
- Exemplo de uma configuração
  - Texto que está sendo lido
  - Estado interno da máquina
  - Conteúdo da memória auxiliar
- Algumas congurações são especiais
  - Configuração inicial
  - Configuração final

### Configuração Inicial

É restaurada a cada início de reconhecimento de uma cadeia

Elementos da configuração são inicializados com valores pré-determinados:

- O cursor aponta para o **primeiro elemento** do texto de entrada
- O estado interno da máquina **é sempre conhecido** e é chamado de estado inicial ou de repouso
- A memória auxiliar é inicializada **vazia**

### Configuração Final

É a configuração em que se encontra a MFE ao final do processo de reconhecimento de uma cadeia

## Processo de Reconhecimento

```
RESET -→ TRANSIÇÃO
          |     ↑
          ↓     |
         função de
         transição -→ CONF. FINAL -→ ACEITAÇÃO
```

- `RESET` Coloca o reconhecedor na configuração inicial.

- `TRANSIÇÃO` Aplica `função de transição` baseado na configuração atual, gerando uma nova configuração

  - `função de transição`
    - Modifica estado interno da máquina
    - Modifica conteúdo da memória
    - Movimenta posição do cursor sobre o texto de entrada.

- `CONF. FINAL` Aplica `função de transição` até chegar numa configuração final possível

- `ACEITAÇÃO` Testa configuração final para indicar se a cadeia foi aceita ocmo parte da linguagem

## Tipos de Reconhecedores

| Tipo |              Linguagem               |                  Gramática                  |              Reconhecedor               |
| :--: | :----------------------------------: | :-----------------------------------------: | :-------------------------------------: |
|  0   | Conjuntos recursivamente enumeráveis |           Gramáticas irrestritas            |           Máquinas de Turing            |
|  1   |   Linguagens sensíveis ao contexto   |      Gramáticas sensíveis ao contexto       | Máquinas de Turing com memória limitada |
|  2   |    Linguagens livres de contexto     |        gramáticas livres de contexto        |           Autômatos de pilha            |
|  3   |         Conjuntos regulares          | Gramáticas lineares à esquerda ou à direita |            Autômatos finitos            |
