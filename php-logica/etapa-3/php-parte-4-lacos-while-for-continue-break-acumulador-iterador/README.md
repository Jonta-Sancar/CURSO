# PHP (parte 4) - Lacos: while, for, continue, break, acumulador, iterador

> Modulo: Logica

## Objetivo da aula
Automatizar repeticoes com `while` e `for`, controlar o fluxo interno dos lacos com `continue` e `break`, e entender os padroes de acumulador e iterador.

## Exemplo rapido
```php
<?php

for ($i = 1; $i <= 5; $i++) {
    echo $i . PHP_EOL;
}

$soma = 0;
for ($i = 1; $i <= 10; $i++) {
    $soma += $i; // acumulador
}
echo "Soma: " . $soma . PHP_EOL; // 55
```

## while

Repete um bloco enquanto a condicao for verdadeira. Use quando nao se sabe antecipadamente quantas vezes o laco vai rodar.

```php
<?php

$tentativas = 0;
$senha_correta = "1234";

do {
    $entrada = readline("Digite a senha: ");
    $tentativas++;
} while ($entrada !== $senha_correta && $tentativas < 3);

if ($entrada === $senha_correta) {
    echo "Acesso liberado!" . PHP_EOL;
} else {
    echo "Muitas tentativas. Bloqueado." . PHP_EOL;
}
```

### while vs do-while
- `while`: testa a condicao **antes** de executar — pode nao executar nenhuma vez.
- `do-while`: executa **pelo menos uma vez**, depois testa a condicao.

```php
<?php

// while simples
$n = 1;
while ($n <= 5) {
    echo $n . PHP_EOL;
    $n++;
}
```

## for

Use quando se sabe exatamente quantas iteracoes serao feitas.

```php
for (inicializacao; condicao; incremento) {
    // corpo
}
```

```php
<?php

for ($i = 10; $i >= 1; $i--) {
    echo $i . PHP_EOL;
}
```

## continue

Pula para a proxima iteracao do laco sem executar o restante do bloco atual.

```php
<?php

for ($i = 1; $i <= 10; $i++) {
    if ($i % 2 === 0) {
        continue; // pula os pares
    }
    echo $i . PHP_EOL; // exibe so os impares
}
```

## break

Encerra o laco completamente.

```php
<?php

for ($i = 1; $i <= 100; $i++) {
    if ($i === 7) {
        break; // para ao encontrar 7
    }
    echo $i . PHP_EOL;
}
```

## Padrao: acumulador

Variavel inicializada fora do laco que acumula um valor a cada iteracao (soma, produto, contagem).

```php
<?php

$qtd = (int) readline("Quantos numeros deseja somar? ");
$soma = 0; // acumulador

for ($i = 1; $i <= $qtd; $i++) {
    $numero = (float) readline("Numero $i: ");
    $soma += $numero;
}

echo "Total: " . $soma . PHP_EOL;
echo "Media: " . ($soma / $qtd) . PHP_EOL;
```

## Padrao: iterador

Variavel que conta as iteracoes ou avanca por uma sequencia. O `$i` do `for` ja e um iterador, mas o padrao aparece tambem no `while`.

```php
<?php

$iterador = 0;
$limite = 5;

while ($iterador < $limite) {
    echo "Iteracao " . ($iterador + 1) . PHP_EOL;
    $iterador++;
}
```

## Pratica sugerida (exercicio concreto)
### Projeto: Analisador de numeros via terminal
Crie um script que leia uma sequencia de numeros e calcule estatisticas.

### Requisitos obrigatorios
1. Solicite via `readline` quantos numeros o usuario deseja informar.
2. Use um laco `for` para coletar cada numero.
3. Calcule e armazene: soma total, maior valor, menor valor e contagem de numeros pares.
4. Use `continue` para pular numeros negativos (nao incluir na soma nem na contagem de pares).
5. Use `break` para encerrar o laco se o usuario digitar `0` antes de completar a quantidade informada.
6. Ao final, exiba: soma, media, maior, menor e quantidade de pares.

### Regras de validacao
- O acumulador de soma deve ser inicializado como `0` fora do laco.
- `continue` e `break` devem ter uso real (nao apenas decorativo).
- O script deve funcionar corretamente mesmo que o usuario interrompa com `0`.

### Entrega esperada
- Arquivo `analisador.php` na pasta da aula.

## Desafio opcional
Adicione um segundo laco `while` que exibe a tabuada do numero com maior valor encontrado (de 1 a 10).

## Navegacao
- [Aula anterior: PHP (parte 3) - Condicionais](../../etapa-2/php-parte-3-condicionais-if-else-ternarios-switch/)
- [Voltar para Logica](../../)
- [Proxima etapa: PHP (parte 5) - Arrays](../../etapa-4/php-parte-5-arrays/)
