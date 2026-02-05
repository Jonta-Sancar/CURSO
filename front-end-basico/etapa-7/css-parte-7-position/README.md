# CSS (parte 7) - position

> Modulo: Front-end Basico

## Objetivo da aula
Controle de posicionamento com static, relative, absolute, fixed e sticky.

## Exemplo rapido
```css
.aviso {
  position: fixed;
  right: 16px;
  bottom: 16px;
}
```

## Pratica sugerida (exercicio concreto)
### Projeto: Pagina com elementos posicionados

### Requisitos obrigatorios
1. Crie um cabecalho com `position: sticky` no topo.
2. Monte um card com selo no canto usando `relative` + `absolute`.
3. Adicione um botao flutuante de ajuda com `position: fixed`.
4. Inclua um exemplo de elemento `static` e descreva o comportamento.
5. Organize secoes suficientes para gerar rolagem vertical.

### Regras de validacao
- Sticky deve funcionar durante a rolagem.
- Elemento absoluto deve respeitar o pai relativo.
- Botao fixo nao pode cobrir texto principal.
- Evitar usar `top/left` sem necessidade em elementos estaticos.

### Entrega esperada
- Arquivo(s) HTML e CSS organizados em pasta unica da aula.
- Estrutura legivel, com nomes claros e sem conteudo placeholder.
## Navegacao
- [Voltar para Front-end Basico](../../)
