# MySQL e SQL (parte 3) - Atribuindo comentarios e valores padrao as colunas

> Modulo: Banco de dados relacional

## Objetivo da aula
Usar `DEFAULT` para definir valores automaticos, adicionar `COMMENT` para documentar colunas, e modificar tabelas existentes com `ALTER TABLE`.

## Exemplo rapido
```sql
CREATE TABLE pedidos (
    id         INT           NOT NULL AUTO_INCREMENT,
    status     VARCHAR(20)   NOT NULL DEFAULT 'pendente' COMMENT 'Status atual do pedido',
    criado_em  DATETIME      NOT NULL DEFAULT CURRENT_TIMESTAMP,
    PRIMARY KEY (id)
);
```

## DEFAULT — valores padrao

`DEFAULT` define o valor que sera inserido automaticamente quando a coluna nao for informada no `INSERT`.

```sql
CREATE TABLE usuarios (
    id        INT          NOT NULL AUTO_INCREMENT,
    nome      VARCHAR(150) NOT NULL,
    ativo     BOOLEAN      NOT NULL DEFAULT TRUE,
    criado_em DATETIME     NOT NULL DEFAULT CURRENT_TIMESTAMP,
    cargo     VARCHAR(50)           DEFAULT 'visitante',
    PRIMARY KEY (id)
);
```

| Valor DEFAULT util | Descricao |
|--------------------|-----------|
| `TRUE` / `FALSE` | Para colunas booleanas de controle |
| `CURRENT_TIMESTAMP` | Registra automaticamente a data/hora de criacao |
| `0` | Para contadores e saldos iniciais |
| `'pendente'` | Para colunas de status |

## COMMENT — documentando colunas

`COMMENT` adiciona uma descricao legivel a uma coluna. Ela nao afeta o comportamento do banco, mas fica visivel ao inspecionar a tabela.

```sql
CREATE TABLE produtos (
    id     INT           NOT NULL AUTO_INCREMENT COMMENT 'Identificador unico do produto',
    nome   VARCHAR(100)  NOT NULL COMMENT 'Nome de exibicao na vitrine',
    estoque INT          NOT NULL DEFAULT 0 COMMENT 'Quantidade disponivel no deposito',
    PRIMARY KEY (id)
);
```

Para visualizar os comentarios:
```sql
SHOW CREATE TABLE produtos;
```

## ALTER TABLE — modificando tabelas existentes

`ALTER TABLE` permite alterar a estrutura de uma tabela ja criada sem recria-la.

### Adicionar uma coluna
```sql
ALTER TABLE usuarios
ADD COLUMN telefone VARCHAR(20) DEFAULT NULL COMMENT 'Telefone de contato';
```

### Modificar uma coluna existente
```sql
ALTER TABLE usuarios
MODIFY COLUMN cargo VARCHAR(80) NOT NULL DEFAULT 'colaborador' COMMENT 'Cargo atual';
```

### Renomear uma coluna
```sql
ALTER TABLE usuarios
RENAME COLUMN cargo TO funcao;
```

### Remover uma coluna
```sql
ALTER TABLE usuarios
DROP COLUMN telefone;
```

### Adicionar um valor DEFAULT a uma coluna existente
```sql
ALTER TABLE pedidos
ALTER COLUMN status SET DEFAULT 'aguardando';
```

## Inspecionando a estrutura atual

```sql
-- Resumo das colunas
DESC usuarios;

-- Script completo de criacao (inclui COMMENT e DEFAULT)
SHOW CREATE TABLE usuarios;
```

## Pratica sugerida (exercicio concreto)
### Projeto: Refinamento da tabela de livros (via Workbench)

### Requisitos obrigatorios
1. Usando o banco `biblioteca_db` da aula anterior, execute `ALTER TABLE` para:
   - Adicionar a coluna `cadastrado_em` do tipo `DATETIME` com `DEFAULT CURRENT_TIMESTAMP` e um `COMMENT` explicativo.
   - Adicionar a coluna `edicao` do tipo `INT` com `DEFAULT 1`.
2. Modifique a coluna `disponivel` para incluir um `COMMENT` com o texto `'TRUE = disponivel para emprestimo'`.
3. Execute `SHOW CREATE TABLE livros;` e leia o resultado completo.

### Entrega esperada
- Scripts `ALTER TABLE` utilizados e saida de `SHOW CREATE TABLE livros;`.

## Desafio opcional
Adicione a coluna `deletado_em` do tipo `DATETIME` com `DEFAULT NULL` e comentario `'Preenchido em exclusao logica'`. Pesquise o que e **soft delete** e escreva uma linha explicando o conceito em um comentario SQL.

## Navegacao
- [Aula anterior: MySQL e SQL (parte 2) - Criacao de bancos de dados e tabelas](../mysql-e-sql-parte-2-criacao-de-bancos-de-dados-e-tabelas/)
- [Voltar para Banco de dados relacional](../../)
- [Proxima aula: MySQL e SQL (parte 4) - CRUD](../../etapa-2/mysql-e-sql-parte-4-crud/)
