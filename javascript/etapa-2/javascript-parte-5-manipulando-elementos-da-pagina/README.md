# JavaScript (parte 5) - Manipulando elementos da pagina

> Modulo: JavaScript

## Objetivo da aula
Selecionar elementos HTML via JavaScript, alterar seu conteudo, estilos e classes, e responder a eventos do usuario.

## Exemplo rapido
```html
<button id="btn">Clique aqui</button>
<p id="mensagem"></p>
```
```js
const btn = document.querySelector("#btn");
const mensagem = document.querySelector("#mensagem");

btn.addEventListener("click", () => {
  mensagem.textContent = "Voce clicou!";
});
```

## Selecionando elementos

```js
// Seleciona o primeiro elemento que corresponde ao seletor CSS
const titulo = document.querySelector("h1");
const caixa = document.querySelector(".caixa");
const campo = document.querySelector("#email");

// Seleciona todos os elementos correspondentes (retorna NodeList)
const itens = document.querySelectorAll("li");
itens.forEach(item => console.log(item.textContent));
```

> `querySelector` e `querySelectorAll` aceitam qualquer seletor CSS valido.

## Lendo e escrevendo conteudo

```js
const paragrafo = document.querySelector("p");

// ler
console.log(paragrafo.textContent); // texto puro
console.log(paragrafo.innerHTML);   // HTML interno

// escrever
paragrafo.textContent = "Novo texto";
paragrafo.innerHTML = "<strong>Negrito</strong>";
```

## Manipulando atributos

```js
const link = document.querySelector("a");

link.getAttribute("href");           // le o atributo
link.setAttribute("href", "/novo");  // define o atributo
link.removeAttribute("target");      // remove o atributo
```

## Manipulando estilos e classes

```js
const caixa = document.querySelector(".caixa");

// estilo inline
caixa.style.backgroundColor = "blue";
caixa.style.fontSize = "20px";

// classes (preferivel ao estilo inline)
caixa.classList.add("ativo");
caixa.classList.remove("inativo");
caixa.classList.toggle("visivel");   // adiciona se nao tiver, remove se tiver
caixa.classList.contains("ativo");   // retorna true/false
```

## Eventos comuns

| Evento | Quando dispara |
|--------|---------------|
| `click` | Ao clicar no elemento |
| `input` | Ao digitar em um campo |
| `change` | Ao alterar e sair do campo |
| `submit` | Ao enviar um formulario |
| `mouseover` | Ao passar o mouse por cima |
| `keydown` | Ao pressionar uma tecla |

```js
const campo = document.querySelector("input");

campo.addEventListener("input", (event) => {
  console.log(event.target.value);
});
```

## Criando e inserindo elementos

```js
const lista = document.querySelector("ul");

const novoItem = document.createElement("li");
novoItem.textContent = "Novo item";
lista.appendChild(novoItem);
```

## Pratica sugerida (exercicio concreto)
### Projeto: Lista de tarefas simples

### Requisitos obrigatorios
1. Crie um `input` de texto e um botao "Adicionar".
2. Ao clicar no botao, pegue o valor do input e adicione um novo `<li>` a uma `<ul>`.
3. Limpe o input apos adicionar.
4. Cada `<li>` deve ter um botao "Remover" que, ao ser clicado, remove aquele item da lista.
5. Se o input estiver vazio ao clicar em "Adicionar", exiba uma mensagem de erro abaixo do input.

### Entrega esperada
- Arquivos `index.html`, `style.css` e `script.js` na pasta da aula.

## Desafio opcional
Adicione a funcionalidade de marcar tarefas como concluidas: ao clicar no texto do `<li>`, aplique/remova uma classe CSS que risca o texto (`text-decoration: line-through`).

## Navegacao
- [Aula anterior: JavaScript (parte 4) - Objeto window](../javascript-parte-4-objeto-window/)
- [Voltar para JavaScript](../../)
- [Proxima aula: JavaScript (parte 6) - Dataset](../javascript-parte-6-dataset-propriedades-personalizadas/)
