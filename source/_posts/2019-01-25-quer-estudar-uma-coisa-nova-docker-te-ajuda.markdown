---
layout: post
title: "Quer estudar uma coisa nova? Docker te ajuda!"
permalink: ":year/quer-estudar-uma-coisa-nova-docker-te-ajuda"
date: 2019-01-25 00:00:00
comments: true
categories: [desenvolvimento]
---

Sempre que vamos estudar algo em tecnologia, em programação temos a complexidade do ambiente para resolver. Para um simples **Hello World** precisamos de um ambiente e a complexidade da criação dele pode desanimar os iniciantes (Por isso o JavaScript vem a ser execelente para os iniciantes!).

Mas para ajudar com isso temos os containers e uma ferramenta excelente para trabalhar com eles, o Docker. Diferente de uma máquina virtual, o container vai abranger apenas o que é necessário para rodar sua aplicação, sem precisar de um SO completo.

Vamos dizer então que você quer estudar algo diferente, um banco de dados de grafos e vamos entender como o Docker vai te ajudar com isso.

<!--more-->
## Pesquise
Então até aqui já temos alguns nomes que podem ser novos para alguns.

### Docker
Se você não conhece docker, dê uma buscada sobre. É uma ferramenta que pode mudar sua maneira de pensar em ambientes, arquiteturas e até sua maneira de desenvolver.

### Banco de dados de Grafos
Outro ponto são bancos de dados de Grafos. Pesquise, veja suas aplicações, leia os conceitos. Busque pela solução do problema do caminho mínimo, do caixeiro viajante e outros similares.  

## Neo4J
O Neo4J se tornou um bancos de dados de grafos muito conhecido. Pode ser pela sua interface gráfica ou pelo seu tutorial passo a passo que te mostra algumas coisas legais de entender com grafos.

Ele não é o foco desse artigo mas espero que traga algo para bater na cabeça de vocês.

## O Docker te ajudando a estudar qualquer coisa
Então vamos dizer que você escolheu que quer estudar grafos e chegou a conclusão que o Neo4J é bom para iniciar. Vamos ver como o docker vai te ajudar nisso. 

Massssss...... Esse é um exemplo, o que quero mostrar é a facilidade que ele traz seja lá o que você quer estudar. Go, Java, NodeJS, PhantomJS, ferramentas, bancos de dados e outras tantas coisas. Siga os passos que vou descrever abaixo e você encontrará seu caminho.

## Dockerhub
O Docker funciona com imagens. Uma imagem é um arquivo que contém todas (ou quase todas) as instruções para a rodar a aplicação que você precisa.

O [Dockerhub](https://hub.docker.com/) é um repositório dessas imagens, e lá você pode procurar pelo o que você precisa.

Repare que você encontrará imagens oficiais, produzidas pelas empresas dos softwares e imagens criados por outros usuários. As oficiais, geralmente, vem com uma extensa documentação que são de grande ajuda para fazer tudo rodar certinho. Mas, um usuário pode ter tido um insight legal e acrescentado ou facilitado ainda mais o processo, então vale ficar de olho nos dois.

Para um futuro, vale você ver como subir suas imagens

## Subindo um Neo4J
No Dockerhub procure por Neo4J.

Nos resultados da pesquisa você deve chegar na imagem oficial que está no seguinte endereço [https://hub.docker.com/_/neo4j](https://hub.docker.com/_/neo4j).

Dentrp desse repositório oficial do Neo4J você tem as versões, uma explicação do que é o Neo4J, como usar, documentacão e licença.

Em ***como usar essa imagem***, você vê o comando **docker run** para rodar a aplicação.

***** Sim!! Você já deve ter o docker instalado em sua máquina antes de seguir em diante. Não será difícil achar tutoriais de como fazer isso par aseu sistema operacional internet a fora.*****

Vamos executar:

~~~
docker run --publish=7474:7474 --publish=7687:7687 --volume=$HOME/neo4j/data:/data neo4j
~~~

Explicando esse comando temos:

* --publish está expondo sua porta 7474 e encaminhando ela para a porta 7474 do container.
* O mesmo acontece com a porta 7687.
* --volume é um caminho na sua máquina que será compatilhado com o container. Ele armazenará as mudanças de dados que você fizer, e quando você erguer novamente esse container suas alterações estarão lá.
* Neo4J no final é o nome da imagem.

A instrução --publish pode ser abreviado para -p e a instrução --volume para -v. 
Você pode tirar o sinal de igual, manter, tanto faz. 

Eu uso como abaixo:

~~~
docker run -p 7474:7474 -p 7687:7687 -v $HOME/neo4j/data:/data neo4j
~~~

Essa é a saída que começa a aparecer aqui:

~~~
Unable to find image 'neo4j:latest' locally
latest: Pulling from library/neo4j
cd784148e348: Downloading [========================================>          ]  1.785MB/2.207MB
35920a071f91: Download complete 
1a5149a464dd: Downloading [=>                                                 ]  1.621MB/54.87MB
15bb04bfc35a: Waiting 
...
~~~

* O Docker viu que eu não tinha a imagem, então foi buscar o caminho dela para fazer o download.
* Layers, é a maneira que o docker usa para fazer o download das imagens.

Na sequência disso ele vai subir a aplicação, até te dizer o seguinte:

~~~
....
INFO  ======== Neo4j 3.5.2 ========
INFO  Starting...
INFO  Bolt enabled on 0.0.0.0:7687.
INFO  Started.
INFO  Remote interface available at http://localhost:7474/
~~~

Acesse conforme a saída sugere o endereço http://localhost:7474 e você está na interface do Neo4J.

Viu como é fácil?

## Teste com outras ferramentas / tecnologias
Acredito que não houve nenhuma dor em seguir os passos acima. É muito simples!

Buscar no dockerhub a tecnologia, dar uma lida em como a imagem se comporta e executar um docker run.

Teste com outras ferramentas, bancos de dados, sistemas, frameworks e se apaixone pelo docker assim como eu.

Grande Abraço!
