# CSS (parte 6) - Displays grid

> Modulo: Front-end Basico

## Objetivo da aula
Criacao de layouts bidimensionais com Grid para composicoes complexas.

## Exemplo rapido
```css
.layout {
  display: grid;
  grid-template-columns: 240px 1fr;
  gap: 16px;
}
```

## Pratica sugerida (exercicio concreto)
### Projeto: Dashboard simples com areas de Grid

### Requisitos obrigatorios
1. Monte um layout com: cabecalho, menu lateral, conteudo principal e rodape.
2. Use `grid-template-areas` para organizar as regioes.
3. No conteudo principal, crie uma sub-grade com 4 cards de metricas.
4. Defina `gap` consistente entre regioes e cards.
5. Inclua uma area de "alertas" ocupando 2 colunas da sub-grade.

### Regras de validacao
- Estrutura principal deve usar Grid (nao Flex para tudo).
- Areas precisam estar nomeadas e aplicadas corretamente.
- Sub-grade deve manter alinhamento entre cards.
- Layout deve continuar legivel em largura menor.

### Entrega esperada
- Arquivo(s) HTML e CSS organizados em pasta unica da aula.
- Estrutura legivel, com nomes claros e sem conteudo placeholder.
## Navegacao
- [Voltar para Front-end Basico](../../)
