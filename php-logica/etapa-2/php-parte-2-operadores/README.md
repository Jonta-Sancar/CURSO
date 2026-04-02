# PHP (parte 2) - Operadores

> Modulo: Logica

## Objetivo da aula
Conhecer e aplicar os operadores aritmeticos, relacionais, logicos e de atribuicao do PHP.

## Exemplo rapido
```php
<?php

$a = 10;
$b = 3;

echo $a + $b . PHP_EOL;  // 13
echo $a % $b . PHP_EOL;  // 1 (resto da divisao)
echo $a ** $b . PHP_EOL; // 1000 (potenciacao)

var_dump($a > $b);        // bool(true)
var_dump($a === "10");    // bool(false) — tipo diferente
```

## Operadores aritmeticos

| Operador | Operacao | Exemplo | Resultado |
|----------|----------|---------|-----------|
| `+` | Adicao | `5 + 3` | `8` |
| `-` | Subtracao | `5 - 3` | `2` |
| `*` | Multiplicacao | `5 * 3` | `15` |
| `/` | Divisao | `10 / 4` | `2.5` |
| `%` | Modulo (resto) | `10 % 3` | `1` |
| `**` | Potenciacao | `2 ** 8` | `256` |

## Operadores de atribuicao

| Operador | Equivale a |
|----------|------------|
| `$x = 5` | atribuicao simples |
| `$x += 3` | `$x = $x + 3` |
| `$x -= 2` | `$x = $x - 2` |
| `$x *= 4` | `$x = $x * 4` |
| `$x /= 2` | `$x = $x / 2` |
| `$x %= 3` | `$x = $x % 3` |
| `$x .= " texto"` | `$x = $x . " texto"` (concatenacao) |

```php
<?php

$total = 100;
$total += 50; // 150
$total -= 20; // 130
echo $total . PHP_EOL;

$frase = "Ola";
$frase .= ", mundo!";
echo $frase . PHP_EOL; // Ola, mundo!
```

## Operadores relacionais (comparacao)

Retornam `true` ou `false`.

| Operador | Significado | Exemplo | Resultado |
|----------|-------------|---------|-----------|
| `==` | Igual (valor) | `"5" == 5` | `true` |
| `===` | Identico (valor e tipo) | `"5" === 5` | `false` |
| `!=` | Diferente (valor) | `3 != 4` | `true` |
| `!==` | Nao identico | `"5" !== 5` | `true` |
| `>` | Maior que | `7 > 3` | `true` |
| `<` | Menor que | `2 < 1` | `false` |
| `>=` | Maior ou igual | `5 >= 5` | `true` |
| `<=` | Menor ou igual | `4 <= 3` | `false` |

> Prefira sempre `===` e `!==` para evitar comparacoes inesperadas por conversao de tipo.

## Operadores logicos

| Operador | Significado | Exemplo |
|----------|-------------|---------|
| `&&` ou `and` | E logico | `$a && $b` |
| `||` ou `or` | OU logico | `$a || $b` |
| `!` | Negacao | `!$a` |

```php
<?php

$idade = 20;
$tem_documento = true;

var_dump($idade >= 18 && $tem_documento); // bool(true)
var_dump($idade < 18 || $tem_documento);  // bool(true)
var_dump(!$tem_documento);               // bool(false)
```

## Operadores de incremento e decremento

```php
<?php

$contador = 0;
$contador++;  // incrementa 1 (pos-incremento)
$contador--;  // decrementa 1 (pos-decremento)
++$contador;  // pre-incremento
--$contador;  // pre-decremento

echo $contador . PHP_EOL;
```

## Pratica sugerida (exercicio concreto)
### Projeto: Calculadora de desconto via terminal
Crie um script que calcula o preco final de um produto com desconto.

### Requisitos obrigatorios
1. Solicite via `readline`: nome do produto, preco original (float) e percentual de desconto (int).
2. Calcule o valor do desconto: `$preco * ($desconto / 100)`.
3. Calcule o preco final: `$preco - $valor_desconto`.
4. Exiba: nome do produto, preco original, valor descontado e preco final.
5. Exiba tambem uma mensagem condicional: se o desconto for maior que 30%, escreva "Promocao especial!".
6. Use `var_dump` para inspecionar o resultado da comparacao do item 5.

### Regras de validacao
- Use operadores aritmeticos para todos os calculos (nao calcule manualmente).
- Use `===` na comparacao do desconto especial, nao `==`.
- O script deve rodar via terminal com `php calculadora.php`.

### Entrega esperada
- Arquivo `calculadora.php` na pasta da aula.

## Desafio opcional
Adicione uma segunda comparacao: verifique se o preco final e menor que 50 **E** o desconto e maior que 10. Use operador logico `&&` e exiba o resultado com `var_dump`.

## Navegacao
- [Aula anterior: PHP (parte 1) - Tipos de valores, variaveis e constantes](../php-parte-1-tipos-de-valores-variaveis-e-constantes/)
- [Voltar para Logica](../../)
- [Proxima aula: PHP (parte 3) - Condicionais: if, else, ternarios, switch](../php-parte-3-condicionais-if-else-ternarios-switch/)
