# Recuperação de Desenho #

Este arquivo tem como finalidade formalizar a **Recuperação de Desenho** referente ao projeto **Corpus Retrieval**. Nele citaremos as partes importantes do que iremos manter da arquitetura do projeto original e onde planejamos fazer alterações/adições.

### O que será mantido ###
1. **[Ruby](https://www.ruby-lang.org/en/)**: principal linguagem de programação usada para desenvolver a aplicação. A versão usada é **[v2.3.0](https://github.com/ruby/ruby/releases/tag/v2_3_0)**.
2. **[Rails](http://rubyonrails.org/)**: framework escrito em **Ruby** voltado para o desenvolvimento de aplicações web, ele é baseado na arquitetura MVC(ModelViewController), como pode ser verificado na ordenação do diretório **[..\app](https://github.com/ninofabrizio/corpus-retrieval/tree/master/app)**. A versão usada é **[v4.2.5](https://github.com/rails/rails/releases/tag/v4.2.5)**.
3. **[docker](https://docs.docker.com/)**: gerencia a imagem de uma máquina virtual que irá conter todas as dependências necessárias (e listadas aqui) para a nossa aplicação ser executada. Ela irá facilitar para que qualquer pessoa possa executar nosso software, independente do computador usado pela pessoa e sem ter que instalar nada além do próprio **docker**.
4. **[docker-compose](https://docs.docker.com/compose/overview/)**: interliga o que o **docker** chama de **containers**, que são nada mais do que componentes divididas da aplicação, onde cada um possui uma tarefa específica. A aplicação faz uso de 4 **containers** no total (vide informação em **[docker-compose.yml](https://github.com/ninofabrizio/corpus-retrieval/blob/master/docker-compose.yml)**):
    1. **web**: contém os processos referentes ao servidor usado pela aplicação.
    2. **sidekiq**: contém a **RubyGem** (biblioteca em **Ruby**) **SideKiq**, que agenda o trabalho de pegar o que se deseja obter referente a uma busca para ser feita em background. **Sidekiq** usa **Redis** sem o usuário ter que gerenciar, sua interface é só **Ruby**. Para isso, um dos **containers** a que este é interligado é o **redis**.
    3. **redis**: contém o **[Redis](https://redis.io/)**, banco de dados **NoSQL** que armazena todos os dados em memória. Ele é baseado no armazenamento chave-valor (como as listas em **Lua**). Este banco é usado para armazenar a resposta da API do Github temporariamente, com a finalidade de evitar fazer a requisição mais de uma vez em pouco tempo, o que pode resultar em passar do limite de requisições permitido pelo GitHub por hora. A versão usada é **v3.2**.
    4. **mongodb**: contém o **[MongoDB](https://www.mongodb.com/)**, banco de dados **NoSQL** baseado em documentos. É usado para armazenar os arquivos **.zip** contendo os conteúdos puxados das requisições (no nosso caso, informações referentes a **issues**). A versão usada é a **v3.3**.
5. **Typhoeus**: **RubyGem** que faz requisições HTTP usando **libcurl**, o que lhe permite fazer requisições assíncronas.
6. **Mongoid**: **RubyGem** que faz o intermédio entre o **MongoDB** e **Ruby**.
7. **Bundler**: **RubyGem** encarregada de fazer o gerenciamento das **RubyGems** citadas acima, e de outras que dependeremos, para usar no projeto, como pode ser verificado no arquivo **[Gemfile](https://github.com/ninofabrizio/corpus-retrieval/blob/master/Gemfile)**.

### O que mudaremos/adicionaremos ###
1. **[../app/models](https://github.com/ninofabrizio/corpus-retrieval/tree/master/app/models)**: Possui os arquivos referentes a consultar a API do Github e pegar a informação das requisições. Precisaremos adaptar para navegar pela parte da API referente a **issues** e puxar as informações contidas ali (o projeto inicial só lida com navegar e puxar dados de **READMEs**).
2. A forma de armazenar os dados obtidos. Precisamos apresentar os dados de cada **issue** no formato **JSON**.
3. A interface de comunicação entre nosso software e o cliente. Usando o **[Heroku](https://www.heroku.com/ruby#)**, faremos nossa própria aplicação web para um uso mais prático do software. Será similar ao do [projeto original](http://corpus-retrieval.herokuapp.com), mas com opções para o usuário pedir informações mais específicas referentes a **issues**. Como:
    1. Tipo de issue: Uma lista onde o usuário pode escolher um dos tipos oficiais dados pelo GitHub: bug, duplicate, enhancement, help wanted, invalid, question, wontfix, unlabeled.
    2. Comentários: Uma opção dada ao usuário se ele deseja que cada **issue** inclua os comentários atribuídos a ela.
4. **Proxies**. Precisaremos para fazer as requisições ao GitHub. Temos que criar as nossas próprias visto que as do projeto original são de uso exclusivo deste. A forma como foram especificadas no orinal estão em **[github-proxy](https://github.com/nitanilla/github-proxy)**.
