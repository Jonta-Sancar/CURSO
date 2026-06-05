# JavaScript (parte 3) - Operadores e verificadores condicionais

> Modulo: JavaScript

## Objetivo da aula
Utilizar operadores aritmeticos, de comparacao e logicos, e escrever estruturas condicionais com `if/else`, ternario e `switch`.

## Exemplo rapido
```js
const idade = 20;

if (idade >= 18) {
  console.log("Maior de idade");
} else {
  console.log("Menor de idade");
}
```

## Operadores aritmeticos

```js
console.log(10 + 3);  // 13
console.log(10 - 3);  // 7
console.log(10 * 3);  // 30
console.log(10 / 3);  // 3.333...
console.log(10 % 3);  // 1  (resto da divisao)
console.log(2 ** 3);  // 8  (potenciacao)
```

## Operadores de comparacao

| Operador | Significado | Exemplo | Resultado |
|----------|-------------|---------|-----------|
| `==` | Igual (com coercao) | `"5" == 5` | `true` |
| `===` | Identico (sem coercao) | `"5" === 5` | `false` |
| `!=` | Diferente (com coercao) | `"5" != 5` | `false` |
| `!==` | Nao identico | `"5" !== 5` | `true` |
| `>` | Maior que | `10 > 5` | `true` |
| `<` | Menor que | `3 < 2` | `false` |
| `>=` | Maior ou igual | `5 >= 5` | `true` |
| `<=` | Menor ou igual | `4 <= 3` | `false` |

> Prefira sempre `===` e `!==` para evitar resultados inesperados com coercao de tipo.

## Operadores logicos

```js
const a = true;
const b = false;

console.log(a && b); // false — E logico
console.log(a || b); // true  — OU logico
console.log(!a);     // false — negacao
```

## Condicional `if / else`

```js
const nota = 7;

if (nota >= 7) {
  console.log("Aprovado");
} else if (nota >= 5) {
  console.log("Recuperacao");
} else {
  console.log("Reprovado");
}
```

## Operador ternario

```js
const hora = 14;
const periodo = hora < 12 ? "manha" : "tarde";
console.log(periodo); // tarde
```

## `switch`

```js
const dia = "segunda";

switch (dia) {
  case "segunda":
    console.log("Inicio da semana");
    break;
  case "sexta":
    console.log("Quase fim de semana");
    break;
  default:
    console.log("Dia comum");
}
```

> Nao esquecer o `break` em cada `case`, ou a execucao continua para o proximo.

## Pratica sugerida (exercicio concreto)
### Projeto: Classificador de IMC

### Requisitos obrigatorios
1. Declare `const peso` e `const altura` com valores numericos.
2. Calcule o IMC: `peso / (altura * altura)`.
3. Use `if/else if/else` para classificar: abaixo do peso (`< 18.5`), normal (`18.5–24.9`), sobrepeso (`25–29.9`), obesidade (`>= 30`).
4. Exiba o IMC calculado e a classificacao com `console.log`.
5. Reescreva a classificacao usando o operador ternario (pode ser aninhado).

### Entrega esperada
- Arquivo `imc.js` vinculado a um `index.html`.

## Desafio opcional
Implemente um `switch` que, dado um numero de 1 a 7, exiba o dia da semana correspondente. Trate o caso de numeros fora do intervalo com `default`.

## Navegacao
- [Aula anterior: JavaScript (parte 2) - Variaveis e constantes](../javascript-parte-2-variaveis-e-constantes/)
- [Voltar para JavaScript](../../)
- [Proxima aula: JavaScript (parte 4) - Objeto window](../../etapa-2/javascript-parte-4-objeto-window/)
