# O que é um Monorepo?
Um Monorepo é uma arquitetura para [[Repositorios de Código]] versionado de projetos, que tem como objetivo centralizar as diversas aplicações e pacotes de uma organização em um unico repositorio, podendo elas serem relacionadas ou independentes e gerenciadas por um unico ou diversos times dentro de uma empresa.

Algumas empresas utilizam a arquitetura de Monorepo, para manter uma unica fonte de verdade entre todas as aplicações e pacotes da organização centralizadas.
os Monorepos são normalmente grandes em termo de espaço de armazenamento, alguns dos maiores Monorepos são de grandes empresas como Google, Microsoft, Facebook e Twitter, sendo o Monorepo da Google, atualmente estimado em cerca de 80 TBs (Terabytes), pois houve decisão logo no inicio da compania, que esta seria a sua cultura de desenvolvimento, alem de possuirem ferramentas internas que foram desenvolvidas para gerenciar o repositorio tendo a cultura da empresa em mente.

Existem diversas vantagens em se ter projetos e bibliotecas centralizadas em um unico repositorio, principalmente quando falamos de compartilhamento de codigo, por exemplo, varios projetos de desenvolvimento web tendem a ser compostos de componentes base, como botões e campos de texto personalizados, em um Monorepo, existe a vantagem de ser manter um unico componente e disponibiliza-lo para todas as aplicações que vivem dentro do Monorepo, minimizando as chances de codigo redundante.

Monorepos podem tambem ser chamados de Repositorios Monoliticos, porem não devem 
ser confundidos com [[Arquitetura Monolitica]].

# Monorepo Vs. [[Multirepo]] Vs. [[Arquitetura Monolitica]]
Cada arquitetura de repositorios possui suas vantagens e desvantagens, e não podemos considerar uma solução como sendo a melhor ou pior de todas, cada escopo de projeto ou empresa se adequa a um tipo de arquitetura, e sempre é possivel migrar de arquitetura caso seja necessario.

Um Monorepo consiste em um unico repositorio contendo todas as aplicações de uma organização centralizada. Por ter as aplicações centralizadas, automaticamente se torna disponivel para todos os times, ou seja, qualquer funcionalidade ou componente desenvolvido em uma aplicação, pode ser usado por outro time em outra aplicação, como uma especie de biblioteca que esta constantemente atualizada, tendo qualquer alteração refletida em todas as demais aplicações que consomem esta funcionalidade, evitando assim as famosas "breaking changes", uma vez que quando as mudanças são aplicadas e conflitos corrigidos antes de ser realizado o commit, não existirão mudanças que quebrem as aplicações

Um Multirepo consiste em diversos repositorios, separados comumente por times, podendo os repositorios serem ou não dependentes uns dos outros.

Uma arquitetura monolitica consiste em uma unica aplicação que "faz tudo", sendo mais comum em projetos legados, em uma arquitetura monolitica, conforme for necessario adicionar novas funcionalidades, é criado de forma interligada com a aplicação, dificultando a sua reutilização em outros projetos.

# Monorepos em Ambiente de Produção
Existem diversas estratégias para a implementação de projetos construidos em Monorepos no ambiente de produção, uma delas sendo com a implementação de containers usando [[Docker]].

Ao adicionar a aplicação em um container, é comum encontar situações em que cada container é um repositorio, contendo seu Dockerfile especifico. No entento em Monorepos, por termos todas as aplicações e suas dependencias em um unico repositorio, pode ocasionar em dificuldades durante a orquestração destes containers.

Um dos principais fatores que podem causar problemas, são as dependencias locais do Monorepo, elas são normalmente bibliotecas desenvolvidas internamento no Monorepo para serem reutilizadas entre os demais projetos, cada aplicação quando passa por usa pipeline de build, necessita que todas as dependencias sejam copiadas para dentro do container. Um possivel solução é organizar todas essas bibliotecas em uma unica pasta e para cada aplicação copiar todas as bibliotecas para cada um dos containers, porem esta solução não é escalavel, uma vez que a cada nova biblioteca adicionada no Monorepo, o tempo de build para cada imagem cresce exponencialmente.

