# Diário #

### 11/05/2017 ###

- Fomos apresentados à cliente e recebemos uma explicação da tarefa.

### 29/05/2017 ###

- Foi criada a primeira versão do arquivo contendo a Recuperação de Desenho. Ele foi feito para melhorar como o software que usamos como base está estruturado e ao mesmo tempo como registro do que iremos mudar nele para obter nosso software final. Ela está mais focada nas componentes principais do software, não na arquitetura como um todo (não falamos de algumas bibliotecas externas, por exemplo).

### 30/05/2017 ###

- Foram criados os Requisitos.

### 01/06/2017 ###

- Requisitos atualizados.
- Arquivo de Rastro criado e atualizado.

### 04/06/2017 ###

- Foi criada a primeira versão do Modelo de Classes que representa parte da Arquitetura. Como o foco desse modelo é representar as classes definidas no software, o objetivo desse modelo é mostrar quais são essas classes e encaixar elas na arquitetura MVC, que serviu de base para a organização da aplicação. Essa versão inicial segue uma visão mais fiel de como o software original está montado precisamente para ajudar a visualizar ele. Foram adicionadas arestas para representar chamadas explícitas entre as classes como está no código, o objetivo é apenas servir de apoio para quando formos começar a implementação. Como usaremos o Modelo de Componentes, que foca em mostrar as conexões entre classes, as arestas devem ser retiradas do Modelo de Classes futuramente.

### 11/06/2017 ###

- Foram modificadas as classes de busca para atender busca de issues **github_consumer.rb**, **issues_searcher.rb** e **issue_info_searcher.rb**. A preocupação inicial era de estruturar a base de requisições para a API do GitHub e guardar as informações mais acessíveis referentes às issues resultantes da query. A parte de puxar comentários não está incluída. As mudanças foram testadas a base de prints no console para ver parte das estruturas onde o conteúdo extraído da API está armazenado. Como está, o código ao ser executado e usado pela interface com o usuário devolve o corpus após terminar o processamento das queries. Só que os arquivos estão vazios. Normal, visto que ainda devemos ter que mudar as outras classes do software para acompanharem as mudanças feitas até então.
- Foi atualizado o Diagrama de Classes. Os nomes das classes foram atualizados conforme as mudanças registradas no item acima. Foi levado também em consideração a observação feita pelo professor para analisar se os subgrupos **ASSETS** e **WORKERS** não seriam na verdade parte dos grupos que definem o MVC. **ASSETS** foi incluído em **VIEW**, visto que ele trabalha diretamente com esse grupo. **WORKERS** ainda deve ser analisado com calma pra ver se entra em **CONTROLLER** ou **MODEL**.

### 13/06/2017 ###

- A página inicial **index.html.erb** tinha sido alterada na data 07/06/2017 para incluir as opções de label e se quer ou não comentários. Hoje foi alterada para também dar a opção de qual ordenação o usuário quer as issues. Com isso poderemos capturar as informações passadas pelo usuário.
- **issue_info_searcher.rb** foi atualizado para satisfazer o requisito na issue **[#9](https://github.com/danielamaksoud/INF1629TerceiroTrabalho/issues/9)**, mudando o formato dos arquivos dentro do corpus de **TXT** para **JSON**. Também foram incluídos mais alguns comentários do que falta implementar nessa classe para ajudar os integrantes que forem complementar seu código.

### 17/06/2017 ###

- Mais uma atualização no Diagrama de Classes. **WORKERS** foi incluído a **CONTROLLER**, visto que seu papel principal é repassar informações de outras classes de **CONTROLLER** para classes de **MODEL**. Ele serve de ponto de início para as requisições, para a montagem do **ZIP** e para a classe responsável pelos resultados anteriores (**ZIP**s de resultados para download mostrados no site).

### 19/06/2017 ###
- Todas as informações da pesquisa que o usuário precisa passar já estão sendo passadas para o **ReadmesSetCreatorWorker.perform_async** dentro do **readmes_controller.rb**. As informações são: Query (o que se deve buscar), Match (newest, oldest, most commented...), Label (sem label, bug, ...) e se quer comentarios (true or false). Essa atualização ocorreu dia 16 e foi esquecida de ser relatada.

### 27/06/2017 ###
- **index.html.erb** foi atualizado para conter corretamente as opções de label e match. Os valores gerados pelo **HTML** foram construídos da forma que seria minimamente representado na API do GitHub (ex.: para label bug, retornar uma string `label:bug`) para que as classes que fazem as requisições se preocupem apenas em como ordenar os dados para fazer as requisições.
- **readmes_set_creator_worker.rb** teve seu campo de testes no código comentado para agilizar o processo da aplicação. Foi atualizado para quando chamar `GithubConsumer.get_issues` passar as informações sobre label, match e comments.
- **github_consumer.rb** foi atualizado para conter parâmetros referentes ao que se precisa saber sobre a busca em seu método `get_issues`. As chamadas `get_all_issues_urls(query, match, label)` e `get_info_from_issues(issues_urls, comments)` foram implementadas, motivos estão nos tópicos abaixo.
- **issues_searcher.rb** foi atualizado em um de seus métodos para conter `get_all_issues_urls(query, match, label)`. Como nesta classe só nos preocupamos em fazer a requisição principal de issues, comments não é necessário aqui. Match e label importam pois já filtram a requisição principal. 
- **issue_info_searcher.rb** foi atualizado em um de seus métodos para conter `get_info_from_issues(issues_urls, comments)`. Aqui como procuramos informações dentro de cada issue, pode nos interessar procurar sobre campo comments.

### 29/06/2017 ###
- Método `IssueInfoSearcher.get_info_from_issues` teve parâmetro match incluído para a possibilidade de já arrumar issues na estrutura principal pela ordenação. Por enquanto não é usado.
- **issues_searcher.rb** teve adicionado na string da query principal a parte de busca por label pedida pelo usuário para filtrar a busca. Lógica de ordenação não revisada.
- **issue_info_searcher.rb** teve a parte de requisição de comentário implementada e teve os dados de usuário incluídos. Como uma solução rápida, o código para criar a estrutura final foi dividido em duas partes com repetição de código. Uma parte para tratar comentários, outra sem. O ideal é tirar o código repetido futuramente. No caso, foi criada uma nova estrutura (array) com dois campos (usuário e body). Assim, cada par constituindo um índice do array equivale a um comentário dentro da respectiva issue. Parte testada e aparentemente ok.

### 30/06/2017 ###
- Correção em **issue_info_searcher.rb** sobre comentários, não estavam sendo tratadas issues sem comentários (lembrando que mesmo que o usuário peça issue com comments, issue com e sem são incluídas no corpus). Isso dava erro no momento de organizar os nomes dos arquivos dentro do corpus, pois não entravam as issues sem comentário (no nome dos arquivos entra a indexação deles pela ordem da organização em match).
- As informações sobre labels em **issue_info_searcher.rb** foram reduzidas ao passar na estrutura final para apenas nomes dados à label. Foram mantidos todos os nomes dados pelo criador da issue para caso seja interesse do usuário final saber outros nomes além do nome de label que faz parte da query principal.
- Renomeação de **readmes_controller** para **issues_controller** ocorreu dia 29/06/2017, o que levou a renomeação de outros arquivos relacionados. O arquivos alterados podem ser obtidos pelos commits: [primeiro](https://github.com/ninofabrizio/corpus-retrieval/commit/7a4e64d6cad7e3e8d3d267cb6dfb78e5c044bb8d) e [segundo](https://github.com/ninofabrizio/corpus-retrieval/commit/3391ec8cf6b258af656a5cafc27addda24ec7cee)
