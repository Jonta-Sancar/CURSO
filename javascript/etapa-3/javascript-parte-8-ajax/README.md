# JavaScript (parte 8) - Ajax

> Modulo: JavaScript

## Objetivo da aula
Entender o que e Ajax, como usar `fetch` para comunicar com um servidor sem recarregar a pagina, e integrar dados externos ao DOM.

## Exemplo rapido
```js
fetch("/api/produtos")
  .then(resposta => resposta.json())
  .then(dados => console.log(dados))
  .catch(erro => console.error(erro));
```

## O que e Ajax

Ajax (Asynchronous JavaScript and XML) e a tecnica de fazer requisicoes HTTP em segundo plano, atualizando partes da pagina sem recarregamento completo. Hoje em dia usa-se JSON no lugar de XML.

## `fetch` — sintaxe completa

```js
fetch(url, opcoes)
  .then(resposta => {
    if (!resposta.ok) {
      throw new Error(`HTTP ${resposta.status}`);
    }
    return resposta.json();
  })
  .then(dados => console.log(dados))
  .catch(erro => console.error(erro));
```

## Metodos HTTP com `fetch`

### GET (buscar dados)
```js
async function buscar() {
  const resposta = await fetch("/api/usuarios");
  return resposta.json();
}
```

### POST (enviar dados)
```js
async function criar(dados) {
  const resposta = await fetch("/api/usuarios", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(dados),
  });
  return resposta.json();
}

criar({ nome: "Ana", email: "ana@email.com" });
```

### PUT (atualizar)
```js
async function atualizar(id, dados) {
  const resposta = await fetch(`/api/usuarios/${id}`, {
    method: "PUT",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(dados),
  });
  return resposta.json();
}
```

### DELETE (excluir)
```js
async function excluir(id) {
  await fetch(`/api/usuarios/${id}`, { method: "DELETE" });
}
```

## Verificando o status da resposta

```js
async function buscarComVerificacao(url) {
  const resposta = await fetch(url);

  if (resposta.status === 404) {
    console.error("Recurso nao encontrado");
    return null;
  }

  if (!resposta.ok) {
    throw new Error(`Erro ${resposta.status}: ${resposta.statusText}`);
  }

  return resposta.json();
}
```

## Enviando formulario via Ajax

```html
<form id="form-contato">
  <input name="nome" type="text" placeholder="Nome">
  <input name="email" type="email" placeholder="Email">
  <button type="submit">Enviar</button>
</form>
```
```js
const form = document.querySelector("#form-contato");

form.addEventListener("submit", async (event) => {
  event.preventDefault();

  const dados = {
    nome: form.nome.value,
    email: form.email.value,
  };

  try {
    const resposta = await fetch("/api/contato", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify(dados),
    });
    const resultado = await resposta.json();
    console.log("Enviado:", resultado);
  } catch (erro) {
    console.error("Falha no envio:", erro.message);
  }
});
```

## Pratica sugerida (exercicio concreto)
### Projeto: CRUD de posts via API publica

Use a API `https://jsonplaceholder.typicode.com/posts` (aceita GET, POST, PUT, DELETE).

### Requisitos obrigatorios
1. Liste os primeiros 10 posts ao carregar a pagina (GET).
2. Adicione um formulario para criar um novo post com titulo e corpo (POST). Exiba o objeto retornado no console.
3. Adicione um botao "Atualizar" em cada post que envia um PUT com o titulo modificado.
4. Adicione um botao "Excluir" em cada post que envia um DELETE e remove o item do DOM.
5. Trate erros em todas as operacoes com `try/catch`.

### Entrega esperada
- Arquivos `index.html` e `script.js` na pasta da aula.

## Desafio opcional
Adicione um indicador visual de carregamento (spinner ou texto "Carregando...") que aparece enquanto qualquer requisicao esta em andamento e desaparece quando ela conclui.

## Navegacao
- [Aula anterior: JavaScript (parte 7) - Async](../javascript-parte-7-async/)
- [Voltar para JavaScript](../../)
- [Proxima aula: JavaScript (parte 9) - Iteradores](../javascript-parte-9-iteradores-filter-map-foreach-reduce/)
