# HTML (parte 1) - Estrutura e funcionamento

> Modulo: Front-end Basico

## Objetivo da aula
Entender como um documento HTML e organizado e como o navegador interpreta essa estrutura.

## Visao geral da estrutura de uma pagina
```html
<!DOCTYPE html>
<html lang="pt-BR">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Minha primeira pagina</title>
  </head>
  <body>
    <h1>Ola, mundo!</h1>
    <p>Primeira pagina da e-apostila.</p>
  </body>
</html>
```

## Como funciona
- `<!DOCTYPE html>` indica HTML5.
- `<html>` envolve todo o documento.
- `<head>` guarda metadados, titulo e links de recursos.
- `<body>` contem o que aparece para o usuario.

## Estrutura basica dos elementos HTML
Em HTML, um elemento e formado por uma tag de abertura, conteudo e (na maioria dos casos) uma tag de fechamento.

### 1) Tags sem autofechamento (elementos com conteudo)
```html
<!-- sem propriedade -->
<tag>conteudo</tag>

<!-- com propriedade -->
<tag propriedade="valor">conteudo</tag>
```

Exemplos reais:
```html
<p>Este e um paragrafo.</p>
<a href="https://exemplo.com">Abrir site</a>
```

### 2) Tags autofechaveis (void elements)
No HTML, algumas tags nao possuem conteudo interno e nao usam fechamento.

```html
<!-- sem propriedade -->
<br>

<!-- com propriedade -->
<img src="foto.png" alt="Foto de exemplo">
```

> Observacao: nem toda tag pode ser autofechada.  
> `div`, `p`, `section`, `a` e varias outras precisam de abertura e fechamento.

## Regras rapidas sobre propriedades (atributos)
- Propriedades ficam na tag de abertura.
- Formato: `nome="valor"`.
- Um elemento pode ter varias propriedades.
- Exemplo: `<input type="email" name="contato" required>`

## Vocabulario essencial de tags HTML
- `<html>`: elemento raiz que envolve toda a pagina.
- `<head>`: area de configuracoes e metadados (nao aparece como conteudo principal).
- `<title>`: define o titulo da aba do navegador.
- `<body>`: area de conteudo visivel da pagina.
- `<h1>` ate `<h6>`: titulos e subtitulos em niveis de importancia.
- `<p>`: paragrafo de texto.
- `<a>`: cria links para outras paginas, secoes ou arquivos.
- `<img>`: exibe imagens.
- `<br>`: quebra de linha.
- `<hr>`: separador tematico (linha horizontal).
- `<ul>`: lista nao ordenada (com marcadores).
- `<ol>`: lista ordenada (numerada).
- `<li>`: item de lista.
- `<div>`: bloco generico para agrupar elementos.
- `<span>`: elemento generico em linha para pequenos trechos.
- `<section>`: secao tematica de conteudo.
- `<article>`: bloco de conteudo independente (post, noticia, card).
- `<header>`: cabecalho de pagina ou secao.
- `<main>`: conteudo principal da pagina.
- `<footer>`: rodape de pagina ou secao.

## Pratica sugerida (exercicio concreto)
### Projeto: Pagina de apresentacao pessoal
Crie uma pagina simples para se apresentar, focando na estrutura HTML correta (sem CSS por enquanto).

### Requisitos obrigatorios
1. Use a estrutura base completa: `<!DOCTYPE html>`, `html`, `head` e `body`.
2. No `head`, inclua:
   - `meta charset="UTF-8"`;
   - `meta name="viewport"`;
   - `title` com seu nome e o texto \"- Apresentacao\".
3. No `body`, organize o conteudo nesta ordem:
   - `h1` com seu nome;
   - 2 paragrafos (`p`) explicando quem voce e e o que esta estudando;
   - uma lista nao ordenada (`ul`) com 3 interesses seus;
   - um link (`a`) para seu GitHub, LinkedIn ou portfolio;
   - uma imagem (`img`) com `alt` descritivo.
4. Feche todas as tags corretamente e mantenha indentacao consistente.

### Regras de validacao
- O documento deve abrir sem erros visuais basicos no navegador.
- O `title` deve estar preenchido e coerente com a pagina.
- O link deve ter `href` valido.
- A imagem deve conter `alt` com descricao real.

### Entrega esperada
- Arquivo unico: `index.html`.
- Estrutura legivel e sem texto placeholder generico (ex.: \"lorem ipsum\").

## Desafio opcional
Adicione uma secao \"Meus objetivos nos proximos 3 meses\" com:
- subtitulo (`h2`);
- lista ordenada (`ol`) com 3 metas especificas.

## Navegacao
- [Voltar para Front-end Basico](../../)
- [Proxima aula: HTML (parte 2) - Principais Elementos](../html-parte-2-principais-elementos/)
