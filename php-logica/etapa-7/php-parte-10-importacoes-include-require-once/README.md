# PHP (parte 10) - Importacoes: include, require, _once

> Modulo: Logica

## Objetivo da aula
Organizar um projeto PHP em multiplos arquivos usando `include`, `require`, `include_once` e `require_once`, e compreender as diferencas entre eles.

## Exemplo rapido
```php
<?php
// config.php
const APP_NOME = 'MeuSistema';
const VERSAO = '1.0.0';
```

```php
<?php
// index.php
require_once 'config.php';

echo APP_NOME . " v" . VERSAO . PHP_EOL;
```

## Por que dividir em arquivos

Em projetos reais, concentrar todo o codigo em um unico arquivo torna-o dificil de manter. A modularizacao permite:
- Reutilizar codigo (ex.: uma classe `Produto` usada em varios scripts).
- Separar responsabilidades (configuracoes, modelos, funcoes utilitarias).
- Facilitar leitura e manutencao.

## include vs require

| | `include` | `require` |
|--|-----------|-----------|
| Arquivo nao encontrado | Emite warning e **continua** | Emite erro fatal e **para** |
| Uso tipico | Partes opcionais (ex.: sidebar) | Dependencias criticas (ex.: config, classes) |

```php
<?php
include 'opcional.php';  // continua mesmo se o arquivo nao existir
require 'config.php';    // para se o arquivo nao existir
```

## include_once e require_once

Garantem que o arquivo e incluido **apenas uma vez**, mesmo que a instrucao apareça varias vezes no codigo. Evitam redeclaracao de classes, funcoes e constantes.

```php
<?php
require_once 'classes/Produto.php';
require_once 'classes/Produto.php'; // ignorado na segunda vez
```

> **Regra geral:** prefira sempre `require_once` para importar classes e arquivos de configuracao. Use `include_once` apenas para templates ou partes que podem falhar sem comprometer o sistema.

## Organizando um projeto modular

### Estrutura de exemplo
```
projeto/
├── config.php
├── funcoes.php
├── classes/
│   └── Produto.php
└── index.php
```

### config.php
```php
<?php

const APP_NOME  = 'Lojinha';
const VERSAO    = '1.2.0';
const MOEDA     = 'BRL';
```

### funcoes.php
```php
<?php

function formatar_preco(float $valor): string {
    return "R$ " . number_format($valor, 2, ',', '.');
}

function exibir_separador(): void {
    echo str_repeat("-", 40) . PHP_EOL;
}
```

### classes/Produto.php
```php
<?php

class Produto {
    public function __construct(
        public string $nome,
        public float $preco,
        public int $estoque
    ) {}

    public function exibir(): string {
        return $this->nome . " — R$ " . number_format($this->preco, 2, ',', '.');
    }
}
```

### index.php
```php
<?php

require_once 'config.php';
require_once 'funcoes.php';
require_once 'classes/Produto.php';

echo APP_NOME . " v" . VERSAO . PHP_EOL;
exibir_separador();

$produtos = [
    new Produto("Teclado", 149.90, 10),
    new Produto("Mouse",    79.90, 25),
    new Produto("Monitor", 999.00,  5),
];

foreach ($produtos as $produto) {
    echo $produto->exibir() . PHP_EOL;
}
```

## Caminhos relativos e absolutos

```php
<?php

// relativo ao arquivo atual
require_once 'config.php';
require_once './classes/Produto.php';

// usando __DIR__ (mais seguro — caminho absoluto do arquivo atual)
require_once __DIR__ . '/config.php';
require_once __DIR__ . '/classes/Produto.php';
```

> Prefira `__DIR__` em projetos reais para evitar problemas com o diretorio de trabalho atual.

## Pratica sugerida (exercicio concreto) — Projeto do modulo
### Projeto: Sistema de catalogo modular
Esta e a pratica final do modulo. O objetivo e aplicar tudo que foi aprendido — tipos, lacos, arrays, funcoes, classes e constantes — em um projeto organizado em multiplos arquivos.

### Requisitos obrigatorios
1. Crie a seguinte estrutura de arquivos:
   ```
   catalogo/
   ├── config.php
   ├── funcoes.php
   ├── classes/
   │   └── Produto.php
   └── index.php
   ```
2. Em `config.php`: defina constantes para nome do sistema, versao e taxa de desconto padrao.
3. Em `funcoes.php`: crie pelo menos 3 funcoes utilitarias (ex.: `formatar_preco`, `exibir_cabecalho`, `calcular_desconto`).
4. Em `classes/Produto.php`: implemente a classe `Produto` com propriedades tipadas, construtor e metodos.
5. Em `index.php`:
   - Importe todos os arquivos com `require_once`.
   - Instancie pelo menos 4 produtos.
   - Exiba o catalogo completo usando `foreach`.
   - Ofeca um menu via terminal: 1) Ver catalogo | 2) Buscar produto por nome | 3) Aplicar desconto em todos | 4) Sair.
6. A busca por nome deve ser case-insensitive (use `strtolower` para comparar).

### Regras de validacao
- Todo arquivo importado deve usar `require_once` com `__DIR__`.
- Nenhuma classe ou funcao pode ser declarada diretamente no `index.php`.
- As constantes de `config.php` devem ser usadas em pelo menos 2 arquivos diferentes.
- O script deve rodar sem erros com `php index.php`.

### Entrega esperada
- Pasta `catalogo/` com todos os arquivos organizados conforme a estrutura acima.

## Desafio opcional
Adicione um arquivo `relatorio.php` que e incluido pelo `index.php` apenas na opcao 5 do menu: "Gerar relatorio". Ele deve exibir estatisticas calculadas a partir do array de produtos (total de itens, preco medio, produto mais caro, produto mais barato).

## Navegacao
- [Aula anterior: PHP (parte 9) - Constantes](../php-parte-9-constantes/)
- [Voltar para Logica](../../)
