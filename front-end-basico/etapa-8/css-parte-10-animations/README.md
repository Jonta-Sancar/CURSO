# CSS (parte 10) - Animations

> Modulo: Front-end Basico

## Objetivo da aula
Animacoes com transition e @keyframes para feedback visual e destaque.

## Exemplo rapido
```css
.card {
  transition: transform 0.25s ease;
}

.card:hover {
  transform: translateY(-4px);
}
```

## Pratica sugerida (exercicio concreto)
### Projeto: Tela de cards com microinteracoes

### Requisitos obrigatorios
1. Crie 4 cards de curso com titulo e descricao.
2. Aplique `transition` em hover para elevar levemente o card.
3. Crie uma animacao com `@keyframes` para entrada do titulo da pagina.
4. Configure duracao e timing function diferentes para hover e entrada.
5. Garanta que animacoes nao prejudiquem legibilidade.

### Regras de validacao
- Hover deve responder de forma suave.
- Animacao de entrada deve ocorrer apenas no carregamento.
- Nao usar tempos longos (acima de 1.2s) sem justificativa.
- Nao esconder conteudo essencial durante a animacao.

### Entrega esperada
- Arquivo(s) HTML e CSS organizados em pasta unica da aula.
- Estrutura legivel, com nomes claros e sem conteudo placeholder.
## Navegacao
- [Voltar para Front-end Basico](../../)
