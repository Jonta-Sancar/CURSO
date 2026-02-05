# CSS (parte 12) - @import

> Modulo: Front-end Basico

## Objetivo da aula
Organizacao de folhas de estilo e quando utilizar @import com criterio.

## Exemplo rapido
```css
@import url("./base.css");
@import url("./components.css");
```

## Pratica sugerida (exercicio concreto)
### Projeto: Refatoracao de CSS em modulos

### Requisitos obrigatorios
1. Divida o CSS da pagina em 3 arquivos: `base.css`, `layout.css`, `components.css`.
2. Crie um arquivo `main.css` que importa os outros com `@import`.
3. Garanta que o HTML referencie apenas `main.css`.
4. Mantenha cada arquivo com responsabilidade clara.
5. Documente no topo de cada arquivo o que ele deve conter.

### Regras de validacao
- Nao duplicar regras entre arquivos.
- Ordem dos `@import` deve evitar conflitos de cascata.
- A pagina final deve renderizar igual ou melhor que antes.
- Nomes de arquivos e secoes devem ser autoexplicativos.

### Entrega esperada
- Arquivo(s) HTML e CSS organizados em pasta unica da aula.
- Estrutura legivel, com nomes claros e sem conteudo placeholder.
## Navegacao
- [Voltar para Front-end Basico](../../)
