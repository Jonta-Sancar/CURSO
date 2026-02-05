# CSS (parte 4) - CSS Variaveis

> Modulo: Front-end Basico

## Objetivo da aula
Uso de custom properties para reaproveitamento, temas e manutencao de estilos.

## Exemplo rapido
```css
:root {
  --cor-primaria: #0b7285;
  --espacamento: 16px;
}
```

## Pratica sugerida (exercicio concreto)
### Projeto: Mini design system de pagina institucional

### Requisitos obrigatorios
1. Declare no `:root` variaveis para: 2 cores, 2 tamanhos de fonte e 2 espacamentos.
2. Use essas variaveis em pelo menos 4 componentes (header, botao, card, footer).
3. Crie uma classe `.tema-escuro` sobrescrevendo apenas as variaveis de cor.
4. Aplique a classe no `body` para simular troca de tema.
5. Evite valores fixos repetidos fora das variaveis.

### Regras de validacao
- Variaveis devem ter nomes claros e consistentes.
- Tema escuro deve alterar visual sem trocar todas as regras.
- A pagina deve continuar legivel nos dois temas.
- Nao duplicar blocos de estilo inteiros desnecessariamente.

### Entrega esperada
- Arquivo(s) HTML e CSS organizados em pasta unica da aula.
- Estrutura legivel, com nomes claros e sem conteudo placeholder.
## Navegacao
- [Voltar para Front-end Basico](../../)
