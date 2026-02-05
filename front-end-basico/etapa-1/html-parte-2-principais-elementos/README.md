# HTML (parte 2) - Principais Elementos

> Modulo: Front-end Basico

## Objetivo da aula
Uso dos elementos mais comuns para texto, links, imagens e organizacao de conteudo.

## Vocabulario com sintaxe e aplicacao pratica

```html
<!-- Titulos e texto -->
<h1>Titulo principal da pagina</h1>
<h2>Subtitulo da secao</h2>
<p>Este paragrafo explica o conteudo da aula.</p>

<!-- Link -->
<a href="https://coude-escola.github.io/docs/">Abrir documentacao</a>

<!-- Imagem -->
<img src="assets/logo.png" alt="Logo do projeto">

<!-- Lista nao ordenada -->
<ul>
  <li>HTML</li>
  <li>CSS</li>
  <li>JavaScript</li>
</ul>

<!-- Lista ordenada -->
<ol>
  <li>Estudar conceito</li>
  <li>Reproduzir exemplo</li>
  <li>Praticar sozinho</li>
</ol>

<!-- Agrupamento -->
<div class="card-aula">
  <h3>Card da aula</h3>
  <p>Resumo rapido do topico.</p>
</div>

<!-- Conteudo em linha -->
<p>Aprenda <span>um passo por vez</span> para evoluir com consistencia.</p>
```

## Tags principais
- `<h1>` a `<h6>`: definem hierarquia de titulos.
- `<p>`: representa paragrafos de texto.
- `<a>`: cria links com `href`.
- `<img>`: insere imagens com `src` e `alt`.
- `<ul>`: lista com marcadores.
- `<ol>`: lista numerada.
- `<li>`: item de lista (usado dentro de `ul` ou `ol`).
- `<div>`: agrupador em bloco para organizar layout.
- `<span>`: agrupador em linha para destacar partes pequenas do texto.

## Exemplo pratico completo
```html
<section>
  <h2>Trilha Front-end Basico</h2>
  <p>Veja os proximos passos para sua evolucao:</p>

  <ol>
    <li>Estrutura HTML</li>
    <li>Principais elementos</li>
    <li>Tabelas e formularios</li>
  </ol>

  <p>
    Material complementar:
    <a href="https://coude-escola.github.io/docs/">Acessar docs</a>
  </p>

  <img src="assets/trilha.png" alt="Mapa da trilha de estudos">
</section>
```

## Pratica sugerida (exercicio concreto)
### Projeto: Convite digital de evento
Crie uma pagina de convite digital usando HTML semantico. O objetivo e organizar informacoes reais de um evento de forma clara, sem usar CSS por enquanto.

### Requisitos obrigatorios
1. Use a estrutura base: `<!DOCTYPE html>`, `html`, `head` e `body`.
2. Monte um `header` com:
   - nome do evento;
   - frase curta de destaque;
   - data principal.
3. Crie pelo menos **3 secoes** no `main`:
   - **Sessao 1 - Sobre o evento:** descricao curta (2 paragrafos).
   - **Sessao 2 - Programacao:** lista ordenada com no minimo 4 atividades.
   - **Sessao 3 - Confirmacao:** instrucoes de confirmacao com um link (`a`) para contato.
4. Inclua pelo menos **1 imagem** relacionada ao evento com `alt` descritivo.
5. Finalize com `footer` contendo:
   - endereco completo do local;
   - nome do remetente/organizacao;
   - um meio de contato (email ou telefone em texto).

### Regras de validacao
- Use pelo menos estas tags: `header`, `main`, `section`, `h1`, `h2`, `p`, `ol`, `li`, `a`, `img`, `footer`.
- Nao repetir titulos vazios como \"Titulo aqui\".
- Todo link deve ter destino valido (`href` preenchido).
- Toda imagem deve ter `alt` com contexto.

### Entrega esperada
- Arquivo unico: `index.html`.
- O arquivo deve abrir no navegador com leitura clara de cima para baixo, sem depender de explicacao externa.

## Navegacao
- [Voltar para Front-end Basico](../../)
- [Aula anterior: HTML (parte 1) - Estrutura e funcionamento](../html-parte-1-estrutura-e-funcionamento/)
