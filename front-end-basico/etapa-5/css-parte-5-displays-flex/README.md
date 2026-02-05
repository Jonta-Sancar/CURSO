# CSS (parte 5) - Displays flex

> Modulo: Front-end Basico

## Objetivo da aula
Montagem de layouts unidimensionais com Flexbox e alinhamentos eficientes.

## Exemplo rapido
```css
.menu {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
```

## Pratica sugerida (exercicio concreto)
### Projeto: Barra de navegacao + lista de cards com Flexbox

### Requisitos obrigatorios
1. Crie uma navbar com logo a esquerda e links a direita usando flex.
2. Abaixo, monte uma secao com 6 cards em linha e quebra para nova linha.
3. Use `gap` para espaco entre cards.
4. Centralize verticalmente o conteudo interno de cada card.
5. Teste pelo menos 2 variacoes de `justify-content` e registre qual ficou melhor.

### Regras de validacao
- Navbar deve alinhar itens sem gambiarras de margem manual.
- Cards devem quebrar linha com `flex-wrap`.
- Espacamento deve ser controlado principalmente por `gap`.
- Layout nao deve colapsar em largura media (tablet).

### Entrega esperada
- Arquivo(s) HTML e CSS organizados em pasta unica da aula.
- Estrutura legivel, com nomes claros e sem conteudo placeholder.
## Navegacao
- [Voltar para Front-end Basico](../../)
