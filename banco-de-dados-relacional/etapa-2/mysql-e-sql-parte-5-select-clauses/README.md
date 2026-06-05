# MySQL e SQL (parte 5) - SELECT Clauses: WHERE, ORDER BY, AS, CAST, BETWEEN

> Modulo: Banco de dados relacional

## Objetivo da aula
Escrever consultas `SELECT` mais precisas usando filtros, ordenacao, apelidos de coluna, conversao de tipos e intervalos de valor.

## Exemplo rapido
```sql
SELECT nome AS produto, CAST(preco AS CHAR) AS preco_texto
FROM produtos
WHERE ativo = TRUE AND preco BETWEEN 100.00 AND 500.00
ORDER BY preco DESC;
```

## Tabela de referencia para os exemplos

```sql
USE loja_db;

-- Reaproveitando a tabela de produtos da aula anterior
-- Insira alguns registros antes de testar:
INSERT INTO produtos (nome, preco, estoque, ativo) VALUES
    ('Teclado Mecanico',  299.90, 15, TRUE),
    ('Mouse Sem Fio',     149.90, 30, TRUE),
    ('Monitor 24"',      1299.00,  8, TRUE),
    ('Headset USB',       229.90, 20, TRUE),
    ('Webcam HD',         189.90, 12, FALSE),
    ('Mousepad XL',        49.90, 50, TRUE);
```

---

## WHERE — filtrando registros

```sql
-- Igualdade
SELECT * FROM produtos WHERE ativo = TRUE;

-- Diferenca
SELECT * FROM produtos WHERE ativo != FALSE;

-- Comparacoes numericas
SELECT * FROM produtos WHERE preco > 200.00;
SELECT * FROM produtos WHERE estoque <= 10;

-- Multiplas condicoes
SELECT * FROM produtos WHERE ativo = TRUE AND preco < 300.00;
SELECT * FROM produtos WHERE estoque = 0 OR ativo = FALSE;

-- Valor nulo
SELECT * FROM produtos WHERE deletado_em IS NULL;
SELECT * FROM produtos WHERE deletado_em IS NOT NULL;
```

### Operadores de comparacao

| Operador | Descricao |
|----------|-----------|
| `=` | Igual |
| `!=` ou `<>` | Diferente |
| `<` | Menor que |
| `>` | Maior que |
| `<=` | Menor ou igual |
| `>=` | Maior ou igual |
| `IS NULL` | Campo sem valor |
| `IS NOT NULL` | Campo com valor |
| `LIKE 'texto%'` | Correspondencia parcial |

---

## ORDER BY — ordenando resultados

```sql
-- Ordem crescente (padrao)
SELECT nome, preco FROM produtos ORDER BY preco ASC;

-- Ordem decrescente
SELECT nome, preco FROM produtos ORDER BY preco DESC;

-- Ordenando por multiplos campos
SELECT nome, estoque, preco FROM produtos
ORDER BY estoque DESC, preco ASC;
```

---

## AS — apelidos (aliases)

`AS` renomeia colunas ou tabelas na saida da consulta, sem alterar o banco.

```sql
-- Renomeando colunas na saida
SELECT
    nome        AS produto,
    preco       AS valor,
    estoque     AS qtd_disponivel
FROM produtos;

-- Alias sem aspas (funciona se nao houver espacos)
SELECT nome produto, preco valor FROM produtos;

-- Alias com espaco exige aspas ou crase
SELECT preco AS `preco em reais` FROM produtos;
```

---

## BETWEEN — intervalos de valor

```sql
-- Produtos com preco entre 100 e 300 (inclusive)
SELECT nome, preco FROM produtos
WHERE preco BETWEEN 100.00 AND 300.00;

-- Equivalente com >= e <=
SELECT nome, preco FROM produtos
WHERE preco >= 100.00 AND preco <= 300.00;

-- Intervalo em datas
SELECT * FROM pedidos
WHERE criado_em BETWEEN '2024-01-01' AND '2024-12-31';
```

---

## CAST — convertendo tipos

`CAST` converte um valor de um tipo para outro na saida da consulta.

```sql
-- Inteiro para texto
SELECT nome, CAST(estoque AS CHAR) AS estoque_texto FROM produtos;

-- Decimal para inteiro (trunca a parte decimal)
SELECT nome, CAST(preco AS UNSIGNED) AS preco_inteiro FROM produtos;

-- Texto para data
SELECT CAST('2024-06-15' AS DATE) AS data_convertida;
```

| Tipo alvo | Descricao |
|-----------|-----------|
| `CHAR` | Converte para texto |
| `UNSIGNED` / `SIGNED` | Converte para inteiro |
| `DECIMAL(M,D)` | Converte para decimal |
| `DATE` | Converte para data |
| `DATETIME` | Converte para data e hora |

---

## Combinando tudo

```sql
SELECT
    nome       AS produto,
    preco      AS valor,
    CAST(estoque AS CHAR) AS qtd
FROM produtos
WHERE ativo = TRUE
  AND preco BETWEEN 100.00 AND 400.00
ORDER BY preco ASC;
```

---

## Pratica sugerida (exercicio concreto)
### Projeto: Consultas no catalogo da loja

### Requisitos obrigatorios
1. Consulte todos os produtos ativos com preco acima de R$ 150,00, ordenados do mais caro para o mais barato.
2. Consulte os produtos com estoque entre 10 e 25 unidades.
3. Crie uma consulta que exiba `nome` com alias `produto` e `preco` como `valor_unitario`.
4. Use `CAST` para exibir o preco como texto na consulta.
5. Consulte produtos cujo nome comece com a letra `M` usando `WHERE nome LIKE 'M%'`.

### Entrega esperada
- Os 5 scripts SQL e as saidas obtidas.

## Desafio opcional
Crie uma consulta que exiba o nome do produto, o preco original e o preco com 10% de desconto (calculado diretamente no `SELECT` como `preco * 0.90`), apenas para produtos ativos com preco acima de R$ 100,00, ordenados pelo preco com desconto em ordem crescente.

## Navegacao
- [Aula anterior: MySQL e SQL (parte 4) - CRUD](../mysql-e-sql-parte-4-crud/)
- [Voltar para Banco de dados relacional](../../)
- [Proxima aula: MySQL e SQL (parte 6) - Cardinalidade entre tabelas](../../etapa-3/mysql-e-sql-parte-6-cardinalidade/)
