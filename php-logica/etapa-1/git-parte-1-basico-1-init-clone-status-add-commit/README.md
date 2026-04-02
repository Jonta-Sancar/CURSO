# GIT (parte 1) - Basico 1: init, clone, status, add, commit

> Modulo: Logica

## Objetivo da aula
Entender o que e controle de versao e aprender os comandos fundamentais para iniciar, rastrear e registrar alteracoes em um repositorio Git local.

## O que e Git
Git e um sistema de controle de versao distribuido. Ele rastreia o historico de alteracoes dos arquivos de um projeto, permitindo colaboracao, reversao e organizacao do codigo ao longo do tempo.

## Exemplo rapido
```bash
# iniciar um repositorio
git init

# verificar estado dos arquivos
git status

# adicionar arquivo ao stage
git add arquivo.txt

# registrar um commit
git commit -m "primeiro commit"
```

## Conceitos essenciais

### Repositorio
Um repositorio (repo) e a pasta raiz do projeto controlada pelo Git. Ao rodar `git init`, o Git cria uma pasta oculta `.git` que armazena todo o historico.

### Working directory, Stage e Repositorio
- **Working directory**: onde voce edita os arquivos.
- **Stage (index)**: area de preparacao — arquivos marcados para entrar no proximo commit.
- **Repositorio**: historico permanente de commits.

```
[Arquivo editado] → git add → [Stage] → git commit → [Historico]
```

## Comandos da aula

### `git init`
Inicia um repositorio Git na pasta atual.
```bash
git init
```

### `git clone`
Clona (copia) um repositorio remoto para a maquina local.
```bash
git clone https://github.com/usuario/repositorio.git
```

### `git status`
Exibe o estado atual dos arquivos: quais foram modificados, quais estao no stage e quais sao novos.
```bash
git status
```

### `git add`
Adiciona arquivos ao stage (prepara para o commit).
```bash
# adicionar um arquivo especifico
git add arquivo.txt

# adicionar todos os arquivos modificados
git add .
```

### `git commit`
Registra as alteracoes em stage no historico do repositorio.
```bash
git commit -m "descricao curta do que foi feito"
```

> Boas praticas de mensagem de commit: use verbos no imperativo e seja objetivo.  
> Exemplos: "adiciona tela de login", "corrige calculo de desconto", "remove campo obsoleto".

## Pratica sugerida (exercicio concreto)
### Projeto: Diario de aprendizado
Crie um repositorio local e registre sua evolucao no curso por meio de commits.

### Requisitos obrigatorios
1. Crie uma pasta chamada `diario-git` e inicialize um repositorio dentro dela.
2. Crie um arquivo `dia-01.txt` com um breve texto sobre o que voce aprendeu hoje.
3. Adicione o arquivo ao stage e faca o primeiro commit com a mensagem `"adiciona diario do dia 01"`.
4. Edite o arquivo `dia-01.txt` adicionando mais um paragrafo.
5. Verifique o status com `git status` e observe a diferenca entre arquivos rastreados e modificados.
6. Adicione as mudancas ao stage e faca um segundo commit com mensagem coerente.
7. Crie um segundo arquivo `dia-02.txt` com conteudo livre e faca um terceiro commit.

### Regras de validacao
- O repositorio deve ter exatamente 3 commits ao final.
- Cada mensagem de commit deve ser descritiva e diferente.
- Nao use `git add .` — adicione os arquivos pelo nome para praticar o comando.

### Entrega esperada
- Pasta `diario-git/` com os arquivos e historico de commits verificavel via `git log`.

## Desafio opcional
Clone qualquer repositorio publico do GitHub e explore sua estrutura com `git status` e `git log`.

## Navegacao
- [Voltar para Logica](../../)
- [Proxima aula: GIT (parte 2) - Basico 2: reversao de commits](../git-parte-2-basico-2-reversao-de-commits/)
