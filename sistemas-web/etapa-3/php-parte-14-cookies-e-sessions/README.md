# PHP (parte 14) - Cookies e Sessions

> Modulo: Sistemas Web

## Objetivo da aula
Entender como o HTTP mantem estado entre requisicoes usando cookies e sessions, e aprender a usar ambos no PHP para controle de acesso e persistencia de dados do usuario.

## O problema: HTTP e stateless
O protocolo HTTP nao guarda memoria entre requisicoes. Cada pagina acessada e uma nova requisicao independente — o servidor nao sabe, por padrao, que o usuario da requisicao anterior e o mesmo.

Para resolver isso, existem dois mecanismos principais: **cookies** e **sessions**.

---

## Cookies

Um cookie e um pequeno dado armazenado **no navegador do usuario**. O servidor envia o cookie, o navegador o guarda e o reenvia automaticamente em todas as requisicoes futuras para aquele dominio.

### Criando um cookie
```php
// setcookie(nome, valor, expiracao, caminho, dominio, seguro, httponly)
setcookie('tema', 'escuro', time() + (7 * 24 * 3600)); // expira em 7 dias
```

> `setcookie()` deve ser chamado **antes** de qualquer saida HTML (antes de `echo`, `?>`, etc.).

### Lendo um cookie
```php
if (isset($_COOKIE['tema'])) {
    echo $_COOKIE['tema']; // "escuro"
}
```

### Apagando um cookie
Para apagar um cookie, defina sua expiracao no passado:
```php
setcookie('tema', '', time() - 3600);
```

### Parametros de setcookie()

| Parametro   | Tipo    | Descricao                                                      |
|-------------|---------|----------------------------------------------------------------|
| `name`      | string  | Nome do cookie                                                 |
| `value`     | string  | Valor armazenado                                               |
| `expires`   | int     | Timestamp Unix de expiracao (0 = ate fechar o navegador)       |
| `path`      | string  | Caminho no servidor em que o cookie esta disponivel (`'/'`)    |
| `domain`    | string  | Dominio ao qual o cookie pertence                              |
| `secure`    | bool    | Enviar apenas via HTTPS                                        |
| `httponly`  | bool    | Impede acesso via JavaScript (protege contra XSS)              |

### Boas praticas com cookies
```php
setcookie(
    'usuario_id',
    $id,
    time() + (30 * 24 * 3600), // 30 dias
    '/',
    '',
    true,  // secure: apenas HTTPS
    true   // httponly: inacessivel via JS
);
```

### Limitacoes dos cookies
- Armazenados no cliente — podem ser lidos e modificados pelo usuario.
- Nao armazene dados sensiveis (senhas, permissoes) diretamente em cookies.
- Limite de tamanho: aprox. 4 KB por cookie.

---

## Sessions

Uma session armazena dados **no servidor**. O navegador recebe apenas um ID de session (via cookie chamado `PHPSESSID`), e o servidor associa esse ID aos dados do usuario.

### Iniciando uma session
```php
session_start(); // deve ser a primeira instrucao do arquivo
```

> `session_start()` tambem deve ser chamado antes de qualquer saida HTML.

### Gravando dados na session
```php
session_start();

$_SESSION['usuario_id']   = 42;
$_SESSION['usuario_nome'] = 'Ana';
$_SESSION['logado']       = true;
```

### Lendo dados da session
```php
session_start();

if (isset($_SESSION['logado']) && $_SESSION['logado'] === true) {
    echo "Bem-vindo, " . htmlspecialchars($_SESSION['usuario_nome']);
}
```

### Removendo um dado especifico
```php
unset($_SESSION['carrinho']);
```

### Encerrando a session completamente (logout)
```php
session_start();
session_unset();   // limpa todos os dados da $_SESSION
session_destroy(); // destroi a session no servidor

// Apagar o cookie de session no navegador
setcookie(session_name(), '', time() - 3600, '/');

header('Location: login.php');
exit;
```

---

## Fluxo de autenticacao com sessions

### login.php
```php
<?php
session_start();
require_once 'conexao.php';

if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    $email = trim($_POST['email']);
    $senha = $_POST['senha'];

    $pdo  = conectar();
    $stmt = $pdo->prepare("SELECT * FROM usuarios WHERE email = :email");
    $stmt->execute([':email' => $email]);
    $usuario = $stmt->fetch();

    if ($usuario && password_verify($senha, $usuario['senha'])) {
        $_SESSION['usuario_id']   = $usuario['id'];
        $_SESSION['usuario_nome'] = $usuario['nome'];
        $_SESSION['logado']       = true;

        header('Location: painel.php');
        exit;
    }

    $erro = "E-mail ou senha incorretos.";
}
?>
```

### painel.php (pagina protegida)
```php
<?php
session_start();

if (!isset($_SESSION['logado']) || $_SESSION['logado'] !== true) {
    header('Location: login.php');
    exit;
}
?>
<h1>Ola, <?= htmlspecialchars($_SESSION['usuario_nome']) ?></h1>
<a href="logout.php">Sair</a>
```

### logout.php
```php
<?php
session_start();
session_unset();
session_destroy();
setcookie(session_name(), '', time() - 3600, '/');
header('Location: login.php');
exit;
```

---

## Cookies vs Sessions

| Caracteristica         | Cookie                              | Session                              |
|------------------------|-------------------------------------|--------------------------------------|
| Local de armazenamento | Navegador do usuario                | Servidor                             |
| Acessivel pelo usuario | Sim (pode ser lido/modificado)      | Nao (apenas o ID fica no navegador)  |
| Tamanho maximo         | ~4 KB                               | Limitado pelo servidor               |
| Expiracao              | Definida pelo programador           | Expira ao fechar o navegador (padrao)|
| Uso tipico             | Preferencias, "lembrar-me"          | Login, carrinho, dados temporarios   |
| Seguranca              | Menor (dados no cliente)            | Maior (dados no servidor)            |

---

## Pratica sugerida (exercicio concreto)
### Projeto: Sistema de login com session e preferencia de tema com cookie

### Requisitos obrigatorios
1. Crie `login.php`, `painel.php` e `logout.php` usando o fluxo de session descrito acima.
2. Ao logar, redirecione para `painel.php`.
3. `painel.php` deve redirecionar para `login.php` se o usuario nao estiver logado.
4. Adicione em `painel.php` um formulario que permita ao usuario escolher entre tema claro e escuro.
5. Salve a preferencia de tema em um cookie com validade de 30 dias.
6. Ao carregar qualquer pagina, leia o cookie e aplique a classe CSS correspondente no `<body>`.

### Regras de validacao
- O logout deve destruir a session e apagar o cookie `PHPSESSID`.
- `session_start()` deve aparecer antes de qualquer saida HTML em todos os arquivos.
- Use `httponly: true` ao criar o cookie de tema.

### Desafio opcional
Implemente um "lembrar-me" no login: se marcado, salve o `usuario_id` em um cookie de longa duracao (30 dias) e use-o para iniciar a session automaticamente em visitas futuras.

---

## Navegacao
- [Aula anterior: PHP (parte 13) - Criptografia: password_hash](../php-parte-13-criptografia-password-hash/)
- [Voltar para Sistemas Web](../../)
