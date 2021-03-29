# **Construção de Compiladores**

## Metas

Definir metas de uso do compilador

- Qual será a finalidade com compilador?
- Quem será seu usuário típico?
- Velocidade no tempo de compilação ou velocidade no tempo de execução?
- Mensagem de erro devem ser claras?
- Mais velocidade para o programa ou menos ocupação em memória?
- Não é possível criar um compilador perfeito em tudo (_tradeoff_)

<br/>

## Passos

Definir a quantidade de passos de compilação que o compilador vai ter

**Passo de compilação:** Um passo de compilação é definido pela quantidade de vezes que o compilador lê o texto fonte por inteiro, ou algum texto fonte intermediário

![Exemplos](./passos.png)

### Vantagens de compiladores de muitos passos

- Menor utilização de mémoria do compilador
- Maior possibilidade de executar otimizações
- Projetos e implementações mais independentes

### Vantagens de compiladores de poucos passos

- Menor volume de entrada e saída
- Redução do tempo de compilação
- Redução da complexidade do projeto total

### Técnica de BackPatching

Durante a compilação, itens ainda não conhecidos pelo compilador são substiuídos por lacunas, que serão preenchidas quando os itens forem encontrados

**Obs.:** Esse retorno não configura novos passos na compilação

<br/>

## Blocos || Overlays || Fases (ou overlays)

Definir a quantidade de blocos de código que o compilador vai ter

**Bloco de código:** Um bloco de código é definido pela quantidade de arquivos que o compilador vai gerar no fim de sua compilação. Esses blocos serão executados apenas quando for necessário.

Separar o código em vários arquivos é útil para reduzir o consumo de memória, pois as dlls só serão executadas caso for necessário.

<br/>

## Esquemas

Definir qual o esquema de implementação que vai ser usado

- Esquema de implementação é a decisão sobre como cada parte do processo de compilação (Léxico, Sintático e Semantico) vão se comunicar entre si para formar o compilador

A parte principal geralmente é a que tem mais código (a parte mais volumosa do compilador)

### Programa principal: analisador sintático (mais usado)

Esquema de implementação em que o analisador sintático é o mais importante dentre as 3 partes

### Programa principal: analisador léxico

Esquema de implementação em que o analisador léxico é o mais importante dentre as 3 partes

### Programa principal: analisador semântico / gerador de código

Esquema de implementação em que o analisador semântico e o gerador de código são os mais importantes dentre as 3 partes

### Co-rotinas

Representa uma iteração "_infinita_". Cada trecho de código roda independente num processador ou numa máquina diferente. Todos os trechos repetem permanentemente a tarefa a que se destinam.

<br/>

## Linguagens

Definir as linguagens fonte e objeto que serão tratadas pelo compilador

Maneiras de formalizar linguagens:

- **Enumeração:** Vê se o texto se encontra dentro de uma lista pré-preenchida

- **Gramáticas Formais:** Vê se o texto cumpre as regras pré-estabelecidas da linguagem

- **Reconhecedores (ou autômatos):** Testa o texto fonte para ver se ele respeita as regras de sua linguagem

Enumeração não é utilizada para linguagens de alto nível, por ser finita. Então, é necessário que se use as duas outras opções. Primeiro formaliza-se a gramática da linguagem, depois desenvolve-se reconhecedores que validam o texto fonte, verificando se o mesmo respeita as regras de sua linguagem

![formalização da linguagem fonte](./linguagens.png)

<br/>

## Ambiente

Definir a plataforma e a linguagem de programação que será usada para desenvolver o compilador

Definir as **plataformas**, sendo elas de origem (a de desenvolvimento do compilador), e a de destino do compilador (em qual ele vai rodar)

Definir as **lingugagens de programação**, sendo elas de origem (a de desenvolvimento do compilador), e a de destino do compilador (que linguagem ele compila)

### Classificação pelo Uso das Máquinas

**Autoresidente:** Todo compilador que roda depois de pronto na mesma plataforma de máquina em que ele foi desenvolvido

**Cruzado (ou _cross-compiler_):** Todo compilador que roda depois de pronto em uma plataforma de máquina (chamada de máquina hospedeira) diferente da plataforma de máquina que foi usada no seu desenvolvimento

### Classificação pelo Uso das Linguagens de Programação

**Autocompilável:** Todo compilador que usa (em algum momento de sua construção) como linguagem de programação para o seu desenvolvimento a mesma linguagem de programação que deve ser traduzida por ele (linguagem fonte)

