# **Tradutores**

| Conceitos  |    Texto     |    Linguagem     |
| :--------: | :----------: | :--------------: |
| **Fonte**  | Texto fonte  | Linguagem fonte  |
| **Objeto** | Texto objeto | Linguagem objeto |

<br />

### Conceitos envolvidos:

- **Texto**: elemento trabalhado pela tradução
  - **Ex.:** código, escrita, fala, desenho...
- **Linguagem**: universo conhecido pelo tradutor
  - **Ex.:** Java, C, português, inglês
- **Fonte**: entrada entendida pelo tradutor
- **Objeto**: saída produzida pelo tradutor

### Características

- Mantêm o **significado**
- Traduz apenas o que for **relevante**

<br/>

**Obs.:** linguagem de baixo nível = linguagem de montagem = assembly

<br/>

## **Montadores**

```ts
montador(textoFonte: BaixoNivel) => textoObjeto: Maquina;
```

**Obs.:** Montador = Assembler

O montador pode necessitar de uma tabela de símbolos, para fazer o link de endereços a nomes criados no programa.

<br />

## **Compiladores**

Compilador é um software que faz parte de um conjunto especial de softwares conhecidos como software básico.

```ts
compilador(textoFonte: AltoNivel) => textoObjeto: AltoNivel | BaixoNivel
```

**Tempo de compilação:** momento em que o código é compilado.

**Tempo de execução:** momento em que o código é executado pelo SO.

[**Casos especiais**](/conceitos-basicos/tradutores/casos-especiais)

<br />

## **Interpretadores**

```ts
 interpretador(textoFonte: AltoNivel) => executar(textoFonte);
```

- Roda o código-fonte escrito como sendo o código objeto

- O programa vai sendo utilizado na medida em que é traduzido

- A cada execução do programa precisa ser novamente traduzido e interpretado

- Nos interpretadores não existe texto objeto

- A tradução e a execução do código acontecem ao mesmo tempo, ou seja, não existe tempo de compilação e tempo de execução, somente a interpretação.

<br />

## **(Engenharia reversa)**

<br/>

### **Decompiladores**

```ts
 decompilador(textoFonte: BaixoNivel) => textoObjeto: AltoNivel;
```

### **Demontadores**

```ts
demontador(textoFonte: Maquina) => textoObjeto: BaixoNivel;
```

### **Obfuscadores**

```ts
obfuscador(textoFonte: AltoNivel) => embaralhar(textoFonte): AltoNivel;
```
