# GIT (parte 2) - Basico 2: reversao de commits

> Modulo: Logica

## Objetivo da aula
Entender como visualizar o historico de commits e reverter alteracoes de forma segura usando `git log`, `git revert` e `git reset`.

## Exemplo rapido
```bash
# ver historico de commits
git log --oneline

# reverter um commit sem apagar o historico
git revert abc1234

# desfazer o ultimo commit mantendo as alteracoes no working directory
git reset --soft HEAD~1
```

## Visualizando o historico

### `git log`
Exibe o historico completo de commits.
```bash
git log
```

### `git log --oneline`
Versao resumida, uma linha por commit — mais util no dia a dia.
```bash
git log --oneline
```

Saida esperada:
```
f3a12bc adiciona arquivo de configuracao
9e4d001 corrige bug no calculo
a7b2c3d primeiro commit
```

Cada linha tem: **hash do commit** + **mensagem**.

## Revertendo alteracoes

### `git revert`
Cria um **novo commit** que desfaz as alteracoes de um commit anterior. O historico e preservado — e o metodo mais seguro para desfazer em repositorios compartilhados.

```bash
git revert abc1234
```

> O Git abrira um editor para a mensagem do commit de reversao. Salve e feche para confirmar.

### `git reset`
Move o ponteiro do historico para um commit anterior. Tem tres modos principais:

| Modo | Comando | Efeito |
|------|---------|--------|
| soft | `git reset --soft HEAD~1` | Desfaz o commit, mantem arquivos no stage |
| mixed (padrao) | `git reset HEAD~1` | Desfaz o commit, remove do stage, mantem no disco |
| hard | `git reset --hard HEAD~1` | Desfaz o commit e **apaga as alteracoes** |

> `HEAD~1` significa "um commit antes do atual". Use `HEAD~2` para dois commits antes, e assim por diante.

> **Atencao:** `--hard` apaga alteracoes de forma permanente. Use com cuidado.

## Quando usar cada um

- `git revert`: repositorios compartilhados, quando o commit ja foi publicado.
- `git reset --soft`: quando voce quer reformular a mensagem ou reagrupar commits locais.
- `git reset --mixed`: quando quer desfazer o commit mas continuar editando os arquivos.
- `git reset --hard`: quando quer descartar completamente as alteracoes locais.

## Pratica sugerida (exercicio concreto)
### Projeto: Corrigindo o historico
Pratique a reversao de commits de forma segura num repositorio local.

### Requisitos obrigatorios
1. Crie (ou reutilize) um repositorio local com pelo menos 3 commits.
2. Visualize o historico com `git log --oneline` e copie o hash de um commit.
3. Use `git revert` no commit do meio e confirme o novo commit gerado.
4. Verifique que o historico agora tem 4 commits (os 3 originais + o de reversao).
5. Crie dois novos commits com conteudo qualquer.
6. Use `git reset --soft HEAD~1` e observe que os arquivos ainda estao no stage.
7. Refaca o commit com uma mensagem melhor.

### Regras de validacao
- O `git revert` deve gerar um commit novo — nao apagar o original.
- Apos o `reset --soft`, os arquivos devem estar visiveis no `git status` como "Changes to be committed".
- O historico final deve ser verificavel via `git log --oneline`.

### Entrega esperada
- Repositorio local com historico demonstrando o uso de `revert` e `reset`.

## Desafio opcional
Experimente `git reset --hard` em um commit local (que voce nao precisa mais) e observe o comportamento. Documente no `dia-02.txt` o que aconteceu.

## Navegacao
- [Aula anterior: GIT (parte 1) - Basico 1](../git-parte-1-basico-1-init-clone-status-add-commit/)
- [Voltar para Logica](../../)
- [Proxima aula: GIT (parte 3) - Basico 3: fetch, pull, push](../git-parte-3-basico-3-fetch-pull-push/)