**Normal:** Qualquer compilador não autocompilável.

### Método de BootStrapping

Método para desenvolver compiladores autocompiláveis

**Momento Inicial:** Onde começa o processo. Nele dispomos de recursos para iniciar o desenvolvimento.

Os recursos são:

- **LD:** Linguagem a ser usada no desenvolvimento
- **MD:** Máquina a ser utilizada no desenvolvimento

**Momento Final:** Quando o compilador tiver sido produzido. Nele atendemos os requisitos propostos para o compilador

Os requisitos são:

- **LC:** Linguagem que se quer compilar
- **MC:** máquina onde o compilador vai executar (rodar)

#### Diagrama T

![Diagrama T](./diagrama-t.png)

- 1: linguagem fonte do compilador
- 2: linguagem objeto do compilador
- 3: linguagem de desenvolvimento do compilador

#### Esquema Exemplo

**Momento inicial** recursos

- Maquina Intel
- Compilador de C (devc.exe)

**Momento final** requisitos

- Maquina Arm
- Compilador de O#

Inicialmente, temos um compilador de `C`, em código de máquina Intel, que gera códigos para linguagem de máquina Intel

```
c_to_intel.exe
 _____________________
|_C_           _Intel_|
    |_LMIntel_|
```

Com apenas esse compilador em mãos, e apenas usando uma máquina Intel, podemos desenvolver um compilador da nossa linguagem nova, `O#`, que compila para `Intel`. Esse compilador será desenvolvido em `C` (pois o único compilador que temos no momento é um compilador de `C`).

```
osh_to_intel.c
 ________________
|_O#_     _Intel_|
     |_C_|
```

Após desenvolvido o compilador, podemos compilá-lo no nosso `c_to_intel.exe` e gerar um executável do nosso osharp que roda em `Intel`

```
c_to_intel.exe(osh_to_intel.c) => osh_to_intel.exe
 ________________        ____________________
|_O#_     _Intel_|______|_O#_         _Intel_|
     |_C_|_C_         _Intel_|_Intel_|
             |_Intel_|
```

Tendo nosso compilador de `O#` rodando em `Intel`, desenvolvemos outro compilador. Dessa vez, esse compilador será desenvolvido em `O#`, e ele compilará de `O#` para `Arm` (a máquina requisitada)

```
osh_to_arm.osh
 _______________
|_O#_      _Arm_|
     |_O#_|
```

Após isso, podemos compilar `osh_to_arm.osh` no nosso previamente criado `osh_to_intel.exe`, o qual gerará um compilador de `O#` para `Arm` que roda em `Intel`

```
osh_to_intel.exe(osh_to_arm.osh) => osh_to_arm.exe
 _______________           __________________
|_O#_      _Arm_|_________|_O#_         _Arm_|
     |_O#_|_O#_         _Intel_|_Intel_|
               |_Intel_|
```

Obtido nosso `osh_to_arm.exe`, podemos usá-lo para compilar novamente o `osh_to_arm.osh`, e aí sim termos um compilador de `O#` para `Arm` que roda em `Arm`, que era nosso requisito final

```
osh_to_arm.exe(osh_to_arm.osh) => osh_to_arm.aif
 _______________         ________________
|_O#_      _Arm_|_______|_O#_       _Arm_|
     |_O#_|_O#_         _Arm_|_Arm_|
               |_Intel_|
```

Podemos montar uma tabela para classificar corretamente todos os 5 compiladores envolvidos nesse processo (não vamos incluir o `c_to_intel.exe`)

|     Compilador     | Autoresidente | Cruzado | Autocompilável | Normal |
| :----------------: | :-----------: | :-----: | :------------: | :----: |
|  `osh_to_intel.c`  |       x       |         |                |   x    |
| `osh_to_intel.exe` |       x       |         |                |   x    |
|  `osh_to_arm.osh`  |       x       |         |       x        |        |
|  `osh_to_arm.exe`  |       x       |         |       x        |        |
|  `osh_to_arm.aif`  |               |    x    |       x        |        |

#### Vantagens

Cruzado

- **Multiplicidade de máquinas:** É possível desenvolver programas para diversas plataformas (inclusive plataformas ainda não lançadas), mesmo não tendo acesso a elas

Autocompilável

- **Independência de outras linguagens:** Você pode desenvolver programas apenas em uma linguagem própria
