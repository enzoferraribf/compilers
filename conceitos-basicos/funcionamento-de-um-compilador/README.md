# **Funcionamento de um Compilador**

![Esquema das partes de um compilador](./modelo-geral.png)

## Modelos

- [Análise / Síntese](/conceitos-basicos/funcionamento-de-um-compilador/analise-sintese)
- [Front-End / Back-End](/conceitos-basicos/functionamento-de-um-compilador/front-end-back-end)

### **Analisador Léxico**

Identifica os átomos do texto fonte

- Faz análise do texto fonte
- Varre todo o texto fonte da esquerda para a direita
- Agrupa caracteres em átomos (tokens)
- Checa com padrões determinados de formação dos átomos
- Classifica átomos identificados nos tipos de átomos possíveis
- Identifica palavras reservadas da linguagem
- Monta registros iniciais na tabela de símbolos
- Utiliza construções não recursivas

### **Analisador Sintático**

Verifica sequência correta de átomos

- Faz análise hierárquica do texto fonte
- Agrupa os átomos em frases gramáticas
- Trabalha sobre regras da linguagem (definidas em gramáticas formais)
- Pode conter regras recursivas
- Representa as frases gramaticais em uma árvore
- Exemplo de verificação de sequências ou regras: balanceamento de parênteses

### **Analisador Semântico**

Verifica coerência de significados

- Pode alterar conteúdo da árvore sintática montada
- Tarefa importante é a checagem de tipo
- Efetua ou não conversões de tipo (depende da definição da linguagem)
- Pode eliminar ineficiência na estrutura

### **Gerador de Código Intermediário**

Traduz para lógica de formato de máquina

- Gera representação numa terceira linguagem
- Gera programa para execução em máquina abstrata, fictícia
- Deve gerar código que seja fácil de produzir e, ao mesmo tempo, fácil de traduzir
- Existem vários tipos de representação usados
- O código deve ser indenpendente de máquina

### **Otimizador de Código**

Melhora código intermediário gerado

- Elimina redundâncias
- Reduz ineficiências
- Torna o código mais simples e mais rápido
- Diminui o número de instruções
- Existe grande variedade de tipos de otimização
- Há classe de compiladores com ênfase nesta fase

### **Gerador de Código Final**

Gera o código final resultado da compilação

- Compõe-se de código de máquina relocável ou assembly nos casos mais comuns
- Como alternativa pode gerar códigos em linguagem de alto nível nos casos de transpiladores, filtros ou preprocessadores
- Nos casos mais comuns as instruções em código intermediário são traduzidas emde instruções em linguagem de montagem
- Aspecto crítico: uso de registradores de cada arquitetura de máquina

### **Rotinas de tratamento de Erros**

Controla a ocorrência de erros

- Tenta descrever a falha encontrada em uma das partes do compilador
- Tenta recuperar o erro encontrado (tenta continuar a análise do programa)
- Em cada parte do trabalho do compilador serão descritos os vários erros
- Pode ser uma rotina independente ou diluída

### **Gerenciador da Tabela de Símbolos**

Gerencia o repositório tabela de símbolos

- Estrutura de dados global
- Módulo de código e a própria estrutura de dados
- Grava identificadores e símbolos que foram encontrados no programa fonte
- Armazena informações sobre vários atributos destes símbolos
- Exemplos de atributos: localização de memória, tipo da variável, escopo da variável, numero e tipo dos parâmetros das rotinas, etc.
- É utilizada por todas as outras partes

## **Exemplo**

Suponha a sentença `pos = 8 + 5 * tempo`. Após ser submetido ao _analisador léxico_, é preenchida a tabela de símbolos (mediado pelo _gerenciador da tabela de símbolos_):

| ID  | Lexeme  |   Tipo    | Átomo |
| :-: | :-----: | :-------: | :---: |
|  1  |  `pos`  |  `real`   | `id1` |
|  2  |   `=`   |           | `sa`  |
|  3  |   `8`   | `inteiro` | `co1` |
|  4  |   `+`   |           | `ss`  |
|  5  |   `5`   | `inteiro` | `co2` |
|  6  |   `*`   |           | `sm`  |
|  7  | `tempo` |  `real`   | `id2` |

Preenchida a tabela, a árvore sintática é gerada pelo _analisador sintático_

```
    sa
   /  \
id1    ss
      /  \
   co1    sm
         /  \
      co2    id2
```

O _analisador semântico_ verifica os tipos requeridos pelas operações e altera a árvore de forma a respeitar esses tipos

```
    sa
   /  \
id1    ss
      /  \
    ir    sm
    |    /  \
   co1  ir   id2
        |
       co2
```

Finaliza a etapa de análise, o _gerador de código intermediário_ realiza o processo de síntese do código

```
aux1 = int_to_real(co2)
aux2 = aux1 * id2
aux3 = int_to_real(co1)
aux4 = aux3 + aux2
id1 = aux4
```

O _otimizador de código_ recebe o código intermediário e realiza o processo de otimização

```
aux2 = 5.0 * id2
id1 = 8.0 + aux2
```

Por fim, o _gerador de código final_ traduz para assembly

```
MOVF    id2,R1
MULF    7.0,R1
MOVF    R1,aux2
MOVF    aux2,R1
ADDF    3.0,R1
MOVF    R1,id1
```
