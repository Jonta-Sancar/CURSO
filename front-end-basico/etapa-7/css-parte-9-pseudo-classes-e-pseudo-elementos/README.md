# CSS (parte 9) - pseudo-classes e pseudo-elementos

> Modulo: Front-end Basico

## Objetivo da aula
Interacoes de estado e estilizacao de partes especificas dos elementos.

## Exemplo rapido
```css
.botao:hover {
  background: #0a9396;
}

.titulo::after {
  content: "";
  display: block;
  width: 56px;
  border-bottom: 3px solid #0a9396;
}
```

## Pratica sugerida (exercicio concreto)
### Projeto: Lista de tarefas interativa (visual)

### Requisitos obrigatorios
1. Crie uma lista com 8 tarefas e um botao "Adicionar tarefa".
2. Use `:hover` e `:active` no botao.
3. Use `:nth-child` para alternar cor de fundo dos itens.
4. Use `::before` para inserir um icone textual antes de cada tarefa.
5. Use `::after` em um titulo de secao para criar detalhe visual.

### Regras de validacao
- Estados de interacao devem ser perceptiveis.
- Pseudo-elementos devem usar `content`.
- Alternancia de linhas deve funcionar em toda a lista.
- Evitar excesso de efeitos que prejudiquem leitura.

### Entrega esperada
- Arquivo(s) HTML e CSS organizados em pasta unica da aula.
- Estrutura legivel, com nomes claros e sem conteudo placeholder.
## Navegacao
- [Voltar para Front-end Basico](../../)
