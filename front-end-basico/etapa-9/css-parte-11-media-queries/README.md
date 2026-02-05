# CSS (parte 11) - Media Queries

> Modulo: Front-end Basico

## Objetivo da aula
Adaptacao de layout para dispositivos diferentes com breakpoints.

## Exemplo rapido
```css
@media (max-width: 768px) {
  .cards {
    grid-template-columns: 1fr;
  }
}
```

## Pratica sugerida (exercicio concreto)
### Projeto: Pagina de servicos responsiva

### Requisitos obrigatorios
1. Monte uma pagina com cabecalho, bloco de servicos (3 cards) e rodape.
2. Crie layout desktop primeiro (largura ampla).
3. Adicione ao menos 2 breakpoints: tablet e mobile.
4. No mobile, empilhe cards e ajuste tamanhos de fonte/titulo.
5. Teste manualmente em largura de 1200px, 768px e 375px.

### Regras de validacao
- Nao deve haver rolagem horizontal em 375px.
- Textos devem permanecer legiveis em todos os tamanhos.
- Cards nao podem ficar espremidos no tablet.
- Breakpoints devem ter objetivo claro (nao aleatorios).

### Entrega esperada
- Arquivo(s) HTML e CSS organizados em pasta unica da aula.
- Estrutura legivel, com nomes claros e sem conteudo placeholder.
## Navegacao
- [Voltar para Front-end Basico](../../)
