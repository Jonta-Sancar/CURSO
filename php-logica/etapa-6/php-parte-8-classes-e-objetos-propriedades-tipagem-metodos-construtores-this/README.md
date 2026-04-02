# PHP (parte 8) - Classes e Objetos: propriedades, tipagem, metodos, construtores, $this

> Modulo: Logica

## Objetivo da aula
Entender o conceito de classe e objeto em PHP, declarar propriedades tipadas, criar construtores e metodos, e usar `$this` para autorreferencia.

## Exemplo rapido
```php
<?php

class Produto {
    public string $nome;
    public float $preco;

    public function __construct(string $nome, float $preco) {
        $this->nome = $nome;
        $this->preco = $preco;
    }

    public function exibir(): string {
        return $this->nome . " — R$ " . number_format($this->preco, 2, ',', '.');
    }
}

$teclado = new Produto("Teclado", 150.00);
echo $teclado->exibir() . PHP_EOL;
```

## O que e uma classe

Uma classe e um modelo (template) que define a estrutura e o comportamento de objetos. Um objeto e uma instancia de uma classe — um valor concreto criado a partir do modelo.

```
Classe  →  Produto (o molde)
Objeto  →  $teclado, $mouse, $monitor (as instancias)
```

## Propriedades

Propriedades sao as variaveis de uma classe. Em PHP moderno, declare com tipo e visibilidade.

```php
<?php

class Pessoa {
    public string $nome;
    public int $idade;
    public ?string $email = null; // nullable, valor padrao null
}
```

### Visibilidade
| Modificador | Acesso |
|-------------|--------|
| `public` | Em qualquer lugar |
| `protected` | Na classe e nas subclasses |
| `private` | Somente dentro da propria classe |

> Nesta aula, use `public`. Os modificadores serao aprofundados no modulo de POO.

## Construtor

O metodo `__construct()` e executado automaticamente ao criar um objeto com `new`. Use-o para inicializar as propriedades.

```php
<?php

class Carro {
    public string $marca;
    public string $modelo;
    public int $ano;

    public function __construct(string $marca, string $modelo, int $ano) {
        $this->marca = $marca;
        $this->modelo = $modelo;
        $this->ano = $ano;
    }
}

$meu_carro = new Carro("Toyota", "Corolla", 2022);
echo $meu_carro->marca . PHP_EOL; // Toyota
```

### Promoted properties (PHP 8+)
Atalho para declarar e inicializar propriedades direto no construtor:

```php
<?php

class Carro {
    public function __construct(
        public string $marca,
        public string $modelo,
        public int $ano
    ) {}
}
```

## Metodos

Metodos sao funcoes declaradas dentro de uma classe. Use `$this` para acessar as propriedades e outros metodos do objeto atual.

```php
<?php

class ContaBancaria {
    public string $titular;
    public float $saldo;

    public function __construct(string $titular, float $saldo_inicial = 0.0) {
        $this->titular = $titular;
        $this->saldo = $saldo_inicial;
    }

    public function depositar(float $valor): void {
        $this->saldo += $valor;
    }

    public function sacar(float $valor): bool {
        if ($valor > $this->saldo) {
            return false;
        }
        $this->saldo -= $valor;
        return true;
    }

    public function extrato(): string {
        return "Titular: {$this->titular} | Saldo: R$ " . number_format($this->saldo, 2, ',', '.');
    }
}

$conta = new ContaBancaria("Ana", 500.00);
$conta->depositar(200.00);
$conta->sacar(100.00);
echo $conta->extrato() . PHP_EOL; // Titular: Ana | Saldo: R$ 600,00
```

## $this

`$this` e uma referencia ao objeto atual. E usado dentro dos metodos para acessar as propriedades e outros metodos da propria instancia.

```php
$this->propriedade  // acessa uma propriedade
$this->metodo()     // chama um metodo
```

## Pratica sugerida (exercicio concreto)
### Projeto: Sistema de estoque via terminal
Crie um script com uma classe `Produto` e um menu para gerenciar um estoque simples.

### Requisitos obrigatorios
1. Crie a classe `Produto` com as propriedades: `nome` (string), `preco` (float) e `estoque` (int).
2. O construtor deve receber os tres valores e inicializa-los.
3. Crie os metodos:
   - `adicionar_estoque(int $quantidade): void` — aumenta o estoque.
   - `remover_estoque(int $quantidade): bool` — diminui o estoque; retorna `false` se insuficiente.
   - `esta_disponivel(): bool` — retorna `true` se estoque > 0.
   - `exibir(): string` — retorna uma string formatada com todos os dados do produto.
4. Instancie pelo menos 3 produtos com `new Produto(...)`.
5. Crie um menu via terminal: 1) Listar produtos | 2) Adicionar estoque | 3) Remover estoque | 4) Sair.
6. O menu deve pedir o indice do produto (0, 1, 2...) e a quantidade, chamando os metodos correspondentes.

### Regras de validacao
- Propriedades e metodos devem ter tipagem completa.
- Nao use variaveis globais; tudo deve fluir por metodos e parametros.
- O metodo `remover_estoque` deve exibir mensagem de erro se o estoque for insuficiente.

### Entrega esperada
- Arquivo `estoque.php` na pasta da aula.

## Desafio opcional
Adicione um metodo estatico `Produto::criar_com_desconto(string $nome, float $preco_original, int $desconto_pct, int $estoque): Produto` que retorna uma nova instancia com o preco ja com desconto aplicado. Use `self::` para chamar o construtor dentro do metodo estatico.

## Navegacao
- [Aula anterior: PHP (parte 7) - Funcoes](../../etapa-5/php-parte-7-funcoes-tipando-parametros-valores-padrao-escopo-return/)
- [Voltar para Logica](../../)
- [Proxima etapa: PHP (parte 9) - Constantes](../../etapa-7/php-parte-9-constantes/)
