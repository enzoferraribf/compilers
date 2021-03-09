# **Processo de Tradução de um Código**

```elixir
texto_fonte
|> preprocessador1  # texto fonte preparado 1
|> preprocessador2  # texto fonte preparado 2
   ...
|> preprocessadorN  # texto fonte preparado N
|> compilador       # texto em linguagem de montagem
|> montador         # texto em linguagem de máquina relocável
|> load/link-editor # texto em linguagem de máquina
```

## **Pré-Processadores**

[Detalhes](/conceitos-basicos/tradutores/casos-especiais#pré-processadores)

- Produzem dados de entrada para outros compiladores
- É um módulo opcional (pode não existir na tradução)
- Podem existir vários pré-processadores encadeados até se chegar ao último compilador do processo

**Exemplos de atividades realizadas**

- Processamento de macros
- Inclusão de arquivos (header files)
- Pré-processadores racionais (fluxo de controle, estrutura de dados)
- Extensões de linguagem

<br/>

## **Compiladores**

[Detalhes](/conceitos-basicos/tradutores#compiladores)

- O último da cadeia de compiladores, o que irá traduzir o texto para uma linguagem de baixo nível
- Produzem textos para o processo de montagem

<br/>

## **Montadores**

[Detalhes](/conceitos-basicos/tradutores#montadores-assemblers)

- Embutido na maior parte dos compiladores comerciais, embora não seja parte da compilação.

**Exemplos de atividades realizadas**

- Implementação mais comum através dos montadores de duas passagens (passo: leitura do código fonte)
  - **1º passo:** procura todos os identificadores e
    monta tabela de símbolos separada do compilador
  - **2º passo:** monta linguagem de máquina relocável

<br/>

## **Load/Link-Editores**

- **Loader:** Realiza o trabalho de carga
- **Link-edição:** Realiza trabalho de resolução de referências ou editor de ligações de referência

**Exemplos de atividades realizadas**

- Resolve referências de dados e de instruções entre os vários módulos que devem compor o código executável (bibliotecas de rotinas, módulos em processo de compilação, módulos previamente compilados).
- Monta um código "absoluto" de vários módulos em linguagem de máquina relocável

<br/>

## **Exemplo de um Processo**

```
x = 2y + 7
```

Pre-processadores, Compilador

```as
mov  y, R1
mul #2, R1
add #7, R1
mov R1, x
```

Montador

```as
0001 01 00000000 01
0010 01 00000010 00
0011 01 00000111 00
0100 01 00000100 01
```

Load/Link-Editor

```as
0001 01 00001001 01
0010 01 00000010 00
0011 01 00000111 00
0100 01 00001101 01
```
