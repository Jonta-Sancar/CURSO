# PHP (parte 3) - Condicionais: if, else, ternarios, switch

> Modulo: Logica

## Objetivo da aula
Controlar o fluxo de execucao de um script PHP com base em condicoes usando `if`, `else`, `elseif`, operador ternario e `switch`.

## Exemplo rapido
```php
<?php

$nota = 7;

if ($nota >= 7) {
    echo "Aprovado" . PHP_EOL;
} elseif ($nota >= 5) {
    echo "Recuperacao" . PHP_EOL;
} else {
    echo "Reprovado" . PHP_EOL;
}
```

## if / else / elseif

```php
<?php

$hora = (int) readline("Informe a hora atual (0-23): ");

if ($hora < 12) {
    echo "Bom dia!" . PHP_EOL;
} elseif ($hora < 18) {
    echo "Boa tarde!" . PHP_EOL;
} else {
    echo "Boa noite!" . PHP_EOL;
}
```

### Regras
- A condicao do `if` e avaliada como `bool`.
- Valores considerados `false`: `0`, `0.0`, `""`, `"0"`, `[]`, `null`.
- Tudo o mais e considerado `true`.

## Operador ternario

Forma compacta de um `if/else` simples.

```
$variavel = (condicao) ? valor_se_verdadeiro : valor_se_falso;
```

```php
<?php

$idade = 17;
$acesso = ($idade >= 18) ? "permitido" : "negado";
echo "Acesso: " . $acesso . PHP_EOL;
```

### Ternario nulo (`??`)
Retorna o primeiro valor se ele nao for `null`; caso contrario, retorna o segundo.

```php
<?php

$nome = readline("Nome (ou deixe em branco): ");
$exibir = $nome !== "" ? $nome : "Anonimo";

// equivalente com ??
$exibir = $nome ?: "Anonimo";

echo "Ola, " . $exibir . PHP_EOL;
```

## switch

Compara uma expressao com multiplos casos possíveis.

```php
<?php

$dia = (int) readline("Informe o numero do dia da semana (1-7): ");

switch ($dia) {
    case 1:
        echo "Domingo" . PHP_EOL;
        break;
    case 2:
        echo "Segunda-feira" . PHP_EOL;
        break;
    case 3:
        echo "Terca-feira" . PHP_EOL;
        break;
    case 4:
        echo "Quarta-feira" . PHP_EOL;
        break;
    case 5:
        echo "Quinta-feira" . PHP_EOL;
        break;
    case 6:
        echo "Sexta-feira" . PHP_EOL;
        break;
    case 7:
        echo "Sabado" . PHP_EOL;
        break;
    default:
        echo "Dia invalido." . PHP_EOL;
}
```

> `break` e obrigatorio para impedir que a execucao "caia" para o proximo caso (fall-through).  
> `default` e executado quando nenhum `case` corresponde — equivale ao `else`.

### Quando usar switch vs if
- Use `switch` quando comparar **uma mesma expressao** contra varios valores fixos.
- Use `if/elseif` quando as condicoes envolverem intervalos, comparacoes diferentes ou logica complexa.

## Pratica sugerida (exercicio concreto)
### Projeto: Classificador de IMC via terminal
Crie um script que calcula e classifica o IMC de uma pessoa.

### Requisitos obrigatorios
1. Solicite via `readline`: nome, peso (float) e altura (float).
2. Calcule o IMC: `$peso / ($altura ** 2)`.
3. Classifique o resultado com `if/elseif/else`:
   - Menor que 18.5: "Abaixo do peso"
   - Entre 18.5 e 24.9: "Peso normal"
   - Entre 25 e 29.9: "Sobrepeso"
   - 30 ou mais: "Obesidade"
4. Exiba: nome, IMC formatado com 2 casas decimais (`number_format($imc, 2)`) e classificacao.
5. Use o operador ternario para exibir uma mensagem extra: se IMC for normal, exiba "Parabens!"; caso contrario, exiba "Consulte um profissional de saude.".

### Regras de validacao
- Nao use `switch` para a classificacao (use `if/elseif`).
- O ternario deve ser uma expressao valida, nao um `if` disfarcado.
- O script deve funcionar para diferentes entradas sem erros.

### Entrega esperada
- Arquivo `imc.php` na pasta da aula.

## Desafio opcional
Adicione um `switch` que, com base na classificacao (string), define uma cor de alerta:
- "Abaixo do peso" → "azul"
- "Peso normal" → "verde"
- "Sobrepeso" → "amarelo"
- "Obesidade" → "vermelho"

Exiba a cor junto ao resultado.

## Navegacao
- [Aula anterior: PHP (parte 2) - Operadores](../php-parte-2-operadores/)
- [Voltar para Logica](../../)
- [Proxima etapa: PHP (parte 4) - Lacos](../../etapa-3/php-parte-4-lacos-while-for-continue-break-acumulador-iterador/)
