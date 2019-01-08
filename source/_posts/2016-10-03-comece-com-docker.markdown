---
layout: post
title: "Comece com Docker"
date: 2016-10-03 00:00:00
comments: true
categories: [desenvolvimento]
permalink: ":year/comece-com-docker/"
---
Tenho dois posts envolvendo [vagrant](https://www.vagrantup.com/) aqui no blog que ainda são certo sucesso de acessos. [Vagrant Fácil e Útil](http://flaviosilveira.com/2012/vagrant-facil-e-util) que dá uma introdução ao Vagrant com um exemplo simples e [Vagrant, PuPHPet E PHP Built In](http://flaviosilveira.com/2013/vagrant-puphpet-e-php-built-in/) que apresenta o PuPHPet como um facilitador para criar ambientes e um experimento com o PHP Built In. O primeiro artigo é de 2012, o segundo de 2013. Passados três anos e vendo a busca disso não diminuir, quero trazer para quem ainda não conhece o [Docker](https://www.docker.com/).
<!--more-->

###Containers VS Virtual Machines
Muita coisa me anima no Vagrant: ser uma máquina virtual leve, poder deixar minha máquina limpa sem ter que instalar várias coisas, poder trabalhar com várias versões de software com facilidade, se aproximar bastante do ambiente de produção e poder experimentar sem medo.

Não vou entrar aqui na discussão filosófica sobre docker vs vagrant, quero apenas trazer uma alternativa a tudo que eu coloquei acima e, em um futuro, mostrar como o docker pode nos ajudar a experimentar ainda mais novas tecnologias.

Docker trabalha com containers, Vagrant com máquinas virtuais. Qual a diferença se você está começando com tudo isso? Não muita! Você pode pensar no container como uma máquina virtual se você está começando mas tenha em mente que todo o conceito e funcionamento é diferente. Ná prática você vai continuar com um mundo paralelo onde vai poder criar e experimentar suas coisas.

###O velho que é novo
Containers já existem há algum tempo dentro da nossa área com o que chamavamos de Linux Containers ou LXC. O que aparece com o Docker agora é uma maneira mais fácil de trabalhar com tudo isso e um engajamento da comunidade e das empresas de software gigantesco, trazendo uma gama de várias ferramentas prontas em formato de imagens. Com isso não vamos perder muito tempo com configurações e testar e descobrir tecnologias fica mais fácil.

Marque na agenda para pesquisar sobre libvirt, LXC e a história por trás da criação do Docker na França. Vale a pena! 

###Instalação e não só para Linux
Diferente dos antigos, o docker trouxe maneiras de trabalharmos com containers em qualquer sistema operacional. A maneira como ele faz isso está sempre evoluindo a cada versão. Pesquise como está para o seu sistema operacional. 

Eu não vou tratar aqui como instalar o Docker nem sua arquitetura básica, quero ir direto aos pontos mesmo que ainda ficando muito parecido com os primeiros passos da documentação oficial. A ideia é explicar as coisas um pouquinho diferente para quem não pegou da maneira que ficou lá e trazer umas maneiras diferentes de pensar.

###Hello World
Cada um tem a sua maneira de aprender as coisas, sujiro muito que você descubra a sua. Eu gosto de Hello World, começar do ultra básico e ir evoluindo e tentando entender passo a passo. Vamos fazer juntos e já vou explicando algumas coisas.

O Hello World com docker fica da seguinte maneira. Rode:

	docker run hello-world


####Imagens
O docker vai buscar uma imagem chamada hello-world. Imagens são a base dos containers, são como um cenário pronto que pode conter um sistema operacional e um conjunto de softwares por exemplo. 

Você não tem a imagem localmente, então o docker vai fazer o download dela. Para algumas imagens você vai ver o docker fazendo vários downloads paralelos para deixar as coisas mais rápidas.

####Saída
Uma vez que foi feito o download da imagem o docker vai subir o container e rodar o programa hello-world sozinho.

	Hello from Docker!
	This message shows that your installation appears to be working correctly.
	To generate this message, Docker took the following steps:
	 1. The Docker client contacted the Docker daemon.
	 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
	 3. The Docker daemon created a new container from that image which runs the
	    executable that produces the output you are currently reading.
	 4. The Docker daemon streamed that output to the Docker client, which sent it
	    to your terminal.
	
	To try something more ambitious, you can run an Ubuntu container with:
	 $ docker run -it ubuntu bash

Se é isso que aparece para você, está feito! Tudo funcionando! O docker já te provoca a tentar algo mais ambicioso e é para esse caminho que vamos:

###CentOS
A saída do Hello World te desafia a fazer um container Ubuntu. Como muita gente usa Ubuntu como máquina principal, pessoalmente sugiro tentar outra distro no container. Que tal CentOS?

	docker run -it centos bash

Novamente aqui o docker vai buscar por uma imagem, dessa vez do CentOS, se não tiver vai fazer download dela.

Novidades no comando:

* -i é o comando para interagir, vai manter o STDIN aberto.
* -t é para alocar um TTY(Talk to you) que é um terminal.

Com a imagem em mãos, o docker vai subir o container e executar o comando bash.

Note que a linha do seu terminal mudou e você deve estar dentro do container. Todo comando que você executar agora está sendo executado dentro do seu container com Ubuntu.

Experimente alguns comandos para comprovar. Por exemplo: **yum**.

###Attached
Vamos sair do nosso container sem matar ele. Segure CTRL e pressione P e em sequida Q.
Você está de volta para sua máquina principal. Vamos ver os containers que temos rodando?

	docker ps

O comando ps vai nos mostrar os containers que estão rodando com um id, o processo que estão executando, quando foram criados, seu status, portas e nome do container.

Como não passamos nenhum nome para nosso container, o docker deu um de seus nomes padrão.

Vamos voltar para nosso container CentOS? Para isso vamos fazer o seguinte comando:

	docker attach [id ou nome do container]

Com o ID ou nome do container, você consegue voltar para ele, o que chamam de attach.

Pense no Attach como você dentro do container. O padrão quando se cria um container é attach, e foi isso que aconteceu quando passamos o comando run, entramos no container.

###Detach
De dentro do container, digite exit. Isso vai matar o container e ele não vai existir mais. O mesmo vai acontecer se você fizer um CTRL+C por exemplo.

	docker ps -a
Com o comando acima, além de ver seus containers ativos (se houver) ele mostra também os containers inativos. Se você deu exit em seu container do CentOS, essa mensagem vai ser mostrada em status.

Agora vamos criar o container novamente, mas dessa vez passando uma opção detached, ou seja, vamos criar o container mas não vamos entrar nele. Vamos também dar um nome para nosso container

	docker run --name meu-centos -itd centos bash
	
Ao rodar docker ps você vê que seu container está rodando, com o comando **bash** e com o nome **meu-centos**

**Nesse ponto faça o exercício de entrar e sair de containers, criar outros e etc. Use Attach e CTRL+P+Q**

###Exec
As vezes precisamos apenas executar apenas um comando dentro de um container e entrar e sair dele seria muito chato e demorado. Para isso temos o Exec:
	
	docker exec meu-centos echo teste
	
Aqui o docker entrou no container, executou o comando **echo teste** em meu-centos e retornou a sua máquina.

###Comandos que você talvez precise
	#Para listar as imagens que você tem: docker images
	#Para remover containers: docker rm
	#Para remover imagens: docker rmi
	#Parar e reiniciar container: docker start / docker stop 

###Fechando
Aqui fizemos os pequenos primeiros passos com containers. Muito parecido com o proposto pela documentação oficial.

Te convido a explorar o [DockerHUB](https://hub.docker.com/) repositório oficial de imagens para criarmos containers. Procure ferramentas que você já trabalha, ferramentas que você quer experimentar, o uso de containers vai te ajudar a fazer testes rápidos e estudar qualquer coisa.

Com isso acredito que sua cabeça já começe a fervilhar de ideias de para onde podemos ir.
Me comprometo a evoluir esses exemplos aqui nas próximas semanas.

Grande Abraço!