# PHP (parte 11) - Metodos de requisicao: GET, POST, Arquivos

> Modulo: Sistemas Web

## Objetivo da aula
Entender como o PHP recebe dados vindos do navegador por meio dos metodos HTTP GET e POST, e como processar o envio de arquivos por formulario.

## O que e uma requisicao HTTP
Toda vez que um usuario acessa uma pagina ou envia um formulario, o navegador faz uma **requisicao HTTP** ao servidor. O servidor processa essa requisicao e devolve uma resposta (geralmente HTML).

Os dois metodos mais comuns sao:
- **GET**: envia dados pela URL (visivel na barra de endereco).
- **POST**: envia dados no corpo da requisicao (nao visivel na URL).

---

## GET

### Como funciona
Os dados sao enviados como parametros na URL:
```
https://site.com/busca.php?termo=php&pagina=2
```

### Acessando no PHP
```php
$termo  = $_GET['termo'];   // "php"
$pagina = $_GET['pagina'];  // "2"
```

### Formulario HTML com GET
```html
<form action="busca.php" method="get">
    <input type="text" name="termo" placeholder="Buscar...">
    <button type="submit">Buscar</button>
</form>
```

### Quando usar GET
- Buscas e filtros (o resultado pode ser compartilhado via URL).
- Navegacao paginada.
- Qualquer operacao de **leitura** que nao altere dados.

### Limitacoes
- Dados ficam visiveis na URL — nao use para senhas ou informacoes sensiveis.
- Limite de tamanho na URL (aprox. 2000 caracteres dependendo do navegador).

---

## POST

### Como funciona
Os dados sao enviados no corpo da requisicao HTTP, ficando ocultos da URL.

### Acessando no PHP
```php
$nome  = $_POST['nome'];
$email = $_POST['email'];
```

### Formulario HTML com POST
```html
<form action="cadastro.php" method="post">
    <input type="text"  name="nome"  placeholder="Seu nome">
    <input type="email" name="email" placeholder="Seu e-mail">
    <button type="submit">Cadastrar</button>
</form>
```

### Quando usar POST
- Envio de dados sensiveis (senhas, tokens).
- Operacoes que **criam ou alteram** dados (cadastro, login, edicao).
- Envio de arquivos.

---

## Verificando o metodo da requisicao

```php
if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    // processar formulario
}

if ($_SERVER['REQUEST_METHOD'] === 'GET') {
    // exibir pagina normalmente
}
```

---

## Validacao basica de entrada

Nunca confie diretamente no que vem do usuario. Sempre valide e limpe os dados:

```php
// verificar se o campo existe e nao esta vazio
if (empty($_POST['nome'])) {
    echo "Nome e obrigatorio.";
    exit;
}

// remover espacos extras e tags HTML
$nome = trim(strip_tags($_POST['nome']));
```

| Funcao           | O que faz                                      |
|------------------|------------------------------------------------|
| `trim()`         | Remove espacos no inicio e fim da string       |
| `strip_tags()`   | Remove tags HTML/PHP da string                 |
| `htmlspecialchars()` | Converte caracteres especiais em entidades HTML |
| `intval()`       | Converte para inteiro                          |
| `filter_input()` | Filtra e valida entradas com filtros nativos   |

---

## Upload de arquivos

### Formulario HTML
O atributo `enctype="multipart/form-data"` e **obrigatorio** para envio de arquivos.

```html
<form action="upload.php" method="post" enctype="multipart/form-data">
    <input type="file" name="imagem">
    <button type="submit">Enviar</button>
</form>
```

### Processando no PHP com `$_FILES`
```php
$arquivo = $_FILES['imagem'];

echo $arquivo['name'];     // nome original do arquivo
echo $arquivo['type'];     // tipo MIME: "image/jpeg"
echo $arquivo['size'];     // tamanho em bytes
echo $arquivo['tmp_name']; // caminho temporario no servidor
echo $arquivo['error'];    // codigo de erro (0 = sem erro)
```

### Movendo o arquivo para o destino final
```php
$destino = 'uploads/' . basename($arquivo['name']);

if (move_uploaded_file($arquivo['tmp_name'], $destino)) {
    echo "Arquivo salvo em: " . $destino;
} else {
    echo "Erro ao salvar o arquivo.";
}
```

### Validacoes essenciais para upload
```php
$extensoesPermitidas = ['jpg', 'jpeg', 'png', 'pdf'];
$extensao = strtolower(pathinfo($arquivo['name'], PATHINFO_EXTENSION));

if (!in_array($extensao, $extensoesPermitidas)) {
    echo "Tipo de arquivo nao permitido.";
    exit;
}

$tamanhoMaximo = 2 * 1024 * 1024; // 2 MB
if ($arquivo['size'] > $tamanhoMaximo) {
    echo "Arquivo muito grande.";
    exit;
}

if ($arquivo['error'] !== UPLOAD_ERR_OK) {
    echo "Erro no upload.";
    exit;
}
```

---

## Resumo comparativo

| Caracteristica     | GET                        | POST                        |
|--------------------|----------------------------|-----------------------------|
| Visibilidade       | Dados na URL               | Dados ocultos               |
| Tamanho dos dados  | Limitado (~2000 chars)     | Sem limite pratico          |
| Cache / historico  | Sim (URL fica no historico)| Nao                         |
| Uso tipico         | Busca, filtros, leitura    | Login, cadastro, upload     |
| Seguranca          | Menor (dados expostos)     | Maior para dados sensiveis  |

---

## Pratica sugerida (exercicio concreto)
### Projeto: Formulario de contato com upload

### Requisitos obrigatorios
1. Crie um formulario HTML com os campos: nome, e-mail, mensagem e um campo de arquivo (anexo).
2. O formulario deve usar `method="post"` e `enctype="multipart/form-data"`.
3. No PHP, valide que nenhum campo esta vazio antes de processar.
4. Exiba os dados enviados de volta ao usuario apos o envio (sem redirecionar).
5. Aceite apenas arquivos `.pdf` ou `.png` com no maximo 1 MB.
6. Mova o arquivo para uma pasta `uploads/` e exiba o caminho final.

### Regras de validacao
- Nao exibir dados brutos do `$_POST` — use `htmlspecialchars()` ao imprimir.
- O script deve verificar `$_SERVER['REQUEST_METHOD']` antes de processar.
- A pasta `uploads/` deve existir (crie manualmente ou com `mkdir` no PHP).

### Desafio opcional
Renomeie o arquivo enviado para um nome gerado com `uniqid()` antes de salva-lo, evitando colisoes de nomes.

---

## Navegacao
- [Voltar para Sistemas Web](../../)
- [Proxima aula: PHP (parte 12) - PDO](../../etapa-2/php-parte-12-pdo/)
