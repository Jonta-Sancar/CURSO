# PHP (parte 1) - Tipos de valores, variaveis e constantes

> Modulo: Logica

## Objetivo da aula
Conhecer os tipos de dados fundamentais do PHP, declarar variaveis e constantes, e inspecionar valores via terminal.

## Exemplo rapido
```php
<?php

$nome = "Maria";
$idade = 25;
$altura = 1.68;
$ativo = true;

echo $nome . PHP_EOL;
var_dump($idade);
var_dump($ativo);
```

> Todas as aulas desta etapa devem ser executadas via terminal usando `php arquivo.php`.

## Tipos escalares

| Tipo | Exemplo | Descricao |
|------|---------|-----------|
| `int` | `42`, `-7` | Numeros inteiros |
| `float` | `3.14`, `-0.5` | Numeros decimais |
| `string` | `"ola"`, `'mundo'` | Texto |
| `bool` | `true`, `false` | Verdadeiro ou falso |
| `null` | `null` | Ausencia de valor |

## Variaveis

Em PHP, variaveis comecam sempre com `$` e nao precisam de declaracao de tipo (tipagem dinamica por padrao).

```php
<?php

$produto = "Teclado";
$preco = 199.90;
$disponivel = true;
$descricao = null;

var_dump($produto);    // string(7) "Teclado"
var_dump($preco);      // float(199.9)
var_dump($disponivel); // bool(true)
var_dump($descricao);  // NULL
```

### Regras de nomenclatura
- Comecar com `$` seguido de letra ou underscore: `$nome`, `$_interno`.
- Case-sensitive: `$Nome` e `$nome` sao variaveis diferentes.
- Usar snake_case por convencao: `$nome_completo`, `$data_nascimento`.

## Constantes

Constantes armazenam valores fixos que nao podem ser reatribuidos apos a definicao.

### `define()`
```php
<?php

define('VERSAO', '1.0.0');
define('PI', 3.14159);

echo VERSAO . PHP_EOL; // 1.0.0
echo PI . PHP_EOL;     // 3.14159
```

### `const`
```php
<?php

const LIMITE_TENTATIVAS = 3;
const APP_NOME = 'MeuSistema';

echo LIMITE_TENTATIVAS . PHP_EOL;
```

> Diferencas praticas: `const` e avaliado em tempo de compilacao e deve ficar no escopo global ou de classe. `define()` pode ser usado dentro de condicionais e funcoes.

## Inspecionando valores

| Funcao | Uso |
|--------|-----|
| `echo` | Exibe um valor simples |
| `var_dump()` | Exibe tipo e valor (ideal para debug) |
| `print_r()` | Exibe estruturas de forma legivel (util para arrays) |
| `gettype()` | Retorna o nome do tipo como string |

```php
<?php

$x = 42;
echo gettype($x) . PHP_EOL; // integer
var_dump($x);               // int(42)
```

## Entrada de dados pelo terminal

```php
<?php

$nome = readline("Qual e o seu nome? ");
echo "Ola, " . $nome . "!" . PHP_EOL;
```

## Pratica sugerida (exercicio concreto)
### Projeto: Ficha de cadastro via terminal
Crie um script PHP que coleta dados do usuario pelo terminal e exibe um resumo.

### Requisitos obrigatorios
1. Solicite ao usuario (via `readline`): nome, idade e cidade.
2. Armazene cada dado em uma variavel com tipo adequado (string para nome e cidade, int para idade).
3. Defina uma constante `VERSAO` com o valor `'1.0'`.
4. Exiba um resumo formatado com `echo`, incluindo todos os dados coletados e a versao.
5. Apos o resumo, use `var_dump` para inspecionar cada variavel separadamente.

### Regras de validacao
- As variaveis devem ter nomes em snake_case.
- A constante deve ser definida com `define()` ou `const` antes de ser usada.
- O script deve ser executado via `php ficha.php` no terminal.

### Entrega esperada
- Arquivo `ficha.php` na pasta da aula.

## Desafio opcional
Adicione uma variavel `$ativo` do tipo `bool` e outra `$observacao` com valor `null`. Use `var_dump` em ambas e explique em um comentario PHP o que cada saida significa.

## Navegacao
- [Voltar para Logica](../../)
- [Proxima aula: PHP (parte 2) - Operadores](../php-parte-2-operadores/)
