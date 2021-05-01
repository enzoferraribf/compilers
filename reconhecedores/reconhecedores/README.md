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

`1` **Texto de Entrada:** cadeia que será testada pelo reconhecedor.

`2` **Linguagem de Entrada:** linguagem a qual a cadeia pertence.

`3` **Cursor:** aponta para o átomo da cadeia que está sendo analisado no momento.

`4` **MFE (Máquina de Finitos Estados):** coração do reconhecedor. Possui um estado interno, e sabe para qual estado mudar, dependendo do átomo que o cursor está apontando e o seu estado atual.

`5` **Memória Auxiliar:** repositório que guarda informações que o MFE achar necessário.

`6` **Linguagem da Memória Auxiliar:** linguagem a qual a memória auxiliar pertence.

## Funcionamento (MFE)

- Movimenta o cursor pelo texto de entrada
- Lê uma posição do texto de entrada por vez
- Armazena o conteúdo na memória auxiliar
- Lê o conteúdo da memória auxiliar
- Muda o estado interno da máquina

## Configuração

Registra a situação da MFE em um determinado momento.
