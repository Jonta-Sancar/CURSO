# JavaScript (parte 4) - Objeto window: caracteristicas, principais eventos e utilizacoes

> Modulo: JavaScript

## Objetivo da aula
Entender o objeto global `window` no navegador, suas propriedades e metodos mais usados, e responder a eventos do documento.

## Exemplo rapido
```js
console.log(window.innerWidth);  // largura da janela
console.log(window.location.href); // URL atual

window.addEventListener("load", () => {
  console.log("Pagina carregada!");
});
```

## O objeto `window`

`window` e o objeto global do navegador. Todas as variaveis e funcoes declaradas no escopo global pertencem a ele.

```js
var mensagem = "ola";
console.log(window.mensagem); // ola

function saudar() { return "oi"; }
console.log(window.saudar()); // oi
```

## Propriedades uteis

| Propriedade | Descricao |
|-------------|-----------|
| `window.innerWidth` | Largura visivel da janela em pixels |
| `window.innerHeight` | Altura visivel da janela em pixels |
| `window.location.href` | URL da pagina atual |
| `window.location.reload()` | Recarrega a pagina |
| `window.navigator.userAgent` | Informacoes do navegador |
| `window.document` | Referencia ao documento HTML (DOM) |

## Metodos de dialogo

```js
alert("Mensagem ao usuario");

const confirmado = confirm("Tem certeza?");
console.log(confirmado); // true ou false

const nome = prompt("Qual e o seu nome?");
console.log(nome); // valor digitado ou null
```

> Em producao, evite `alert/confirm/prompt` — eles bloqueiam a thread. Use elementos HTML customizados no lugar.

## Eventos do `window`

```js
window.addEventListener("load", () => {
  console.log("DOM e recursos carregados");
});

window.addEventListener("resize", () => {
  console.log(`Janela: ${window.innerWidth}x${window.innerHeight}`);
});

window.addEventListener("scroll", () => {
  console.log(`Scroll Y: ${window.scrollY}`);
});
```

## `setTimeout` e `setInterval`

```js
// executa uma vez apos 2 segundos
setTimeout(() => {
  console.log("Executado apos 2s");
}, 2000);

// executa a cada 1 segundo
const intervalo = setInterval(() => {
  console.log("tick");
}, 1000);

// para o intervalo apos 5 segundos
setTimeout(() => clearInterval(intervalo), 5000);
```

## Pratica sugerida (exercicio concreto)
### Projeto: Painel de informacoes da janela

### Requisitos obrigatorios
1. Crie um `index.html` com um `<div id="info">`.
2. No `script.js`, ao carregar a pagina (`window.addEventListener("load")`), exiba dentro do `<div>` as seguintes informacoes: largura e altura da janela, URL atual e user agent.
3. Adicione um listener de `resize` que atualiza os valores de largura e altura em tempo real.
4. Adicione um botao "Recarregar" que chama `window.location.reload()`.

### Entrega esperada
- Arquivos `index.html` e `script.js` na pasta da aula.

## Desafio opcional
Use `setInterval` para exibir um contador regressivo de 10 a 0 no console, parando automaticamente ao chegar em zero com `clearInterval`.

## Navegacao
- [Aula anterior: JavaScript (parte 3) - Operadores e verificadores condicionais](../../etapa-1/javascript-parte-3-operadores-e-verificadores-condicionais/)
- [Voltar para JavaScript](../../)
- [Proxima aula: JavaScript (parte 5) - Manipulando elementos da pagina](../javascript-parte-5-manipulando-elementos-da-pagina/)
