# PHP (parte 13) - Criptografia: password_hash

> Modulo: Sistemas Web

## Objetivo da aula
Entender por que senhas nao devem ser armazenadas em texto puro, e aprender a usar as funcoes nativas do PHP `password_hash()` e `password_verify()` para armazenar e validar senhas de forma segura.

## Por que nao armazenar senhas em texto puro
Se o banco de dados for comprometido, o atacante tera acesso direto a todas as senhas. Como usuarios reutilizam senhas em varios servicos, isso causa dano muito alem da sua aplicacao.

### Abordagens incorretas (nao use)
```php
// Texto puro — nunca faca isso
$senha = $_POST['senha'];

// MD5 ou SHA1 — sao funcoes de hash, nao de senha; sao rapidas demais
$senha = md5($_POST['senha']);
$senha = sha1($_POST['senha']);
```

MD5 e SHA1 sao algoritmos projetados para ser **rapidos** — o que e otimo para checksum de arquivos, mas pessimo para senhas, pois facilita ataques de forca bruta.

---

## password_hash()

`password_hash()` cria um hash seguro usando um algoritmo lento por design (bcrypt por padrao), com um **salt** aleatorio embutido automaticamente.

### Sintaxe
```php
string password_hash(string $password, int|string|null $algo, array $options = [])
```

### Uso basico
```php
$senhaDigitada = $_POST['senha'];
$hash = password_hash($senhaDigitada, PASSWORD_DEFAULT);

// $hash tem aparencia similar a:
// $2y$10$AbCdEfGhIjKlMnOpQrStUuVwXyZ0123456789...
```

### Algoritmos disponiveis

| Constante           | Algoritmo | Observacao                              |
|---------------------|-----------|------------------------------------------|
| `PASSWORD_DEFAULT`  | bcrypt    | Recomendado — atualiza automaticamente  |
| `PASSWORD_BCRYPT`   | bcrypt    | Explicito; custo padrao = 10            |
| `PASSWORD_ARGON2I`  | Argon2i   | Requer extensao; mais moderno           |
| `PASSWORD_ARGON2ID` | Argon2id  | Versao mais segura do Argon2            |

### Ajustando o custo (bcrypt)
O custo define quantas iteracoes o algoritmo realiza. Valores maiores = mais lento = mais seguro.

```php
$hash = password_hash($senha, PASSWORD_BCRYPT, ['cost' => 12]);
```

> Recomendacao pratica: escolha o custo mais alto que nao deixe o login perceptivelmente lento (tipicamente entre 10 e 12).

---

## password_verify()

Compara uma senha digitada com o hash armazenado.

### Sintaxe
```php
bool password_verify(string $password, string $hash)
```

### Uso
```php
$senhaDigitada = $_POST['senha'];
$hashNoBanco   = $usuario['senha']; // vindo do SELECT no banco

if (password_verify($senhaDigitada, $hashNoBanco)) {
    echo "Login autorizado.";
} else {
    echo "Senha incorreta.";
}
```

> `password_verify()` ja e resistente a timing attacks — nao precisa de comparacao extra.

---

## Fluxo completo: cadastro e login

### Cadastro
```php
// cadastro.php
require_once 'conexao.php';

$nome  = trim($_POST['nome']);
$email = trim($_POST['email']);
$senha = $_POST['senha'];

if (strlen($senha) < 8) {
    echo "A senha deve ter pelo menos 8 caracteres.";
    exit;
}

$hash = password_hash($senha, PASSWORD_DEFAULT);

$pdo  = conectar();
$stmt = $pdo->prepare("INSERT INTO usuarios (nome, email, senha) VALUES (:nome, :email, :senha)");
$stmt->execute([':nome' => $nome, ':email' => $email, ':senha' => $hash]);

echo "Cadastro realizado.";
```

### Login
```php
// login.php
require_once 'conexao.php';

$email = trim($_POST['email']);
$senha = $_POST['senha'];

$pdo  = conectar();
$stmt = $pdo->prepare("SELECT * FROM usuarios WHERE email = :email");
$stmt->execute([':email' => $email]);
$usuario = $stmt->fetch();

if (!$usuario || !password_verify($senha, $usuario['senha'])) {
    echo "E-mail ou senha incorretos.";
    exit;
}

echo "Bem-vindo, " . htmlspecialchars($usuario['nome']);
```

---

## password_needs_rehash()

Quando voce aumenta o custo ou muda de algoritmo, hashes antigos precisam ser atualizados. O PHP oferece uma funcao para verificar isso no momento do login (quando a senha original esta disponivel).

```php
if (password_verify($senhaDigitada, $hashNoBanco)) {

    if (password_needs_rehash($hashNoBanco, PASSWORD_DEFAULT, ['cost' => 12])) {
        $novoHash = password_hash($senhaDigitada, PASSWORD_DEFAULT, ['cost' => 12]);
        // atualizar o hash no banco
        $stmt = $pdo->prepare("UPDATE usuarios SET senha = :senha WHERE id = :id");
        $stmt->execute([':senha' => $novoHash, ':id' => $usuario['id']]);
    }

    // prosseguir com o login
}
```

---

## Resumo das funcoes

| Funcao                    | Quando usar                                      |
|---------------------------|--------------------------------------------------|
| `password_hash()`         | Ao cadastrar ou redefinir a senha do usuario     |
| `password_verify()`       | Ao fazer login — comparar senha com hash         |
| `password_needs_rehash()` | No login — verificar se o hash precisa ser atualizado |

---

## Pratica sugerida (exercicio concreto)
### Projeto: Sistema de cadastro e login seguro

### Requisitos obrigatorios
1. Crie uma tabela `usuarios` com `id`, `nome`, `email`, `senha`.
2. Implemente `cadastro.php` com formulario POST que valida os campos e salva a senha com `password_hash()`.
3. Implemente `login.php` que busca o usuario pelo e-mail e usa `password_verify()` para validar a senha.
4. Exiba mensagem de erro generica em caso de falha no login (nao informe se foi o e-mail ou a senha que estava errado).
5. Ao logar com sucesso, exiba uma mensagem de boas-vindas com o nome do usuario.

### Regras de validacao
- A senha deve ter no minimo 8 caracteres antes de gerar o hash.
- Nunca armazene a senha original — apenas o hash.
- Use prepared statements para todas as queries.

### Desafio opcional
Adicione `password_needs_rehash()` no fluxo de login e atualize o hash no banco se necessario.

---

## Navegacao
- [Aula anterior: PHP (parte 12) - PDO](../../etapa-2/php-parte-12-pdo/)
- [Voltar para Sistemas Web](../../)
- [Proxima aula: PHP (parte 14) - Cookies e Sessions](../php-parte-14-cookies-e-sessions/)
