# MySQL e SQL (parte 2) - Criacao de bancos de dados e tabelas, configuracao de colunas

> Modulo: Banco de dados relacional

## Objetivo da aula
Criar bancos de dados e tabelas no MySQL, configurar colunas com tipos de dados adequados, definir chaves primarias e aplicar restricoes basicas.

## Exemplo rapido
```sql
CREATE DATABASE loja;
USE loja;

CREATE TABLE produtos (
    id      INT          NOT NULL AUTO_INCREMENT,
    nome    VARCHAR(100) NOT NULL,
    preco   DECIMAL(10,2) NOT NULL,
    ativo   BOOLEAN      NOT NULL DEFAULT TRUE,
    PRIMARY KEY (id)
);
```

## CREATE DATABASE e USE

```sql
-- Cria o banco de dados
CREATE DATABASE nome_do_banco;

-- Seleciona o banco para uso
USE nome_do_banco;

-- Lista todos os bancos existentes
SHOW DATABASES;

-- Remove o banco e tudo dentro dele (irreversivel)
DROP DATABASE nome_do_banco;
```

## CREATE TABLE

```sql
CREATE TABLE nome_da_tabela (
    coluna1 TIPO restricoes,
    coluna2 TIPO restricoes,
    ...
);
```

### Exemplo completo
```sql
CREATE TABLE clientes (
    id         INT          NOT NULL AUTO_INCREMENT,
    nome       VARCHAR(150) NOT NULL,
    email      VARCHAR(150) NOT NULL,
    nascimento DATE,
    saldo      DECIMAL(10,2),
    PRIMARY KEY (id)
);
```

## Tipos de dados principais

| Tipo | Uso | Exemplo |
|------|-----|---------|
| `INT` | Numeros inteiros | `42`, `-7` |
| `BIGINT` | Inteiros muito grandes | IDs de alto volume |
| `DECIMAL(M,D)` | Valores monetarios precisos | `DECIMAL(10,2)` = ate 10 digitos, 2 decimais |
| `FLOAT` / `DOUBLE` | Numeros com ponto flutuante | Medicoes cientificas |
| `VARCHAR(N)` | Texto de tamanho variavel, ate N caracteres | Nomes, emails |
| `TEXT` | Texto longo sem limite fixo | Descricoes, comentarios |
| `DATE` | Data (AAAA-MM-DD) | `'2024-03-15'` |
| `DATETIME` | Data e hora | `'2024-03-15 14:30:00'` |
| `BOOLEAN` | Verdadeiro ou falso (internamente TINYINT 0/1) | `TRUE`, `FALSE` |
| `ENUM(...)` | Valor de uma lista fixa | `ENUM('ativo','inativo')` |

## Restricoes de coluna

| Restricao | Descricao |
|-----------|-----------|
| `NOT NULL` | O campo nao pode ficar vazio |
| `AUTO_INCREMENT` | O MySQL atribui o proximo valor automaticamente (somente em INT com PK) |
| `PRIMARY KEY` | Identificador unico da linha |
| `UNIQUE` | Nao permite valores duplicados na coluna |

### PRIMARY KEY
```sql
-- Declarada inline
CREATE TABLE categorias (
    id   INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(80) NOT NULL
);

-- Declarada no final (mais legivel em chaves compostas)
CREATE TABLE itens_pedido (
    pedido_id  INT NOT NULL,
    produto_id INT NOT NULL,
    quantidade INT NOT NULL,
    PRIMARY KEY (pedido_id, produto_id)
);
```

## Listando e removendo tabelas

```sql
-- Lista as tabelas do banco selecionado
SHOW TABLES;

-- Mostra a estrutura de uma tabela
DESCRIBE clientes;
DESC clientes;

-- Remove a tabela e todos os seus dados (irreversivel)
DROP TABLE clientes;
```

## Pratica sugerida (exercicio concreto)
### Projeto: Estrutura de um sistema de biblioteca (via Workbench)

### Requisitos obrigatorios
1. Crie o banco `biblioteca_db`.
2. Selecione-o com `USE`.
3. Crie a tabela `autores` com as colunas: `id` (INT, PK, AUTO_INCREMENT), `nome` (VARCHAR 150, NOT NULL), `nacionalidade` (VARCHAR 100).
4. Crie a tabela `livros` com as colunas: `id` (INT, PK, AUTO_INCREMENT), `titulo` (VARCHAR 200, NOT NULL), `ano_publicacao` (INT), `paginas` (INT), `disponivel` (BOOLEAN, NOT NULL).
5. Execute `SHOW TABLES;` e `DESC livros;` para confirmar a estrutura criada.

### Entrega esperada
- Scripts SQL utilizados e o resultado de `DESC livros;`.

## Desafio opcional
Adicione a tabela `emprestimos` com: `id`, `data_emprestimo` (DATE), `data_devolucao` (DATE), `status` (ENUM com valores `'ativo'` e `'devolvido'`). Observe como o ENUM restringe os valores aceitos.

## Navegacao
- [Aula anterior: MySQL e SQL (parte 1) - Definicao e diferenciacao](../mysql-e-sql-parte-1-definicao-e-diferenciacao/)
- [Voltar para Banco de dados relacional](../../)
- [Proxima aula: MySQL e SQL (parte 3) - Comentarios e valores padrao](../mysql-e-sql-parte-3-comentarios-e-valores-padrao/)
