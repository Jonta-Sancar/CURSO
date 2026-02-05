# HTML (parte 4) - Formularios

> Modulo: Front-end Basico

## Objetivo da aula
Construcao de formularios com campos, validacao nativa e envio de dados.

## Estrutura base de formulario
```html
<form action="#" method="post">
  <fieldset>
    <legend>Cadastro</legend>

    <label for="nome">Nome completo</label>
    <input id="nome" name="nome" type="text" required>

    <button type="submit">Enviar</button>
  </fieldset>
</form>
```

## Principais tipos de `input` (com sintaxe)
```html
<input type="text" name="nome" placeholder="Seu nome">
<input type="email" name="email" placeholder="voce@exemplo.com">
<input type="password" name="senha" minlength="8">
<input type="number" name="idade" min="14" max="120">
<input type="date" name="nascimento">
<input type="time" name="horario">
<input type="tel" name="telefone" pattern="[0-9]{10,11}">
<input type="url" name="portfolio" placeholder="https://...">
<input type="file" name="curriculo">
<input type="checkbox" name="aceite" required>
<input type="radio" name="turno" value="manha">
<input type="range" name="nivel" min="0" max="10" step="1">
<input type="color" name="cor_favorita">
<input type="hidden" name="origem" value="landing-page">
```

## Propriedades auxiliares importantes
- `placeholder`: dica visual do preenchimento esperado.
- `required`: torna o campo obrigatorio.
- `min` e `max`: limites numericos/data.
- `minlength` e `maxlength`: limite minimo/maximo de caracteres.
- `step`: passo de incremento (ex.: `0.5` em valores decimais).
- `pattern`: regex simples para validar formato.
- `value`: valor inicial do campo.
- `checked`: marca `checkbox`/`radio` por padrao.
- `readonly`: permite leitura, bloqueia edicao.
- `disabled`: desabilita o campo (nao envia no submit).
- `autocomplete`: ajuda preenchimento automatico.

## `textarea`, `select` e `datalist`
```html
<label for="mensagem">Mensagem</label>
<textarea id="mensagem" name="mensagem" rows="4" cols="40" maxlength="300" placeholder="Escreva sua mensagem"></textarea>

<label for="trilha">Trilha de interesse</label>
<select id="trilha" name="trilha" required>
  <option value="">Selecione</option>
  <option value="frontend">Front-end</option>
  <option value="backend">Back-end</option>
  <option value="fullstack">Full Stack</option>
</select>

<label for="cidade">Cidade</label>
<input id="cidade" name="cidade" list="lista-cidades" placeholder="Digite e escolha">
<datalist id="lista-cidades">
  <option value="Sao Paulo"></option>
  <option value="Rio de Janeiro"></option>
  <option value="Belo Horizonte"></option>
</datalist>
```

## Exemplo completo
```html
<form action="#" method="post">
  <fieldset>
    <legend>Inscricao no workshop</legend>

    <label for="nome">Nome completo</label>
    <input id="nome" name="nome" type="text" placeholder="Seu nome completo" required>

    <label for="email">Email</label>
    <input id="email" name="email" type="email" placeholder="voce@exemplo.com" required>

    <label for="idade">Idade</label>
    <input id="idade" name="idade" type="number" min="14" max="80" step="1" required>

    <label for="telefone">Telefone</label>
    <input id="telefone" name="telefone" type="tel" pattern="[0-9]{10,11}" placeholder="11999999999">

    <p>Turno preferido</p>
    <label><input type="radio" name="turno" value="manha" checked> Manha</label>
    <label><input type="radio" name="turno" value="noite"> Noite</label>

    <label><input type="checkbox" name="aceite" required> Aceito os termos</label>

    <label for="objetivo">Objetivo com o curso</label>
    <textarea id="objetivo" name="objetivo" rows="5" maxlength="400"></textarea>

    <label for="trilha">Trilha</label>
    <select id="trilha" name="trilha" required>
      <option value="">Selecione</option>
      <option value="frontend">Front-end</option>
      <option value="backend">Back-end</option>
      <option value="fullstack">Full Stack</option>
    </select>

    <label for="cidade">Cidade</label>
    <input id="cidade" name="cidade" list="cidades">
    <datalist id="cidades">
      <option value="Recife"></option>
      <option value="Salvador"></option>
      <option value="Fortaleza"></option>
    </datalist>

    <button type="submit">Enviar inscricao</button>
    <button type="reset">Limpar formulario</button>
  </fieldset>
</form>
```

## Pratica sugerida (exercicio concreto)
### Projeto: Formulario de inscricao para workshop

### Requisitos obrigatorios
1. Monte um formulario com: nome, email, telefone, data de nascimento e area de interesse.
2. Use `label` associado com `for` + `id` para todos os campos.
3. Adicione pelo menos 1 grupo de opcoes com `radio` e 1 com `checkbox`.
4. Inclua `textarea`, `select` e `datalist`.
5. Use no minimo 6 propriedades auxiliares (`required`, `placeholder`, `min`, `max`, `maxlength`, `pattern`, etc.).
6. Finalize com botoes de enviar e limpar (`submit` e `reset`).

### Regras de validacao
- Campos nome e email devem ser obrigatorios (`required`).
- Email deve usar `type="email"`.
- Telefone deve usar um `pattern` simples (ex.: somente numeros).
- Pelo menos 1 campo numerico deve usar `min` e `max`.
- `select` deve ter opcao inicial vazia (ex.: "Selecione").
- `textarea` deve ter limite com `maxlength`.
- Botao de envio deve funcionar com Enter no campo.

### Entrega esperada
- Arquivo `index.html` organizado na pasta da aula.
- Estrutura legivel, com nomes claros e sem conteudo placeholder generico.
## Navegacao
- [Voltar para Front-end Basico](../../)
