# CSS (parte 8) - Overflow

> Modulo: Front-end Basico

## Objetivo da aula
Gerenciamento de conteudo que excede limites de largura e altura.

## Exemplo rapido
```css
.caixa-log {
  height: 140px;
  overflow-y: auto;
}
```

## Pratica sugerida (exercicio concreto)
### Projeto: Painel de mensagens com controle de overflow

### Requisitos obrigatorios
1. Crie 3 caixas com mesmo tamanho e muito texto interno.
2. Aplique `overflow: visible`, `hidden` e `auto` em cada caixa.
3. Crie uma quarta caixa horizontal com `overflow-x` para linha longa.
4. Inclua titulos para cada caixa indicando o tipo de overflow.
5. Adicione uma observacao curta sobre quando usar cada estrategia.

### Regras de validacao
- Diferencas entre os modos devem ser visiveis.
- Caixa com `auto` deve exibir barra de rolagem quando necessario.
- Nao usar alturas aleatorias sem contexto.
- Texto nao deve sumir sem explicacao da escolha.

### Entrega esperada
- Arquivo(s) HTML e CSS organizados em pasta unica da aula.
- Estrutura legivel, com nomes claros e sem conteudo placeholder.
## Navegacao
- [Voltar para Front-end Basico](../../)
