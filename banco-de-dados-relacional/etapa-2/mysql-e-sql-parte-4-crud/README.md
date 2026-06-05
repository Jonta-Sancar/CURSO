# MySQL e SQL (parte 4) - CRUD

> Modulo: Banco de dados relacional

## Objetivo da aula
Realizar as quatro operacoes fundamentais de manipulacao de dados: inserir, consultar, atualizar e remover registros.

## Exemplo rapido
```sql
INSERT INTO produtos (nome, preco) VALUES ('Teclado', 199.90);
SELECT * FROM produtos;
UPDATE produtos SET preco = 179.90 WHERE id = 1;
DELETE FROM produtos WHERE id = 1;
```

## Tabela de referencia para os exemplos

```sql
CREATE DATABASE loja_db;
USE loja_db;

CREATE TABLE produtos (
    id        INT           NOT NULL AUTO_INCREMENT,
    nome      VARCHAR(100)  NOT NULL,
    preco     DECIMAL(10,2) NOT NULL,
    estoque   INT           NOT NULL DEFAULT 0,
    ativo     BOOLEAN       NOT NULL DEFAULT TRUE,
    PRIMARY KEY (id)
);
```

---

## INSERT — criando registros

```sql
-- Inserindo um unico registro
INSERT INTO produtos (nome, preco, estoque)
VALUES ('Teclado Mecanico', 299.90, 15);

-- Inserindo varios registros de uma vez
INSERT INTO produtos (nome, preco, estoque) VALUES
    ('Mouse Sem Fio',   149.90, 30),
    ('Monitor 24"',    1299.00,  8),
    ('Headset USB',     229.90, 20);
```

> Colunas com `DEFAULT` ou `AUTO_INCREMENT` podem ser omitidas.

---

## SELECT — consultando registros

```sql
-- Todas as colunas
SELECT * FROM produtos;

-- Colunas especificas
SELECT nome, preco FROM produtos;

-- Com condicao
SELECT nome, preco FROM produtos WHERE ativo = TRUE;

-- Limitando resultados
SELECT * FROM produtos LIMIT 5;
```

---

## UPDATE — atualizando registros

```sql
-- Atualiza o preco de um produto especifico
UPDATE produtos
SET preco = 279.90
WHERE id = 1;

-- Atualiza multiplos campos ao mesmo tempo
UPDATE produtos
SET preco = 199.90, estoque = 10
WHERE id = 2;
```

> **ATENCAO:** Um `UPDATE` sem `WHERE` atualiza **todos** os registros da tabela.
> ```sql
> -- PERIGOSO — afeta todas as linhas
> UPDATE produtos SET ativo = FALSE;
> ```

---

## DELETE — removendo registros

```sql
-- Remove um registro especifico
DELETE FROM produtos WHERE id = 3;

-- Remove todos os produtos inativos
DELETE FROM produtos WHERE ativo = FALSE;
```

> **ATENCAO:** Um `DELETE` sem `WHERE` remove **todos** os registros da tabela.
> ```sql
> -- PERIGOSO — apaga todas as linhas (mas mantem a estrutura da tabela)
> DELETE FROM produtos;
>
> -- Para apagar tudo e resetar o AUTO_INCREMENT, use TRUNCATE
> TRUNCATE TABLE produtos;
> ```

---

## Comparativo das operacoes

| Operacao | Comando | O que faz |
|----------|---------|-----------|
| Create | `INSERT INTO` | Adiciona novas linhas |
| Read | `SELECT` | Le linhas existentes |
| Update | `UPDATE ... SET` | Modifica linhas existentes |
| Delete | `DELETE FROM` | Remove linhas existentes |

---

## Pratica sugerida (exercicio concreto)
### Projeto: Gerenciando o catalogo da loja

### Requisitos obrigatorios
1. Crie o banco `loja_db` e a tabela `produtos` conforme o modelo acima.
2. Insira ao menos 5 produtos com precos e estoques variados.
3. Consulte todos os produtos com `SELECT * FROM produtos`.
4. Atualize o preco de dois produtos usando `UPDATE ... WHERE id = ?`.
5. Desative (defina `ativo = FALSE`) um produto sem remove-lo.
6. Delete um produto pelo `id`.
7. Consulte novamente para confirmar as mudancas.

### Entrega esperada
- Script SQL completo com todos os comandos executados em ordem.

## Desafio opcional
Implemente uma **exclusao logica**: em vez de usar `DELETE`, adicione uma coluna `deletado_em DATETIME DEFAULT NULL` e substitua todas as delecoes por `UPDATE ... SET deletado_em = NOW() WHERE id = ?`. Ajuste o `SELECT` para nao exibir registros deletados logicamente.

## Navegacao
- [Aula anterior: MySQL e SQL (parte 3) - Comentarios e valores padrao](../../etapa-1/mysql-e-sql-parte-3-comentarios-e-valores-padrao/)
- [Voltar para Banco de dados relacional](../../)
- [Proxima aula: MySQL e SQL (parte 5) - SELECT Clauses](../mysql-e-sql-parte-5-select-clauses/)
