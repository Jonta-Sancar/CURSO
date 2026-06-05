# JavaScript (parte 2) - Variaveis e constantes

> Modulo: JavaScript

## Objetivo da aula
Declarar variaveis com `var`, `let` e `const`, entender as diferencas de escopo entre elas e inspecionar valores no console.

## Exemplo rapido
```js
const nome = "Ana";
let idade = 28;

console.log(nome);  // Ana
console.log(idade); // 28

idade = 29;
console.log(idade); // 29
```

## Tipos de dados primitivos

| Tipo | Exemplo | Descricao |
|------|---------|-----------|
| `string` | `"ola"`, `'mundo'` | Texto |
| `number` | `42`, `3.14`, `-7` | Numeros inteiros e decimais |
| `boolean` | `true`, `false` | Verdadeiro ou falso |
| `null` | `null` | Ausencia intencional de valor |
| `undefined` | `undefined` | Variavel declarada sem valor |

```js
let texto = "JavaScript";
let numero = 42;
let decimal = 3.14;
let ativo = true;
let vazio = null;
let indefinido;

console.log(typeof texto);     // string
console.log(typeof numero);    // number
console.log(typeof ativo);     // boolean
console.log(typeof vazio);     // object  (peculiaridade historica do JS)
console.log(typeof indefinido); // undefined
```

## `var`, `let` e `const`

| Palavra-chave | Escopo | Reatribuicao | Redeclaracao |
|---------------|--------|--------------|--------------|
| `var` | Funcao | Sim | Sim |
| `let` | Bloco `{}` | Sim | Nao |
| `const` | Bloco `{}` | Nao | Nao |

```js
// let — escopo de bloco
if (true) {
  let x = 10;
  console.log(x); // 10
}
// console.log(x); // ReferenceError: x is not defined

// const — nao pode ser reatribuida
const PI = 3.14159;
// PI = 3; // TypeError

// var — escopo de funcao (evitar em codigo moderno)
var legado = "nao use var";
```

> Use `const` por padrao. Use `let` apenas quando precisar reatribuir. Evite `var`.

## Template literals

Forma moderna de montar strings com variaveis:

```js
const nome = "Carlos";
const idade = 30;

console.log(`Meu nome e ${nome} e tenho ${idade} anos.`);
```

## Pratica sugerida (exercicio concreto)
### Projeto: Ficha de usuario no console

### Requisitos obrigatorios
1. Declare com `const`: nome, email.
2. Declare com `let`: idade, cidade.
3. Exiba todos os dados com `console.log` usando template literals.
4. Altere a cidade para outro valor e exiba novamente.
5. Use `typeof` para inspecionar o tipo de cada variavel e exiba no console.

### Entrega esperada
- Arquivo `ficha.js` na pasta da aula, executado via `<script src>` em um `index.html`.

## Desafio opcional
Tente reatribuir uma `const` e observe o erro no console. Comente a linha com a explicacao do que aconteceu e por que.

## Navegacao
- [Aula anterior: JavaScript (parte 1) - Overview](../javascript-parte-1-overview/)
- [Voltar para JavaScript](../../)
- [Proxima aula: JavaScript (parte 3) - Operadores e verificadores condicionais](../javascript-parte-3-operadores-e-verificadores-condicionais/)
