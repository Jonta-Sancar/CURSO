# JavaScript (parte 7) - Async

> Modulo: JavaScript

## Objetivo da aula
Entender o modelo assincrono do JavaScript, trabalhar com Promises e usar `async/await` para escrever codigo assincrono de forma legivel.

## Exemplo rapido
```js
async function buscarUsuario(id) {
  const resposta = await fetch(`https://jsonplaceholder.typicode.com/users/${id}`);
  const usuario = await resposta.json();
  console.log(usuario.name);
}

buscarUsuario(1);
```

## Por que JavaScript e assincrono

JavaScript e single-threaded — executa uma instrucao por vez. Operacoes lentas (requisicoes de rede, leitura de arquivos) nao podem bloquear a thread principal. O modelo assincrono permite que essas operacoes sejam iniciadas e concluidas em segundo plano.

## Callback (forma antiga)

```js
setTimeout(() => {
  console.log("Executado apos 1 segundo");
}, 1000);

console.log("Isso aparece primeiro");
```

## Promise

Uma `Promise` representa uma operacao que sera concluida no futuro. Pode ser resolvida (`fulfilled`) ou rejeitada (`rejected`).

```js
const promessa = new Promise((resolve, reject) => {
  const sucesso = true;

  if (sucesso) {
    resolve("Operacao concluida!");
  } else {
    reject("Algo deu errado.");
  }
});

promessa
  .then(resultado => console.log(resultado))
  .catch(erro => console.error(erro));
```

## `async / await`

`async/await` e uma sintaxe sobre Promises que torna o codigo mais linear e legivel.

```js
function esperar(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

async function principal() {
  console.log("Inicio");
  await esperar(2000);
  console.log("Apos 2 segundos");
}

principal();
```

## Tratando erros com `try/catch`

```js
async function carregarDados() {
  try {
    const resposta = await fetch("https://jsonplaceholder.typicode.com/posts/1");
    const dados = await resposta.json();
    console.log(dados.title);
  } catch (erro) {
    console.error("Falha ao carregar:", erro.message);
  }
}

carregarDados();
```

## `Promise.all` — execucao paralela

```js
async function carregarTudo() {
  const [usuarios, posts] = await Promise.all([
    fetch("https://jsonplaceholder.typicode.com/users").then(r => r.json()),
    fetch("https://jsonplaceholder.typicode.com/posts").then(r => r.json()),
  ]);

  console.log(usuarios.length, posts.length);
}

carregarTudo();
```

> Use `Promise.all` quando as requisicoes sao independentes entre si — elas executam em paralelo, reduzindo o tempo total.

## Pratica sugerida (exercicio concreto)
### Projeto: Exibidor de post da API

### Requisitos obrigatorios
1. Crie um `index.html` com um `<input type="number">` e um botao "Buscar Post".
2. Ao clicar, use `fetch` com `async/await` para buscar o post correspondente em `https://jsonplaceholder.typicode.com/posts/{id}`.
3. Exiba o titulo e o corpo do post em um `<div>` na pagina.
4. Trate erros: se o ID nao existir ou a requisicao falhar, exiba uma mensagem de erro.
5. Enquanto carrega, exiba um texto "Carregando..." no lugar do resultado.

### Entrega esperada
- Arquivos `index.html` e `script.js` na pasta da aula.

## Desafio opcional
Use `Promise.all` para buscar simultaneamente o post e o usuario correspondente (campo `userId` do post), exibindo o titulo do post e o nome do autor juntos na tela.

## Navegacao
- [Aula anterior: JavaScript (parte 6) - Dataset](../../etapa-2/javascript-parte-6-dataset-propriedades-personalizadas/)
- [Voltar para JavaScript](../../)
- [Proxima aula: JavaScript (parte 8) - Ajax](../javascript-parte-8-ajax/)
