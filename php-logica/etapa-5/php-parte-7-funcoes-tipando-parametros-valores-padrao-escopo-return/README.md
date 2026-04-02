# PHP (parte 7) - Funcoes: tipando parametros, valores padrao, escopo, return

> Modulo: Logica

## Objetivo da aula
Criar funcoes reutilizaveis em PHP com tipagem de parametros, valores padrao, retorno tipado e compreender o escopo de variaveis.

## Exemplo rapido
```php
<?php

function saudar(string $nome, string $saudacao = "Ola"): string {
    return "$saudacao, $nome!";
}

echo saudar("Maria") . PHP_EOL;          // Ola, Maria!
echo saudar("Pedro", "Bom dia") . PHP_EOL; // Bom dia, Pedro!
```

## Declarando funcoes

```php
function nome_da_funcao(parametros): tipo_retorno {
    // corpo
    return valor;
}
```

```php
<?php

function somar(int $a, int $b): int {
    return $a + $b;
}

$resultado = somar(5, 3);
echo $resultado . PHP_EOL; // 8
```

## Tipando parametros

PHP suporta declaracao de tipos nos parametros. Se um valor incompativel for passado, um erro e lancado.

```php
<?php

function calcular_area(float $largura, float $altura): float {
    return $largura * $altura;
}

echo calcular_area(3.5, 2.0) . PHP_EOL; // 7
```

Tipos disponiveis para parametros e retorno: `int`, `float`, `string`, `bool`, `array`, `void`, `mixed`, `?tipo` (nullable).

```php
<?php

function buscar_usuario(int $id): ?string {
    // retorna null se nao encontrado
    $usuarios = [1 => "Ana", 2 => "Bruno"];
    return $usuarios[$id] ?? null;
}

var_dump(buscar_usuario(1));  // string(3) "Ana"
var_dump(buscar_usuario(99)); // NULL
```

## Valores padrao (parametros opcionais)

Parametros com valor padrao sao opcionais na chamada. Devem vir sempre **apos** os obrigatorios.

```php
<?php

function formatar_preco(float $valor, int $casas = 2, string $moeda = "R$"): string {
    return $moeda . " " . number_format($valor, $casas, ',', '.');
}

echo formatar_preco(1299.9) . PHP_EOL;         // R$ 1.299,90
echo formatar_preco(1299.9, 0) . PHP_EOL;      // R$ 1.300
echo formatar_preco(49.99, 2, "US$") . PHP_EOL; // US$ 49,99
```

## Escopo de variaveis

Variaveis declaradas **dentro** de uma funcao existem apenas naquele escopo — nao sao visiveis fora. Variaveis externas nao sao acessiveis dentro da funcao sem uso de `global` (evite `global`; prefira passar por parametro).

```php
<?php

$mensagem = "Ola do escopo global";

function exibir(): void {
    // $mensagem nao existe aqui
    $local = "Ola do escopo local";
    echo $local . PHP_EOL;
}

exibir();
// echo $local; // erro: variavel nao definida no escopo global
```

### Passagem por valor vs por referencia

Por padrao, PHP copia o valor ao passar para a funcao (passagem por valor). Use `&` para passar por referencia e modificar a variavel original.

```php
<?php

function dobrar_valor(float &$numero): void {
    $numero *= 2;
}

$preco = 50.0;
dobrar_valor($preco);
echo $preco . PHP_EOL; // 100
```

> Use referencia com moderacao. Na maioria dos casos, retornar o valor novo e mais legivel.

## return

- Toda funcao pode (ou deve) retornar um valor com `return`.
- Funcoes com tipo de retorno `void` nao retornam nada.
- `return` encerra a execucao da funcao imediatamente.

```php
<?php

function validar_idade(int $idade): bool {
    if ($idade < 0 || $idade > 150) {
        return false;
    }
    return true;
}

var_dump(validar_idade(25));   // bool(true)
var_dump(validar_idade(-1));   // bool(false)
```

## Pratica sugerida (exercicio concreto)
### Projeto: Biblioteca de calculos via terminal
Crie um script com um conjunto de funcoes utilitarias e um menu interativo.

### Requisitos obrigatorios
1. Crie as seguintes funcoes com tipagem completa (parametros e retorno):
   - `calcular_media(array $notas): float` — retorna a media das notas.
   - `classificar_media(float $media): string` — retorna "Aprovado", "Recuperacao" ou "Reprovado".
   - `formatar_resultado(string $nome, float $media, string $classificacao): string` — retorna uma string formatada com o resultado.
2. Crie um menu via terminal com: 1) Calcular resultado de aluno | 2) Sair.
3. Na opcao 1, leia nome e 3 notas, use as funcoes para calcular e exiba o resultado formatado.
4. Use `valores padrao` em pelo menos um parametro de alguma funcao.

### Regras de validacao
- Todas as funcoes devem ter tipos declarados nos parametros e no retorno.
- Nenhuma funcao deve usar `echo` internamente — apenas retornar valores.
- O menu deve usar `while` e `switch`.

### Entrega esperada
- Arquivo `calculos.php` na pasta da aula.

## Desafio opcional
Adicione a funcao `calcular_desvio_padrao(array $notas): float` que calcula o desvio padrao do conjunto de notas e exiba-o junto ao resultado de cada aluno.

## Navegacao
- [Aula anterior: PHP (parte 6) - Foreach](../../etapa-4/php-parte-6-foreach/)
- [Voltar para Logica](../../)
- [Proxima etapa: PHP (parte 8) - Classes e Objetos](../../etapa-6/php-parte-8-classes-e-objetos-propriedades-tipagem-metodos-construtores-this/)
