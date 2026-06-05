# MySQL e SQL (parte 1) - Definicao e diferenciacao

> Modulo: Banco de dados relacional

## Objetivo da aula
Entender o que e um banco de dados relacional, distinguir SQL de MySQL, diferenciar o servico MySQL do Workbench, e conhecer as categorias de comandos SQL.

## Exemplo rapido
```sql
-- Listando os bancos de dados existentes no servidor
SHOW DATABASES;

-- Criando e selecionando um banco
CREATE DATABASE loja;
USE loja;
```

## O que e um banco de dados relacional

Um banco de dados relacional organiza dados em **tabelas** (linhas e colunas), onde cada tabela representa uma entidade (ex.: clientes, produtos, pedidos). As tabelas se relacionam entre si por meio de chaves.

| Conceito | Descricao |
|----------|-----------|
| Tabela | Estrutura com linhas (registros) e colunas (campos) |
| Linha | Um registro individual |
| Coluna | Um atributo do registro |
| Chave primaria | Identificador unico de cada linha |
| Chave estrangeira | Referencia a chave primaria de outra tabela |

## SQL vs MySQL

| | SQL | MySQL |
|---|-----|-------|
| O que e | Linguagem de consulta estruturada | Sistema Gerenciador de Banco de Dados (SGBD) |
| Funcao | Define como escrever comandos para manipular dados | Executa esses comandos e gerencia os arquivos do banco |
| Analogia | A linguagem (portugues) | O interprete (pessoa que fala portugues) |

> **SQL** e uma linguagem padrao (ISO/ANSI). **MySQL** e um dos varios SGBDs que a implementam — outros exemplos sao PostgreSQL, SQLite e MariaDB.

## Servico MySQL vs MySQL Workbench

| | Servico MySQL | MySQL Workbench |
|---|--------------|-----------------|
| O que e | Processo em execucao no servidor | Aplicativo visual de administracao |
| Funcao | Armazena e processa os dados | Interface grafica para modelagem e consultas |
| Acesso | Via terminal (`mysql -u root -p`) ou drivers | Interface grafica (GUI) |
| Obrigatorio? | Sim — sem ele nada funciona | Nao — e opcional, mas facilita o desenvolvimento |

> O Workbench se conecta ao servico MySQL. Se o servico estiver parado, o Workbench nao consegue se conectar.

## Categorias de comandos SQL

| Categoria | Sigla | Exemplos | Uso |
|-----------|-------|---------|-----|
| Linguagem de Definicao de Dados | DDL | `CREATE`, `ALTER`, `DROP` | Estrutura do banco |
| Linguagem de Manipulacao de Dados | DML | `INSERT`, `UPDATE`, `DELETE` | Conteudo das tabelas |
| Linguagem de Consulta de Dados | DQL | `SELECT` | Leitura de dados |
| Linguagem de Controle de Dados | DCL | `GRANT`, `REVOKE` | Permissoes de acesso |

## Fluxo basico de trabalho

```
1. Iniciar o servico MySQL
2. Conectar via Workbench ou terminal
3. Criar ou selecionar um banco de dados (USE)
4. Criar tabelas (DDL)
5. Inserir e consultar dados (DML / DQL)
```

## Pratica sugerida (exercicio concreto)
### Projeto: Exploracao inicial via Workbench
Conecte-se ao MySQL Workbench e realize as seguintes acoes.

### Requisitos obrigatorios
1. Abra o Workbench e conecte-se ao servidor local.
2. Execute `SHOW DATABASES;` e identifique os bancos existentes.
3. Crie um banco chamado `curso_db` com `CREATE DATABASE curso_db;`.
4. Execute `USE curso_db;` para seleciona-lo.
5. Execute `SHOW TABLES;` e observe que ainda nao ha tabelas.

### Entrega esperada
- Print ou relato das saidas de cada comando executado.

## Desafio opcional
Pesquise a diferenca entre MySQL e MariaDB. Escreva em um comentario SQL (usando `--`) dentro do Workbench por que eles coexistem no mercado.

## Navegacao
- [Voltar para Banco de dados relacional](../../)
- [Proxima aula: MySQL e SQL (parte 2) - Criacao de bancos de dados e tabelas](../mysql-e-sql-parte-2-criacao-de-bancos-de-dados-e-tabelas/)
