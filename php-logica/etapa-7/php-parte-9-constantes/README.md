# PHP (parte 9) - Constantes

> Modulo: Logica

## Objetivo da aula
Entender as formas de declarar constantes em PHP — globais e de classe — e saber quando usa-las no lugar de variaveis.

## Exemplo rapido
```php
<?php

define('VERSAO_APP', '2.0.1');
const LIMITE_ITENS = 50;

echo VERSAO_APP . PHP_EOL;  // 2.0.1
echo LIMITE_ITENS . PHP_EOL; // 50
```

## Constantes globais

### `define()`
Define uma constante em tempo de execucao. Pode ser usada dentro de condicionais e funcoes.

```php
<?php

define('APP_NOME', 'GerenciadorFiscal');
define('TAXA_JUROS', 0.025);
define('MODOS_VALIDOS', ['leitura', 'escrita', 'admin']); // arrays tambem sao suportados

echo APP_NOME . PHP_EOL;
echo TAXA_JUROS . PHP_EOL;
print_r(MODOS_VALIDOS);
```

### `const` (escopo global)
Define uma constante em tempo de compilacao. Mais eficiente, mas nao pode ser usada dentro de funcoes ou condicionais.

```php
<?php

const MAX_TENTATIVAS = 5;
const SEPARADOR = "---";

echo MAX_TENTATIVAS . PHP_EOL;
```

## Constantes de classe

Declaradas com `const` dentro de uma classe. Sao acessadas com `::` (operador de escopo).

```php
<?php

class Configuracao {
    const VERSAO = '1.0.0';
    const TIMEOUT = 30;
    const AMBIENTE = 'producao';
}

echo Configuracao::VERSAO . PHP_EOL;   // 1.0.0
echo Configuracao::TIMEOUT . PHP_EOL;  // 30
```

### Acesso dentro da propria classe

Use `self::CONSTANTE` para acessar uma constante dentro de metodos da mesma classe.

```php
<?php

class Pagamento {
    const TAXA_CARTAO = 0.03;
    const TAXA_BOLETO = 0.01;

    public function calcular_taxa(float $valor, string $metodo): float {
        $taxa = match ($metodo) {
            'cartao' => self::TAXA_CARTAO,
            'boleto' => self::TAXA_BOLETO,
            default  => 0.0,
        };
        return $valor * $taxa;
    }
}

$pag = new Pagamento();
echo $pag->calcular_taxa(1000, 'cartao') . PHP_EOL; // 30
echo $pag->calcular_taxa(1000, 'boleto') . PHP_EOL; // 10
```

## Quando usar constantes

| Situacao | Usar constante? |
|----------|----------------|
| Valor que nunca muda (PI, taxa, versao) | Sim |
| Configuracao global do sistema | Sim |
| Valor que depende de logica ou entrada | Nao — use variavel |
| Dado calculado em tempo de execucao | Nao — use variavel |

## Diferenca entre `define` e `const` (resumo)

| | `define()` | `const` |
|--|-----------|---------|
| Avaliacao | Tempo de execucao | Tempo de compilacao |
| Dentro de funcoes/condicionais | Sim | Nao |
| Dentro de classes | Nao | Sim |
| Suporta arrays | Sim (PHP 7+) | Sim |

## Pratica sugerida (exercicio concreto)
### Projeto: Configuracoes de sistema via terminal
Crie um script que usa constantes para centralizar as configuracoes de uma aplicacao simulada.

### Requisitos obrigatorios
1. Defina pelo menos 4 constantes globais com `define` ou `const`: nome do app, versao, limite de usuarios e ambiente (dev/producao).
2. Crie uma classe `Configuracao` com pelo menos 3 constantes de classe: timeout, taxa de imposto e separador visual.
3. Crie uma funcao `exibir_cabecalho(): void` que usa as constantes globais para exibir um cabecalho formatado.
4. Crie um metodo na classe `Configuracao` que usa `self::` para calcular o preco com imposto a partir de um valor recebido.
5. Execute a funcao de cabecalho e teste o metodo de imposto com valores lidos via `readline`.

### Regras de validacao
- As constantes nao podem ter valores alterados em nenhuma parte do script (nao reatribuir).
- Use `const` para as constantes de classe e `define` para pelo menos uma constante global.
- O metodo de imposto deve usar `self::` — nao o valor literal.

### Entrega esperada
- Arquivo `configuracoes.php` na pasta da aula.

## Desafio opcional
Adicione uma constante de array `PERMISSOES` com os valores `['admin', 'editor', 'leitor']`. Escreva uma funcao `tem_permissao(string $papel): bool` que verifica se o papel passado existe no array usando `in_array`.

## Navegacao
- [Aula anterior: PHP (parte 8) - Classes e Objetos](../../etapa-6/php-parte-8-classes-e-objetos-propriedades-tipagem-metodos-construtores-this/)
- [Voltar para Logica](../../)
- [Proxima aula: PHP (parte 10) - Importacoes](../php-parte-10-importacoes-include-require-once/)
