# JavaScript (parte 1) - Overview

> Modulo: JavaScript

## Objetivo da aula
Entender o que e JavaScript, como ele funciona no navegador, onde e inserido no HTML e quais sao suas principais caracteristicas como linguagem.

## Exemplo rapido
```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <title>Primeiro JS</title>
</head>
<body>
  <h1>Ola, mundo!</h1>

  <script>
    console.log("JavaScript funcionando!");
    alert("Bem-vindo ao JavaScript!");
  </script>
</body>
</html>
```

## O que e JavaScript

JavaScript e uma linguagem de programacao interpretada, de tipagem dinamica e fraca, executada diretamente pelo navegador (client-side) sem necessidade de compilacao.

| Caracteristica | Descricao |
|----------------|-----------|
| Interpretada | Executada linha a linha pelo motor do navegador (V8, SpiderMonkey...) |
| Dinamica | Tipos de variaveis sao definidos em tempo de execucao |
| Orientada a eventos | Responde a acoes do usuario (cliques, teclas, scroll...) |
| Multiparadigma | Suporta imperativo, funcional e orientado a objetos |

## Como inserir JavaScript no HTML

### Inline (dentro da tag `<script>`)
```html
<script>
  console.log("inline");
</script>
```

### Arquivo externo (recomendado)
```html
<script src="script.js"></script>
```

> A tag `<script>` deve ser colocada antes do fechamento do `</body>` para garantir que o HTML ja foi carregado antes da execucao.

## Console do navegador

O `console` e a principal ferramenta de debug no navegador.

```js
console.log("mensagem comum");
console.warn("aviso");
console.error("erro");
console.table([1, 2, 3]);
```

Para abrir o console: `F12` → aba **Console**.

## Diferencas em relacao ao PHP

| Aspecto | PHP | JavaScript |
|---------|-----|------------|
| Onde executa | Servidor | Navegador (ou Node.js) |
| Saida | Terminal / HTML | Console / DOM |
| Variaveis | `$nome` | `let nome` / `const nome` |
| Tipagem | Dinamica | Dinamica |

## Pratica sugerida (exercicio concreto)
### Projeto: Pagina de apresentacao com console

### Requisitos obrigatorios
1. Crie um arquivo `index.html` com estrutura HTML basica.
2. Adicione uma tag `<h1>` com seu nome.
3. Crie um arquivo `script.js` externo e vincule ao HTML com `<script src>`.
4. No `script.js`, use `console.log` para exibir: seu nome, sua idade e a frase `"JavaScript carregado com sucesso!"`.
5. Use `console.warn` para exibir uma mensagem de aviso qualquer.

### Entrega esperada
- Arquivos `index.html` e `script.js` na pasta da aula.

## Desafio opcional
Pesquise e use `console.table` para exibir um array com tres nomes. Observe a diferenca de formatacao em relacao ao `console.log`.

## Navegacao
- [Voltar para JavaScript](../../)
- [Proxima aula: JavaScript (parte 2) - Variaveis e constantes](../javascript-parte-2-variaveis-e-constantes/)
