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
