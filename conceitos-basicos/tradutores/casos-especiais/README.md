# Compiladores | Casos especiais

Existem outras denominações para `compiladores especiais` a depender de suas características. Classificar um compilador por uma destas denominações especiais **não exclui** a possibilidade da classificação do mesmo compilador em alguma outra denominação. **Um mesmo compilador pode ser classificado em várias destas denominações ao mesmo tempo** (desde que respeite as características definidas).

<br/>

## **Transpiladores**

```ts
transpilador(textoFonte: AltoNivel) => textoObjeto: AltoNivel
```

**Obs.:** Quando a linguagem que você escreve é transformada para JavaScript, elas são chamados de linguagem **_compile-to-JS_**

- **Ex.:** CoffeScript, TypeScript, ES2015...

<br/>

## **Filtros**

```ts
filtro(textoFonte: AltoNivel) => (textoObjeto ~= textoFonte): AltoNivel
```

**Obs.:** Normalmente usados para uniformizar códigos em padrões ou variações de determinada linguagem

<br/>

## **Pré-processadores**

```ts
tradutor(
  preprocessador(textoFonte: AltoNivel) => textoObjeto: AltoNivel
)
```

**Obs.:** produzem um código equivalente para que seja **compilado pelo próximo tradutor**.
