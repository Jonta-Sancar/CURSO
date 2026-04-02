# PHP (parte 5) - Arrays

> Modulo: Logica

## Objetivo da aula
Criar e manipular arrays indexados, associativos e multidimensionais, e conhecer as principais funcoes nativas para trabalhar com eles.

## Exemplo rapido
```php
<?php

$frutas = ["maca", "banana", "laranja"];
$pessoa = ["nome" => "Ana", "idade" => 30];

echo $frutas[0] . PHP_EOL;         // maca
echo $pessoa["nome"] . PHP_EOL;    // Ana
echo count($frutas) . PHP_EOL;     // 3
```

## Array indexado

Elementos acessados por indice numerico, comecando em `0`.

```php
<?php

$cores = ["vermelho", "verde", "azul"];

echo $cores[0] . PHP_EOL; // vermelho
echo $cores[2] . PHP_EOL; // azul

// adicionar elemento ao final
$cores[] = "amarelo";

// total de elementos
echo count($cores) . PHP_EOL; // 4
```

## Array associativo

Elementos acessados por chaves de string (como um dicionario).

```php
<?php

$produto = [
    "nome"     => "Monitor",
    "preco"    => 1299.90,
    "estoque"  => 15,
    "ativo"    => true,
];

echo $produto["nome"] . PHP_EOL;   // Monitor
echo $produto["preco"] . PHP_EOL;  // 1299.9

// alterar um valor
$produto["estoque"] = 14;

// adicionar nova chave
$produto["categoria"] = "Informatica";

var_dump($produto);
```

## Array multidimensional

Array cujos elementos sao outros arrays.

```php
<?php

$alunos = [
    ["nome" => "Carlos", "nota" => 8.5],
    ["nome" => "Beatriz", "nota" => 9.0],
    ["nome" => "Diego",   "nota" => 6.5],
];

echo $alunos[0]["nome"] . PHP_EOL;  // Carlos
echo $alunos[1]["nota"] . PHP_EOL;  // 9
```

## Funcoes essenciais de array

| Funcao | O que faz |
|--------|-----------|
| `count($arr)` | Retorna o numero de elementos |
| `array_push($arr, $val)` | Adiciona elemento ao final |
| `array_pop($arr)` | Remove e retorna o ultimo elemento |
| `array_shift($arr)` | Remove e retorna o primeiro elemento |
| `array_unshift($arr, $val)` | Adiciona elemento no inicio |
| `in_array($val, $arr)` | Verifica se valor existe no array |
| `array_key_exists($key, $arr)` | Verifica se chave existe |
| `array_keys($arr)` | Retorna todas as chaves |
| `array_values($arr)` | Retorna todos os valores |
| `array_merge($a, $b)` | Une dois arrays |
| `sort($arr)` | Ordena array indexado (ascendente) |
| `rsort($arr)` | Ordena array indexado (descendente) |
| `asort($arr)` | Ordena array associativo pelos valores |
| `ksort($arr)` | Ordena array associativo pelas chaves |
| `implode($sep, $arr)` | Une elementos em uma string |
| `explode($sep, $str)` | Divide uma string em array |

```php
<?php

$numeros = [5, 2, 8, 1, 9, 3];
sort($numeros);
print_r($numeros); // [1, 2, 3, 5, 8, 9]

$tags = ["php", "git", "html"];
echo implode(", ", $tags) . PHP_EOL; // php, git, html

$linha = "joao;25;curitiba";
$dados = explode(";", $linha);
print_r($dados); // ["joao", "25", "curitiba"]
```

## Pratica sugerida (exercicio concreto)
### Projeto: Gerenciador de lista de tarefas via terminal
Crie um script que mantém uma lista de tarefas enquanto o usuario interage.

### Requisitos obrigatorios
1. Inicie com um array vazio `$tarefas = []`.
2. Exiba um menu com opcoes: 1) Adicionar tarefa | 2) Remover ultima | 3) Ver lista | 4) Sair.
3. Use um laco `while` para manter o menu ativo ate o usuario escolher "Sair".
4. Na opcao "Adicionar": leia o nome da tarefa com `readline` e adicione ao array.
5. Na opcao "Remover ultima": use `array_pop` e exiba o nome da tarefa removida.
6. Na opcao "Ver lista": exiba todas as tarefas com seus indices usando um laco.
7. Ao sair, exiba o total de tarefas restantes com `count`.

### Regras de validacao
- Nao usar `print_r` para exibir a lista — iterar manualmente com indice.
- O menu deve usar `switch` ou `if/elseif` para tratar cada opcao.
- A lista nao pode ficar negativa: verifique se ha elementos antes de remover.

### Entrega esperada
- Arquivo `tarefas.php` na pasta da aula.

## Desafio opcional
Transforme o array de tarefas em associativo, onde cada chave e um ID numerico e o valor e um array com `["descricao" => ..., "feita" => false]`. Adicione a opcao 5 para marcar uma tarefa como feita pelo ID.

## Navegacao
- [Aula anterior: PHP (parte 4) - Lacos](../../etapa-3/php-parte-4-lacos-while-for-continue-break-acumulador-iterador/)
- [Voltar para Logica](../../)
- [Proxima aula: PHP (parte 6) - Foreach](../php-parte-6-foreach/)