Um cenario escalavel é que durante o processo de build das aplicações, as dependencias internas sejam tradas como se fossem pacotes, baixados de uma CDN (Content Delivery Network), e caso não sejam encontrdas, então realizar o processo de build e publish deste pacote, dessa maneira garantido que os pacotes sempre serão buildados durante a criação das imagens, porem passando por este fluxo apenas uma vez, sendo possivel as demais aplicações apenas baixarem desta "CDN"  a biblioteca recem buildada.

É importante que as empresas que adotem o Monorepo em sua cultura de desenvolvimento, tenham um fluxo bem definido para o processo das imagens Docker, uma vez que este é um processo que demanda tempo, e se não for devidamente implementaedo, irá gerar custos buildando pacotes redundates.

# Monorepo da Google
Desde seu inicio, os desenvolvedores da Google decidiram trabalhar centralizando todas suas aplicações e serviços em um unico repositorio, e mesmo com o constante crescimento da empresa, e por consequencia, o numero de desenvolvedores, a arquitetura de Monorepo ainda é utilizada em grande força. Em 2016, era estimado que o Monorepo da Google se aproximava de 86TBs de dados e cerca de 35 milhões de commits entre os 18 anos de existencia do repositorio. Devido ao imenso tamanho deste repositorio, foi necessario o desenvolvimento de ferramentas especializadas para poder gerenciar o repositorio
A ferramenta desenvolvida para gerenciar o Monorepo recebeu o codinome Piper, de acordo com a Google, não existe uma ferramenta comercial que conseguisse lidar com o seu Monorepo. Piper é responsavel por hospedar um unico repositorio implementado sob a infraestrutura da Google, e é distribuido entre dez data centers ao redor do mundo.

# Ferramentas de Monorepo
Existem diversas ferramentas para construir e gerenciar Monorepos, dentro do ecossistema de Javascript algumas das ferramentas com maiors satisfação são:

- pnpm -> 89% de satisfação
- Turborepo -> 88% de satisfação
- Nx -> 85% de satisfação
- npm Workspaces -> 84% de satisfação
- Yarn Workspaces -> 80% de satisfação
- Yalc -> 76% de satisfação
- Lerna -> 60% de satisfação
- Rush -> 59% de satisfação

Dentre essas ferramentas, uma que vem ganhando bastante atenção da comunidade Javascript é o [[Turborepo]], uma ferramenta desenvolvida por Jared Palmer e que foi adquirida pela empresa Vercel em 2021. Ela possui diversas funcionalidades para facilitar o gerenciamento de Monorepos alem de disponibilizar um registry para salvar o cache de builds de aplicações e pacotes, sendo o complemento ideal para o desenvolvimento de Monorepos rapidos com containers

# Cultura Monorepo
Monorepos não podem ser considerado como uma solução definitiva para todos os tipos de projetos. Para que uma implementação de Monorepo seja bem sucedida, uma serie de preparações devem ser realizadas. É necessario ter um fluxo bem definido de como serão dispostas as aplicações e pacotes, como elas serão gerenciadas, executadas e versionadas.

Alem da parte técnica é importante que o time que ira utilizar o Monorepo esteja pronto para aderir a cultura de Monorepo. Todos os desenvolvedores estão trabalahndo em um unico repositorio contendo diversos projetos, é importante que haja uma comunicação clara entre os times, para evitar que uma alteração afete o trabalho dos demais. Possuir planos de testes consistentes, garantindo que toda e qualquer alteração não gere problemas em outras dependencias, e estar pronto para que se houver algum problema, resolve-lo imediatamente. Essas são algumas das bases fundamentais para que a adoção de Monorepos se torne algo produtivo, se todos os times não estiverem dispostos a trabalharem seguindo essas praticas, a implementação do Monorepo não ira trazer beneficios para o time, e ira se tornar um incomodo improdutivo

# Referencias
[Why Google Stores Billions of Lines of Code in a Single Repository](https://dl.acm.org/doi/pdf/10.1145/2854146)
[Monolito, Multirepo ou Monorepo?](https://ggdaltoso.dev/posts/monolito-multirepo-ou-monorepo/)
[State of Js](https://2021.stateofjs.com/en-US/libraries/monorepo-tools)
[Advantages and Disadvantages of a Monolithic Repository](https://dl.acm.org/doi/pdf/10.1145/3183519.3183550)