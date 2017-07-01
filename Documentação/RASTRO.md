# Rastro

|    Símbolo / Requisito        | #2 | #3 | #4 | #5 | #6 | #9 | #10 | #11 | #12 | #13 | #14 | #15 |
|-------------------------------|----|----|----|----|----|----|-----|-----|-----|-----|-----|-----|
| [apresentação](#apresentação) |    |    |    | X  |    |    |     |     |     |     | X   |     |
| [busca](#busca)               | X  | X  | X  |    | X  |    | X   | X   |     |     | X   |     |
| [buscador](#buscador)         |    |    |    | X  |    | X  | X   |     | X   | X   | X   | X   |
| [comentário](#comentário)     |    |    | X  |    |    |    |     |     |     |     |     |     |
| [corpus](#corpus)             |    |    |    | X  |    | X  |     |     |     |     | X   |     |
| [github](#github)             | X  |    |    |    |    |    | X   |     |     | X   |     |     |
| [issue](#issue)               | X  | X  | X  |    |    |    |     | X   |     |     |     |     |
| [label](#label)               |    | X  |    |    |    |    |     | X   |     |     |     |     |
| [minerador](#minerador)       | X  |    |    |    |    |    |     |     | X   |     | X   |     |
| [requisitando](#requisitando) | X  | X  | X  |    | X  |    | X   |     |     |     | X   |     |

## Apresentação ##
Resulta no corpus de resultados, gerado por uma busca.

## Busca ##
minerador ativa uma busca ao definir o que deseja no corpus.  
É a requisição dos dados do github sobre o assunto definido.

## Buscador ##
Software que o minerador usa para fazer a busca no github.  
Obtém as issues e, se o minerador desejar, os seus comentários.  
Faz apresentação do corpus de resultados.

## Comentário ##
É uma discussão referente a uma issue. Pode ser requisitado pelo minerador.

## Corpus ##
Conjunto de textos estruturados.
Possui os dados referntes a issues e comentários delas.

## Github ##
GitHub é um site que permite gerenciamento de projetos criados pelo Git.  
Armazena dados referentes a esses projetos, como issues e seus comentários.

## Issue ##
É a sugestão de melhorias, tarefas e bugs relacionado a um repositório. usuários abrem issues dentro de repositórios no github. Pode possuir comentários. corpus irá conter o seu conteúdo.

## Label ##
Assunto sobrer o qual uma issue trata/fala.  
Uma issue pode ter uma label ou não.

## Minerador ##
É o sujeito que deseja obter dados do github referente a issues e/ou seus comentários.

## Requisitando ##
Ativado quando minerador pede uma busca ao buscador. buscador faz a requisição de dados do github.
