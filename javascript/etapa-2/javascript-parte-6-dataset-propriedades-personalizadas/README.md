# JavaScript (parte 6) - Dataset (propriedades personalizadas)

> Modulo: JavaScript

## Objetivo da aula
Usar atributos `data-*` no HTML para armazenar dados diretamente nos elementos e acessar esses dados via JavaScript com a propriedade `dataset`.

## Exemplo rapido
```html
<button data-produto-id="42" data-nome="Teclado">Comprar</button>
```
```js
const btn = document.querySelector("button");

console.log(btn.dataset.produtoId); // "42"
console.log(btn.dataset.nome);      // "Teclado"
```

## O que sao atributos `data-*`

Atributos `data-*` permitem embutir dados customizados em qualquer elemento HTML sem afetar a renderizacao ou violar o padrao HTML.

```html
<ul>
  <li data-id="1" data-categoria="fruta">Maca</li>
  <li data-id="2" data-categoria="legume">Cenoura</li>
  <li data-id="3" data-categoria="fruta">Banana</li>
</ul>
```

## Lendo dados com `dataset`

```js
const item = document.querySelector("li");

console.log(item.dataset.id);        // "1"
console.log(item.dataset.categoria); // "fruta"
```

### Conversao de nomes (kebab-case → camelCase)

O navegador converte automaticamente o nome do atributo:

| Atributo HTML | Propriedade JS |
|---------------|----------------|
| `data-id` | `dataset.id` |
| `data-produto-id` | `dataset.produtoId` |
| `data-preco-total` | `dataset.precoTotal` |

## Escrevendo e removendo dados

```js
const item = document.querySelector("li");

// escrever
item.dataset.estoque = "10";

// remover
delete item.dataset.categoria;

// verificar existencia
console.log("id" in item.dataset); // true
```

## Caso de uso pratico: evento unico em multiplos botoes

Em vez de adicionar um listener para cada botao, use um unico listener no pai (event delegation):

```html
<div id="acoes">
  <button data-acao="editar" data-id="5">Editar</button>
  <button data-acao="excluir" data-id="5">Excluir</button>
</div>
```
```js
const acoes = document.querySelector("#acoes");

acoes.addEventListener("click", (event) => {
  const btn = event.target.closest("button");
  if (!btn) return;

  const { acao, id } = btn.dataset;
  console.log(`Acao: ${acao}, ID: ${id}`);
});
```

## Pratica sugerida (exercicio concreto)
### Projeto: Galeria de produtos com filtro

### Requisitos obrigatorios
1. Crie uma lista de pelo menos 6 produtos em HTML, cada `<li>` com `data-categoria` (ex: "eletronico", "roupa", "livro") e `data-preco`.
2. Adicione tres botoes de filtro: "Todos", "Eletronico", "Roupa".
3. Ao clicar em um filtro, mostre apenas os itens com a categoria correspondente (use `classList.toggle` ou manipule `style.display`).
4. Adicione um campo de busca que filtra por texto do produto em tempo real.

### Entrega esperada
- Arquivos `index.html`, `style.css` e `script.js` na pasta da aula.

## Desafio opcional
Adicione um botao "Ordenar por preco" que reordena os itens visiveis do menor para o maior preco usando o valor de `data-preco`.

## Navegacao
- [Aula anterior: JavaScript (parte 5) - Manipulando elementos da pagina](../javascript-parte-5-manipulando-elementos-da-pagina/)
- [Voltar para JavaScript](../../)
- [Proxima aula: JavaScript (parte 7) - Async](../../etapa-3/javascript-parte-7-async/)
