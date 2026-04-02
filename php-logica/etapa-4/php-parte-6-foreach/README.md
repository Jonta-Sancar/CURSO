# PHP (parte 6) - Foreach

> Modulo: Logica

## Objetivo da aula
Percorrer arrays indexados e associativos de forma legivel e idiomatica usando `foreach`.

## Exemplo rapido
```php
<?php

$frutas = ["maca", "banana", "laranja"];

foreach ($frutas as $fruta) {
    echo $fruta . PHP_EOL;
}

$pessoa = ["nome" => "Lucas", "idade" => 28, "cidade" => "Sao Paulo"];

foreach ($pessoa as $chave => $valor) {
    echo $chave . ": " . $valor . PHP_EOL;
}
```

## Sintaxe

### Array indexado — so valor
```php
foreach ($array as $valor) {
    // $valor e cada elemento
}
```

### Array associativo — chave e valor
```php
foreach ($array as $chave => $valor) {
    // $chave e a chave, $valor e o elemento
}
```

> A variavel `$chave` e opcional. Use so quando precisar da chave no corpo do laco.

## Exemplos praticos

### Percorrer lista de produtos
```php
<?php

$produtos = [
    ["nome" => "Teclado",  "preco" => 150.00],
    ["nome" => "Mouse",    "preco" => 80.00],
    ["nome" => "Monitor",  "preco" => 1200.00],
];

foreach ($produtos as $produto) {
    echo $produto["nome"] . " — R$ " . number_format($produto["preco"], 2, ',', '.') . PHP_EOL;
}
```

### Calcular media com foreach
```php
<?php

$notas = [7.5, 8.0, 6.5, 9.0, 5.5];
$soma = 0;

foreach ($notas as $nota) {
    $soma += $nota;
}

$media = $soma / count($notas);
echo "Media: " . number_format($media, 2) . PHP_EOL;
```

### Modificar elementos com referencia (`&`)
Para alterar o array original dentro do foreach, use `&` antes da variavel:

```php
<?php

$precos = [100, 200, 300];

foreach ($precos as &$preco) {
    $preco *= 1.1; // aplica 10% de aumento
}
unset($preco); // boa pratica: desfaz a referencia apos o laco

print_r($precos); // [110, 220, 330]
```

> Sempre chame `unset($variavel)` apos um `foreach` com referencia para evitar comportamentos inesperados.

## foreach vs for

| Criterio | `for` | `foreach` |
|----------|-------|-----------|
| Controle de indice | Manual | Automatico |
| Arrays associativos | Nao (direto) | Sim |
| Legibilidade | Menor | Maior |
| Modificar elementos | Com `$arr[$i]` | Com `&$valor` |

Use `for` quando precisar do indice para logica especifica. Use `foreach` na maioria dos casos com arrays.

## Pratica sugerida (exercicio concreto)
### Projeto: Relatorio de vendas via terminal
Crie um script que processa um conjunto de vendas e exibe um relatorio.

### Requisitos obrigatorios
1. Defina um array de vendas ja preenchido com pelo menos 5 registros, cada um sendo um array associativo com: `"produto"`, `"quantidade"` e `"preco_unitario"`.
2. Use `foreach` para percorrer as vendas e calcular o `"total"` de cada uma (`quantidade * preco_unitario`).
3. Acumule o total geral de todas as vendas.
4. Exiba cada venda no formato: `Produto: X | Qtd: Y | Unit: R$Z | Total: R$W`.
5. Ao final, exiba o total geral do relatorio.
6. Identifique e exiba a venda com maior valor total (use uma variavel auxiliar dentro do foreach).

### Regras de validacao
- Usar `foreach` com `$chave => $valor` em pelo menos uma parte do script.
- Nao usar `for` com indice numerico para percorrer as vendas.
- Valores monetarios devem ser formatados com `number_format($valor, 2, ',', '.')`.

### Entrega esperada
- Arquivo `relatorio.php` na pasta da aula.

## Desafio opcional
Adicione um segundo `foreach` que percorre os produtos com referencia (`&`) e aplica um desconto de 5% no `preco_unitario` de todos os itens com `quantidade > 3`. Exiba o relatorio novamente apos o ajuste.

## Navegacao
- [Aula anterior: PHP (parte 5) - Arrays](../php-parte-5-arrays/)
- [Voltar para Logica](../../)
- [Proxima etapa: PHP (parte 7) - Funcoes](../../etapa-5/php-parte-7-funcoes-tipando-parametros-valores-padrao-escopo-return/)
