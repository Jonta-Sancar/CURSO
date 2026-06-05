# PHP (parte 12) - PDO

> Modulo: Sistemas Web

## Objetivo da aula
Aprender a conectar o PHP a um banco de dados MySQL usando PDO (PHP Data Objects), executar consultas de forma segura com prepared statements e tratar erros de banco de dados adequadamente.

## O que e PDO
PDO (PHP Data Objects) e uma extensao nativa do PHP que fornece uma interface uniforme para acessar diferentes bancos de dados (MySQL, PostgreSQL, SQLite, etc.) usando o mesmo codigo.

### Por que PDO e nao mysql_query
- `mysql_query` foi removido no PHP 7 — nao existe mais.
- PDO suporta **prepared statements**, que protegem contra SQL Injection.
- PDO funciona com varios bancos de dados sem mudar o codigo da aplicacao.

---

## Conectando ao banco de dados

```php
$host   = 'localhost';
$banco  = 'nome_do_banco';
$usuario = 'root';
$senha  = '';

try {
    $pdo = new PDO(
        "mysql:host=$host;dbname=$banco;charset=utf8",
        $usuario,
        $senha
    );
    $pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
    $pdo->setAttribute(PDO::ATTR_DEFAULT_FETCH_MODE, PDO::FETCH_ASSOC);
} catch (PDOException $e) {
    echo "Erro na conexao: " . $e->getMessage();
    exit;
}
```

### Atributos importantes

| Atributo                        | Valor                    | Efeito                                               |
|---------------------------------|--------------------------|------------------------------------------------------|
| `PDO::ATTR_ERRMODE`             | `ERRMODE_EXCEPTION`      | Lanca excecoes em caso de erro (recomendado)         |
| `PDO::ATTR_DEFAULT_FETCH_MODE`  | `FETCH_ASSOC`            | Retorna linhas como arrays associativos por padrao   |
| `PDO::ATTR_EMULATE_PREPARES`    | `false`                  | Usa prepared statements reais do banco               |

---

## Modos de busca (fetch modes)

| Constante             | Resultado                                      |
|-----------------------|------------------------------------------------|
| `PDO::FETCH_ASSOC`    | Array com chaves pelo nome da coluna           |
| `PDO::FETCH_NUM`      | Array com indices numericos                    |
| `PDO::FETCH_OBJ`      | Objeto com propriedades pelo nome da coluna    |
| `PDO::FETCH_CLASS`    | Instancia de uma classe especificada           |

---

## Executando consultas

### Consulta simples (sem parametros externos)
Use `query()` apenas quando nao ha dados vindos do usuario.

```php
$stmt = $pdo->query("SELECT * FROM usuarios");
$usuarios = $stmt->fetchAll();

foreach ($usuarios as $usuario) {
    echo $usuario['nome'] . '<br>';
}
```

---

## Prepared Statements

Prepared statements separam o codigo SQL dos dados, eliminando o risco de SQL Injection.

### Sintaxe com marcadores `?` (posicional)
```php
$stmt = $pdo->prepare("SELECT * FROM usuarios WHERE email = ?");
$stmt->execute([$email]);
$usuario = $stmt->fetch();
```

### Sintaxe com marcadores `:nome` (nomeado)
```php
$stmt = $pdo->prepare("SELECT * FROM usuarios WHERE email = :email AND ativo = :ativo");
$stmt->execute([':email' => $email, ':ativo' => 1]);
$usuario = $stmt->fetch();
```

---

## CRUD com PDO

### INSERT
```php
$stmt = $pdo->prepare("INSERT INTO usuarios (nome, email, senha) VALUES (:nome, :email, :senha)");
$stmt->execute([
    ':nome'  => $nome,
    ':email' => $email,
    ':senha' => $senha,
]);

$idInserido = $pdo->lastInsertId();
```

### SELECT — buscar todos
```php
$stmt = $pdo->prepare("SELECT * FROM usuarios WHERE ativo = :ativo");
$stmt->execute([':ativo' => 1]);
$usuarios = $stmt->fetchAll();
```

### SELECT — buscar um registro
```php
$stmt = $pdo->prepare("SELECT * FROM usuarios WHERE id = :id");
$stmt->execute([':id' => $id]);
$usuario = $stmt->fetch();

if (!$usuario) {
    echo "Usuario nao encontrado.";
}
```

### UPDATE
```php
$stmt = $pdo->prepare("UPDATE usuarios SET nome = :nome WHERE id = :id");
$stmt->execute([':nome' => $novoNome, ':id' => $id]);

echo $stmt->rowCount() . " linha(s) afetada(s).";
```

### DELETE
```php
$stmt = $pdo->prepare("DELETE FROM usuarios WHERE id = :id");
$stmt->execute([':id' => $id]);
```

---

## Tratamento de erros

```php
try {
    $stmt = $pdo->prepare("INSERT INTO usuarios (email) VALUES (:email)");
    $stmt->execute([':email' => $email]);
} catch (PDOException $e) {
    // $e->getMessage() — mensagem tecnica (nao exibir ao usuario final)
    error_log($e->getMessage()); // registra no log do servidor
    echo "Ocorreu um erro. Tente novamente.";
}
```

---

## Organizando a conexao em arquivo separado

### `conexao.php`
```php
<?php

function conectar(): PDO {
    $pdo = new PDO(
        'mysql:host=localhost;dbname=meu_banco;charset=utf8',
        'root',
        ''
    );
    $pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
    $pdo->setAttribute(PDO::ATTR_DEFAULT_FETCH_MODE, PDO::FETCH_ASSOC);
    return $pdo;
}
```

### Usando em outro arquivo
```php
<?php
require_once 'conexao.php';

$pdo = conectar();
$stmt = $pdo->query("SELECT * FROM produtos");
$produtos = $stmt->fetchAll();
```

---

## Pratica sugerida (exercicio concreto)
### Projeto: CRUD de produtos via web

### Requisitos obrigatorios
1. Crie uma tabela `produtos` com as colunas: `id`, `nome`, `preco`, `estoque`.
2. Crie um arquivo `conexao.php` com a funcao de conexao PDO.
3. Implemente as 4 operacoes em paginas separadas:
   - `listar.php` — exibe todos os produtos em uma tabela HTML.
   - `cadastrar.php` — formulario POST para inserir novo produto.
   - `editar.php` — formulario preenchido com dados atuais para atualizar.
   - `excluir.php` — recebe o `id` via GET e deleta o registro.
4. Use prepared statements em todas as operacoes que recebem dados externos.
5. Apos cadastrar, editar ou excluir, redirecione para `listar.php` com `header('Location: listar.php')`.

### Regras de validacao
- Nao use `query()` onde ha dados vindos do usuario — sempre `prepare()` + `execute()`.
- O campo `preco` deve ser validado como numero antes de inserir.
- Trate erros com `try/catch` e exiba mensagens amigaveis ao usuario.

### Desafio opcional
Adicione paginacao em `listar.php` usando `LIMIT` e `OFFSET` no SQL, com links "anterior" e "proximo" passados via GET.

---

## Navegacao
- [Aula anterior: PHP (parte 11) - Metodos de requisicao](../../etapa-1/php-parte-11-metodos-de-requisicao-get-post-arquivos/)
- [Voltar para Sistemas Web](../../)
- [Proxima aula: PHP (parte 13) - Criptografia: password_hash](../../etapa-3/php-parte-13-criptografia-password-hash/)
