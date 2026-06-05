# MySQL e SQL (parte 6) - Cardinalidade entre tabelas

> Modulo: Banco de dados relacional

## Objetivo da aula
Entender os tipos de relacionamento entre tabelas (1:1, 1:N, N:N), implementar chaves estrangeiras com `FOREIGN KEY` e configurar o comportamento em cascata.

## Exemplo rapido
```sql
CREATE TABLE categorias (
    id   INT NOT NULL AUTO_INCREMENT,
    nome VARCHAR(80) NOT NULL,
    PRIMARY KEY (id)
);

CREATE TABLE produtos (
    id           INT NOT NULL AUTO_INCREMENT,
    nome         VARCHAR(100) NOT NULL,
    categoria_id INT NOT NULL,
    PRIMARY KEY (id),
    FOREIGN KEY (categoria_id) REFERENCES categorias(id)
);
```

---

## Cardinalidade

Cardinalidade descreve **quantos registros de uma tabela se relacionam com quantos registros de outra**.

| Tipo | Descricao | Exemplo |
|------|-----------|---------|
| 1:1 | Um registro se relaciona com exatamente um outro | Usuario tem um Perfil |
| 1:N | Um registro se relaciona com varios de outro | Categoria tem varios Produtos |
| N:N | Varios registros se relacionam com varios de outro | Alunos e Disciplinas |

---

## Relacionamento 1:N (mais comum)

Um registro da tabela pai referenciado por varios registros da tabela filho.

```sql
CREATE DATABASE catalogo_db;
USE catalogo_db;

CREATE TABLE categorias (
    id   INT         NOT NULL AUTO_INCREMENT,
    nome VARCHAR(80) NOT NULL,
    PRIMARY KEY (id)
);

CREATE TABLE produtos (
    id           INT           NOT NULL AUTO_INCREMENT,
    nome         VARCHAR(100)  NOT NULL,
    preco        DECIMAL(10,2) NOT NULL,
    categoria_id INT           NOT NULL,
    PRIMARY KEY (id),
    FOREIGN KEY (categoria_id) REFERENCES categorias(id)
);
```

```sql
INSERT INTO categorias (nome) VALUES ('Informatica'), ('Audio'), ('Perifericos');

INSERT INTO produtos (nome, preco, categoria_id) VALUES
    ('Teclado Mecanico', 299.90, 1),
    ('Monitor 24"',     1299.00, 1),
    ('Headset USB',      229.90, 2),
    ('Mouse Sem Fio',    149.90, 3);
```

---

## FOREIGN KEY — chave estrangeira

A `FOREIGN KEY` garante **integridade referencial**: voce nao pode inserir um `produto` com `categoria_id = 99` se nao existir uma categoria com `id = 99`.

```sql
-- Tentativa de insercao invalida — erro
INSERT INTO produtos (nome, preco, categoria_id) VALUES ('Produto X', 50.00, 99);
-- ERROR: Cannot add or update a child row: a foreign key constraint fails
```

---

## ON DELETE e ON UPDATE — comportamento em cascata

Define o que acontece com os registros filhos quando o registro pai e alterado ou removido.

| Opcao | Comportamento |
|-------|---------------|
| `RESTRICT` (padrao) | Bloqueia a operacao se houver filhos |
| `CASCADE` | Propaga a alteracao/exclusao para os filhos |
| `SET NULL` | Define a coluna estrangeira como NULL nos filhos |
| `NO ACTION` | Similar ao RESTRICT, verificado no final da transacao |

```sql
CREATE TABLE produtos (
    id           INT           NOT NULL AUTO_INCREMENT,
    nome         VARCHAR(100)  NOT NULL,
    preco        DECIMAL(10,2) NOT NULL,
    categoria_id INT,
    PRIMARY KEY (id),
    FOREIGN KEY (categoria_id)
        REFERENCES categorias(id)
        ON DELETE SET NULL
        ON UPDATE CASCADE
);
```

### Exemplos de comportamento

```sql
-- Com ON DELETE CASCADE: deleta a categoria e todos os seus produtos
DELETE FROM categorias WHERE id = 1;

-- Com ON DELETE SET NULL: deleta a categoria, produtos ficam com categoria_id = NULL
DELETE FROM categorias WHERE id = 1;

-- Com RESTRICT (padrao): bloqueia a exclusao se houver produtos vinculados
DELETE FROM categorias WHERE id = 1;
-- ERROR: Cannot delete or update a parent row: a foreign key constraint fails
```

---

## Relacionamento N:N (tabela intermediaria)

Quando varios alunos podem estar em varias disciplinas, cria-se uma **tabela de juncao**.

```sql
CREATE TABLE alunos (
    id   INT         NOT NULL AUTO_INCREMENT,
    nome VARCHAR(150) NOT NULL,
    PRIMARY KEY (id)
);

CREATE TABLE disciplinas (
    id   INT        NOT NULL AUTO_INCREMENT,
    nome VARCHAR(100) NOT NULL,
    PRIMARY KEY (id)
);

-- Tabela intermediaria que representa a matricula
CREATE TABLE matriculas (
    aluno_id      INT NOT NULL,
    disciplina_id INT NOT NULL,
    data_matricula DATE NOT NULL,
    PRIMARY KEY (aluno_id, disciplina_id),
    FOREIGN KEY (aluno_id)      REFERENCES alunos(id)      ON DELETE CASCADE,
    FOREIGN KEY (disciplina_id) REFERENCES disciplinas(id) ON DELETE CASCADE
);
```

---

## Relacionamento 1:1

```sql
CREATE TABLE usuarios (
    id    INT NOT NULL AUTO_INCREMENT,
    email VARCHAR(150) NOT NULL UNIQUE,
    PRIMARY KEY (id)
);

CREATE TABLE perfis (
    id         INT NOT NULL AUTO_INCREMENT,
    usuario_id INT NOT NULL UNIQUE,   -- UNIQUE garante o 1:1
    bio        TEXT,
    avatar_url VARCHAR(255),
    PRIMARY KEY (id),
    FOREIGN KEY (usuario_id) REFERENCES usuarios(id) ON DELETE CASCADE
);
```

---

## Pratica sugerida (exercicio concreto)
### Projeto: Sistema de pedidos (via Workbench)

### Requisitos obrigatorios
1. Crie o banco `pedidos_db`.
2. Crie a tabela `clientes` (id, nome, email UNIQUE).
3. Crie a tabela `pedidos` (id, cliente_id FK, total DECIMAL, criado_em DATETIME DEFAULT CURRENT_TIMESTAMP).
4. Configure `ON DELETE RESTRICT` na FK de pedidos para clientes.
5. Insira 2 clientes e 3 pedidos (ao menos 2 pedidos para o mesmo cliente).
6. Tente deletar um cliente que possui pedidos e observe o erro.

### Entrega esperada
- Scripts de criacao, insercao, e o erro gerado na tentativa de exclusao.

## Desafio opcional
Implemente a tabela `itens_pedido` como tabela de juncao entre `pedidos` e `produtos` (do banco `loja_db`). Adicione a coluna `quantidade INT NOT NULL` e `preco_unitario DECIMAL(10,2) NOT NULL` para registrar o preco no momento da compra.

## Navegacao
- [Aula anterior: MySQL e SQL (parte 5) - SELECT Clauses](../../etapa-2/mysql-e-sql-parte-5-select-clauses/)
- [Voltar para Banco de dados relacional](../../)
- [Proxima aula: MySQL e SQL (parte 7) - Buscas especiais](../../etapa-4/mysql-e-sql-parte-7-buscas-especiais/)
