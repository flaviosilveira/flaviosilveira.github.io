---
layout: post
title: "Criando seu Container com Dockerfile"
date: 2017-02-12 00:00:00
comments: true
categories: [desenvolvimento, php]
permalink: ":year/criando-seu-container-com-dockerfile/"
---
Foi uma longa jornada até criarmos nosso container da maneira que queríamos [flaviosilveira.com/2017/criando-seu-container-nginx-php-1/](http://flaviosilveira.com/2017/criando-seu-container-nginx-php-1/) e [flaviosilveira.com/2017/criando-seu-container-nginx-php-2/](http://flaviosilveira.com/2017/criando-seu-container-nginx-php-2/). Ainda assim temos alguns pontos chatos como o de ter de iniciar o Nginx e o PHP-FPM Manualmente.

Felizmente há uma maneira mais simples de montarmos nosso container e ainda fugindo do trabalho manual. Vamos usar Dockerfile!

Dockerfile é um arquivo onde colocamos tudo o que precisamos para nosso container. De qual container ele se origina, o que você quer instalar, que serviços quer rodar.

Se você está acompanhando a série de artigos sobre docker, basicamente vamos traduzir o que fizemos nos dois artigos anteriores para um Dockerfile.

No decorrer deste artigo vou me referir aos 2 anteriores praticamente o tempo todo. Caso você não os tenha lido, pode ficar um pouco fora de contexto para você, mas nada que vá comprometer o entendimento final.

<!--more-->

###Preparação
Crie uma pasta chamada *docker-test*, e dentro dela crie um arquivo chamado *Dockerfile*. Com a inicial maiúscula e sem extensão.

Isso é tudo que vamos precisar.

###Container de origem
No começo da parte 1 do artigo falamos sobre de qual container partiríamos. Entre Ubuntu e Debian, ficamos com o Debian.

Para dizer isso para o Dockerfile, usamos **FROM**
	
	FROM debian
	
Com essa diretiva, estamos partindo da última imagem do debian presente no DockerHub.

###Assine sua imagem
Use *MAINTENER* para assinar sua imagem, dizer aos outros quem é o mantenedor dela.
No meu caso:

	MAINTAINER Flavio Silveira

###Atualização e instalações
Passamos algum tempo atualizando o sistema e em seguida instalando o NGinx e o PHP-FPM. Fizemos isso de fora do container usando o comando *docker exec*.

No Dockerfile usamos RUN para criar o ambiente da nossa imagem

	RUN apt-get update
	RUN apt-get install -y nginx
	RUN apt-get install -y php5-fpm
	
Essas 3 linhas resumem muito do trabalho que foi feito na parte 1 do artigo. Elas indicam respectivamente que queremos atualizar o sistema operacional e em seguida instalar o NGinx e o php5-fpm. Simples assim!

###Configurações
Para configurar nosso container, entramos nele com o comando *docker attach* e criamos e alteramos o arquivo */etc/nginx/sites-available/default*. Fizemos um arquivo bem enxuto funcionando na porta *80* e apontando para */var/www/app*.

Copie o trabalho que fizemos com o arquivo default dentro do container para um arquivo local, dentro de nossa pasta *docker-test*, chame ele de *default*.

Agora vamos dizer para o Dockerfile que queremos copiar esse arquivo para a configuração do Nginx.

	COPY default /etc/nginx/sites-available/default
	
O primeiro parâmetro é o arquivo em nossa máquina, e o segundo é o lugar que ele vai parar em nossa imagem.

Os passos de criar a pasta app, não serão necessários. Você vai ver como o container vai se virar com isso sem trazer a dor de cabeça para você.

###Fechando sua imagem
Na parte 2 do artigo anterior criamos a imagem a partir do container que estavamos rodando. Infelizmente tinhamos de iniciar o NGinx e o PHP-FPM manualmente após fazer download da imagem para fazer as coisas acontecerem.

Aqui no Dockerfile vamos resolver esse problema.

Uma vez que nosso ambiente foi preparado com os comandos anteriores, agora vamos usar *CMD* para dizer como nosso container vai rodar.

	CMD service nginx start && service php5-fpm start && /bin/bash
	
Repare que diferente da diretiva *RUN*, com *CMD* concatenamos os comandos usando *&&*. Precisamos disso pois só podemos ter um *CMD* no Dockerfile.

Aqui respectivamente iniciarmos o Nginx, em seguida o PHP-FPM e executamos */bin/bash* para que o container fique de pé quando iniciado.

Caso a gente não use esse */bin/bash* aqui, teremos que passar ele quando rodarmos a imagem com *docker run*.

###Nosso Dockerfile
É isso! Já temos tudo o que precisamos no nosso *Dockerfile*.
Vejam como ficou:

	FROM debian

	MAINTAINER Flavio Silveira

	RUN apt-get update
	RUN apt-get install -y nginx
	RUN apt-get install -y php5-fpm

	COPY default /etc/nginx/sites-available/default

	CMD service nginx start && service php5-fpm start && /bin/bash
	
###Construindo a imagem
Para construir a imagem a partir do Dockerfile vamos executar o comando docker build.

	docker build -t flaviosilveira/php-nginx-2 .
	
Usamos o parâmetro -t para dar a nossa imagem um apelido, uma tag para que fique mais fácil levantar ela depois. Assim como no artigo anterior, coloque seu nome de usuário do DockerHub na frente da tag da imagem. Isso será necessário na hora do envio da imagem. No meu caso ficou *flaviosilveira/php-nginx-2*.

O ponto no final, indica o diretório aonde está o Dockerfile que você criou.

Você verá o docker executar passo a passo do seu Dockerfile em detalhes, acompanhe no seu terminal.

###Checando sua imagem e dando run
Com o comando *docker images* você vê sua imagem criada localmente. Vamos testa-lá?

	docker run --name usando-dockerfile -itd -p 8080:80 -v ~/dev/php:/var/www/app flaviosilveira/php-nginx-2

Coloquei um nome para meu container de *usando-dockerfile*.

Passamos a referência de portas, a 8080 de nossa máquina vai bater na 80 do container.

Compartilhei uma pasta local minha *~/dev/php* para a pasta */var/www/app* do container. Tudo que que for feito na pasta local, vai refletir na pasta dentro do container. */var/www/app* é o local para onde nosso config do NGinx aponta como diretório raiz.

Faça os testes com seus arquivos PHP e veja em funcionamento. 

Caso queira, acesse o container e confirme que seus serviços estão rodando e que o arquivo de configuração do NGinx foi copiado.

###Enviando ao Dockerhub
Para enviar a imagem para o DockerHub, vamos fazer o mesmo processo do artigo anterior.

	docker login

Caso não tenha usuário no DockerHub, não esqueça de criar antes.

E para enviar a imagem
	
	docker push flaviosilveira/php-nginx-2

Use com a tag que deu para sua imagem, com seu nome de usuário.

É isso! Acesse o DockerHub para conferir.

###Testando
Seguindo o mesmo que fizemos no final do último artigo vamos testar.

Antes de testar, vamos eliminar tudo que temos localmente, parar o container e remover a imagem.

	docker stop usando-dockerfile
	docker rm usando-dockerfile
	docker rmi flaviosilveira/php-nginx-2
	
Agora executamos o mesmo run que fizemos acima.

	docker run --name usando-dockerfile -itd -p 8080:80 -v ~/dev/php:/var/www/app flaviosilveira/php-nginx-2

A imagem não será encontrada localmente e será feito download dela diretamente do DockerHub.

Veja seu container rodando:
	
	docker ps
	
Viram como foi muito mais fácil usar o Dockerfile para criar nosso container? Por hoje é isso!

Grande abraço e até a próxima.