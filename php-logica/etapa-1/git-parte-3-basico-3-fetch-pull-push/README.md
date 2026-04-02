# GIT (parte 3) - Basico 3: fetch, pull, push

> Modulo: Logica

## Objetivo da aula
Entender como sincronizar um repositorio local com um repositorio remoto usando `git remote`, `git fetch`, `git pull` e `git push`.

## Exemplo rapido
```bash
# ver repositorios remotos configurados
git remote -v

# baixar alteracoes do remoto sem aplicar
git fetch origin

# baixar e aplicar alteracoes do remoto
git pull origin main

# enviar commits locais para o remoto
git push origin main
```

## Repositorios remotos

### `git remote`
Gerencia as conexoes com repositorios remotos.

```bash
# listar remotos configurados
git remote -v

# adicionar um remoto manualmente
git remote add origin https://github.com/usuario/repositorio.git
```

> Ao usar `git clone`, o remoto `origin` e configurado automaticamente.

## Sincronizando com o remoto

### `git fetch`
Baixa as alteracoes do repositorio remoto, mas **nao aplica** no branch atual. Permite revisar antes de integrar.

```bash
git fetch origin
```

### `git pull`
Baixa **e aplica** as alteracoes do remoto no branch atual. Equivale a `git fetch` + `git merge`.

```bash
git pull origin main
```

### `git push`
Envia os commits locais para o repositorio remoto.

```bash
git push origin main
```

> Na primeira vez, use `--set-upstream` (ou `-u`) para associar o branch local ao remoto:
> ```bash
> git push -u origin main
> ```
> Nas proximas vezes, basta `git push`.

## Fluxo tipico de trabalho

```
[Repositorio remoto] ──fetch/pull──► [Repositorio local]
[Repositorio local]  ────push──────► [Repositorio remoto]
```

1. `git pull` — sincronize antes de comecar a trabalhar.
2. Edite arquivos, `git add`, `git commit`.
3. `git push` — envie seus commits ao final.

## Pratica sugerida (exercicio concreto)
### Projeto: Repositorio no GitHub
Publique o repositorio criado na aula anterior no GitHub e sincronize-o.

### Requisitos obrigatorios
1. Crie um repositorio vazio no GitHub (sem README, sem .gitignore).
2. No repositorio local existente, adicione o remoto com `git remote add origin <url>`.
3. Envie os commits com `git push -u origin main`.
4. Verifique no GitHub que os arquivos e o historico aparecem corretamente.
5. Edite um arquivo diretamente pelo GitHub (botao de edicao na interface web) e faca commit pela interface.
6. No terminal local, rode `git fetch origin` e depois `git pull origin main`.
7. Confirme que o arquivo editado no GitHub agora esta na sua maquina.

### Regras de validacao
- O repositorio deve estar acessivel publicamente ou como privado no GitHub.
- O `git log --oneline` local deve mostrar o commit feito pela interface do GitHub apos o `pull`.
- Nao pode haver conflitos ao fazer o `pull` (o arquivo editado no GitHub nao pode ter sido editado localmente ao mesmo tempo).

### Entrega esperada
- URL do repositorio no GitHub com pelo menos 4 commits visiveis no historico.

## Desafio opcional
Crie um segundo clone do mesmo repositorio em outra pasta (`git clone <url> pasta-2`) e simule um fluxo de colaboracao: faca um commit em `pasta-2`, publique com `push`, e sincronize em `diario-git` com `pull`.

## Navegacao
- [Aula anterior: GIT (parte 2) - Basico 2: reversao de commits](../git-parte-2-basico-2-reversao-de-commits/)
- [Voltar para Logica](../../)
- [Proxima etapa: PHP (parte 1) - Tipos de valores, variaveis e constantes](../../etapa-2/php-parte-1-tipos-de-valores-variaveis-e-constantes/)
