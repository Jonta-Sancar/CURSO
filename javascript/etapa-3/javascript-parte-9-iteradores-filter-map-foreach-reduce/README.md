# JavaScript (parte 9) - Iteradores: filter, map, forEach, reduce

> Modulo: JavaScript

## Objetivo da aula
Usar os metodos de array `forEach`, `filter`, `map` e `reduce` para processar colecoes de dados de forma declarativa, sem loops manuais.

## Exemplo rapido
```js
const precos = [10, 25, 8, 50, 3];

const caros = precos.filter(p => p >= 10);
const dobrados = caros.map(p => p * 2);
const total = dobrados.reduce((acc, p) => acc + p, 0);

console.log(total); // 170
```

## `forEach` — iterar sem retorno

Executa uma funcao para cada elemento. Nao retorna nada.

```js
const nomes = ["Ana", "Bruno", "Carla"];

nomes.forEach((nome, indice) => {
  console.log(`${indice}: ${nome}`);
});
// 0: Ana
// 1: Bruno
// 2: Carla
```

## `filter` — filtrar elementos

Retorna um novo array com os elementos que passaram no teste.

```js
const idades = [15, 22, 17, 30, 12];

const maiores = idades.filter(idade => idade >= 18);
console.log(maiores); // [22, 30]
```

## `map` — transformar elementos

Retorna um novo array com cada elemento transformado pela funcao.

```js
const produtos = [
  { nome: "Caneta", preco: 2 },
  { nome: "Caderno", preco: 15 },
  { nome: "Mochila", preco: 80 },
];

const nomes = produtos.map(p => p.nome);
console.log(nomes); // ["Caneta", "Caderno", "Mochila"]

const comDesconto = produtos.map(p => ({ ...p, preco: p.preco * 0.9 }));
console.log(comDesconto);
```

## `reduce` — acumular em um unico valor

```js
const numeros = [1, 2, 3, 4, 5];

const soma = numeros.reduce((acumulador, atual) => acumulador + atual, 0);
console.log(soma); // 15

// Contando ocorrencias
const frutas = ["maca", "banana", "maca", "laranja", "banana", "maca"];

const contagem = frutas.reduce((acc, fruta) => {
  acc[fruta] = (acc[fruta] || 0) + 1;
  return acc;
}, {});

console.log(contagem); // { maca: 3, banana: 2, laranja: 1 }
```

## Encadeamento

Os metodos podem ser encadeados pois cada um retorna um array novo:

```js
const pedidos = [
  { produto: "Notebook", valor: 3500, pago: true },
  { produto: "Mouse", valor: 80, pago: false },
  { produto: "Teclado", valor: 200, pago: true },
  { produto: "Monitor", valor: 1200, pago: false },
];

const totalPago = pedidos
  .filter(p => p.pago)
  .map(p => p.valor)
  .reduce((acc, v) => acc + v, 0);

console.log(totalPago); // 3700
```

## Comparativo

| Metodo | Recebe | Retorna | Uso tipico |
|--------|--------|---------|------------|
| `forEach` | callback | `undefined` | Efeitos colaterais (exibir, salvar) |
| `filter` | predicado | novo array (subset) | Selecionar elementos |
| `map` | transformacao | novo array (mesmo tamanho) | Converter dados |
| `reduce` | acumulador | qualquer valor | Agregar, contar, agrupar |

## Pratica sugerida (exercicio concreto)
### Projeto: Relatorio de vendas

Dado o array abaixo:
```js
const vendas = [
  { vendedor: "Ana", produto: "Notebook", valor: 3500, mes: "janeiro" },
  { vendedor: "Bruno", produto: "Mouse", valor: 80, mes: "fevereiro" },
  { vendedor: "Ana", produto: "Teclado", valor: 200, mes: "janeiro" },
  { vendedor: "Carla", produto: "Monitor", valor: 1200, mes: "fevereiro" },
  { vendedor: "Bruno", produto: "Notebook", valor: 3500, mes: "janeiro" },
  { vendedor: "Carla", produto: "Headset", valor: 350, mes: "janeiro" },
];
```

### Requisitos obrigatorios
1. Use `filter` para obter apenas as vendas do mes de `"janeiro"`.
2. Use `map` para extrair apenas os valores das vendas de janeiro.
3. Use `reduce` para calcular o total vendido em janeiro.
4. Use `filter` + `reduce` para calcular o total vendido pela vendedora `"Ana"`.
5. Use `forEach` para exibir no console cada venda no formato: `"Ana vendeu Notebook por R$3500"`.

### Entrega esperada
- Arquivo `relatorio.js` vinculado a um `index.html`.

## Desafio opcional
Use `reduce` para agrupar as vendas por vendedor, resultando em um objeto onde a chave e o nome do vendedor e o valor e a soma total de suas vendas.

## Navegacao
- [Aula anterior: JavaScript (parte 8) - Ajax](../javascript-parte-8-ajax/)
- [Voltar para JavaScript](../../)
