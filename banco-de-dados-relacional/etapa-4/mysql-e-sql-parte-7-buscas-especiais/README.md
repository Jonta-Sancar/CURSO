# MySQL e SQL (parte 7) - Buscas especiais: INNER JOIN, EXISTS, DISTINCT, GROUP BY, funcoes de agregacao

> Modulo: Banco de dados relacional

## Objetivo da aula
Combinar dados de multiplas tabelas com `INNER JOIN`, usar subconsultas com `EXISTS`, eliminar duplicatas com `DISTINCT`, agrupar registros com `GROUP BY` e calcular totais com funcoes de agregacao.

## Exemplo rapido
```sql
SELECT c.nome AS categoria, COUNT(p.id) AS total_produtos, AVG(p.preco) AS preco_medio
FROM categorias c
INNER JOIN produtos p ON p.categoria_id = c.id
GROUP BY c.id, c.nome
ORDER BY total_produtos DESC;
```

## Tabela de referencia para os exemplos

```sql
USE catalogo_db;
-- Reaproveitando as tabelas categorias e produtos da aula 6
```

---

## INNER JOIN — combinando tabelas

`INNER JOIN` retorna apenas as linhas onde ha correspondencia em **ambas** as tabelas.

```sql
-- Exibindo produtos com o nome da sua categoria
SELECT
    p.nome       AS produto,
    p.preco,
    c.nome       AS categoria
FROM produtos p
INNER JOIN categorias c ON c.id = p.categoria_id;
```

### Multiplos JOINs

```sql
-- Pedido + cliente + itens
SELECT
    cl.nome        AS cliente,
    pe.id          AS pedido,
    pr.nome        AS produto,
    ip.quantidade,
    ip.preco_unitario
FROM pedidos pe
INNER JOIN clientes       cl ON cl.id = pe.cliente_id
INNER JOIN itens_pedido   ip ON ip.pedido_id = pe.id
INNER JOIN produtos       pr ON pr.id = ip.produto_id;
```

> `INNER JOIN` descarta linhas sem correspondencia. Para incluir registros sem par, use `LEFT JOIN`.

---

## EXISTS — verificando existencia com subconsulta

`EXISTS` retorna `TRUE` se a subconsulta retornar ao menos uma linha.

```sql
-- Clientes que possuem ao menos um pedido
SELECT nome
FROM clientes cl
WHERE EXISTS (
    SELECT 1 FROM pedidos pe WHERE pe.cliente_id = cl.id
);

-- Clientes que NAO possuem nenhum pedido
SELECT nome
FROM clientes cl
WHERE NOT EXISTS (
    SELECT 1 FROM pedidos pe WHERE pe.cliente_id = cl.id
);
```

> `SELECT 1` dentro do `EXISTS` e uma convencao: o valor retornado nao importa, apenas se ha linhas.

---

## DISTINCT — eliminando duplicatas

```sql
-- Sem DISTINCT: repete categorias se houver varios produtos
SELECT categoria_id FROM produtos;

-- Com DISTINCT: cada categoria aparece uma unica vez
SELECT DISTINCT categoria_id FROM produtos;

-- Em combinacao com JOIN
SELECT DISTINCT c.nome AS categoria
FROM categorias c
INNER JOIN produtos p ON p.categoria_id = c.id;
```

---

## GROUP BY — agrupando registros

`GROUP BY` agrupa linhas com o mesmo valor em uma coluna, geralmente usado com funcoes de agregacao.

```sql
-- Contando produtos por categoria
SELECT categoria_id, COUNT(*) AS total
FROM produtos
GROUP BY categoria_id;

-- Com JOIN para exibir o nome da categoria
SELECT c.nome AS categoria, COUNT(p.id) AS total_produtos
FROM categorias c
INNER JOIN produtos p ON p.categoria_id = c.id
GROUP BY c.id, c.nome;
```

### HAVING — filtrando grupos

`WHERE` filtra **antes** do agrupamento; `HAVING` filtra **depois**.

```sql
-- Apenas categorias com mais de 2 produtos
SELECT c.nome, COUNT(p.id) AS total
FROM categorias c
INNER JOIN produtos p ON p.categoria_id = c.id
GROUP BY c.id, c.nome
HAVING COUNT(p.id) > 2;
```

---

## Funcoes de agregacao

| Funcao | Descricao | Exemplo |
|--------|-----------|---------|
| `COUNT(expr)` | Conta linhas (ou valores nao nulos) | `COUNT(*)`, `COUNT(id)` |
| `SUM(col)` | Soma os valores | `SUM(preco)` |
| `AVG(col)` | Media aritmetica | `AVG(preco)` |
| `MAX(col)` | Maior valor | `MAX(preco)` |
| `MIN(col)` | Menor valor | `MIN(preco)` |

```sql
SELECT
    COUNT(*)         AS total_produtos,
    SUM(preco)       AS soma_precos,
    AVG(preco)       AS preco_medio,
    MAX(preco)       AS mais_caro,
    MIN(preco)       AS mais_barato
FROM produtos
WHERE ativo = TRUE;
```

### Por grupo
```sql
SELECT
    c.nome           AS categoria,
    COUNT(p.id)      AS qtd,
    SUM(p.preco)     AS soma,
    AVG(p.preco)     AS media,
    MAX(p.preco)     AS mais_caro,
    MIN(p.preco)     AS mais_barato
FROM categorias c
INNER JOIN produtos p ON p.categoria_id = c.id
GROUP BY c.id, c.nome
ORDER BY media DESC;
```

---

## Ordem de execucao logica do SELECT

```
1. FROM / JOIN    — de onde vem os dados
2. WHERE          — filtra linhas individuais
3. GROUP BY       — agrupa os resultados
4. HAVING         — filtra grupos
5. SELECT         — define o que exibir
6. ORDER BY       — ordena a saida
7. LIMIT          — limita a quantidade
```

---

## Pratica sugerida (exercicio concreto)
### Projeto: Relatorio de vendas

### Requisitos obrigatorios
1. Usando o banco `catalogo_db` com categorias e produtos, execute as consultas abaixo.
2. Liste todos os produtos com o nome da sua categoria (INNER JOIN).
3. Conte quantos produtos existem por categoria (GROUP BY + COUNT).
4. Exiba o produto mais caro e o mais barato de cada categoria (MAX + MIN + GROUP BY).
5. Liste categorias que possuem ao menos 2 produtos (HAVING).
6. Liste categorias que possuem ao menos um produto ativo (EXISTS).
7. Liste os precos unicos (sem repeticao) de todos os produtos (DISTINCT).

### Entrega esperada
- Os 6 scripts SQL e as saidas correspondentes.

## Desafio opcional
Crie uma consulta que exiba o nome do cliente, o numero de pedidos realizados e o valor total gasto (SUM dos totais dos pedidos), apenas para clientes que fizeram mais de 1 pedido (HAVING). Ordene pelo valor total decrescente.

## Navegacao
- [Aula anterior: MySQL e SQL (parte 6) - Cardinalidade entre tabelas](../../etapa-3/mysql-e-sql-parte-6-cardinalidade/)
- [Voltar para Banco de dados relacional](../../)
