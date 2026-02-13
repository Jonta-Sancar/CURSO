# HTML (parte 3) - Tabelas

> Modulo: Front-end Basico

## Objetivo da aula
Criacao de tabelas semanticas com cabecalho, corpo e boas praticas de acessibilidade.

## Exemplo rapido
```html
<table>
  <caption>Horario de aulas</caption>
  <thead>
    <tr>
      <th>Dia</th>
      <th>Horario</th>
      <th>Tema</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Segunda</td>
      <td>19:00</td>
      <td>HTML</td>
    </tr>
  </tbody>
</table>
```

## Pratica sugerida (exercicio concreto)
### Projeto: Boletim de notas de uma turma

### Requisitos obrigatorios
1. Crie uma tabela com `caption`, `thead` e `tbody`.
2. No cabecalho, use 5 colunas: Aluno, Modulo 1, Modulo 2, Modulo 3 e Media.
3. Cadastre pelo menos 6 alunos (6 linhas no corpo).
4. Preencha notas numericas e calcule a media manualmente antes de inserir.
5. Use uma ultima linha para resumo com a media geral da turma.
6. **IMPORTANTE:** Utilize as tags semânticas `thead`, `tbody` e `tfoot`

### Regras de validacao
- Todo cabecalho deve usar `th` (nao `td`).
- A tabela deve ser legivel sem qualquer estilizacao.
- Nao deixar celulas vazias.
- Usar valores de nota coerentes (0 a 10).

### Entrega esperada
- Arquivo `index.html` organizado na pasta da aula.
- Estrutura legivel, com nomes claros e sem conteudo placeholder.
## Navegacao
- [Voltar para Front-end Basico](../../)
