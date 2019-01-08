---
layout: post
title: "Criando seu Container NGinx + PHP (Parte 2)"
date: 2017-01-14 00:00:00
comments: true
categories: [desenvolvimento, php]
permalink: ":year/criando-seu-container-nginx-php-2/"
---
No final da [parte 1 desse artigo](http://flaviosilveira.com/2017/criando-seu-container-nginx-php-1), onde montamos um container com Debian, NGinx e PHP, nos deparamos com o seguinte: Se pararmos nosso container e precisar novamente de NGinx + PHP, teremos que partir do zero.

Para evitar isso, vamos criar nossa própria imagem, uma imagem que vai guardar o que fizemos até agora.
<!--more-->
###Saia do container
Primeiro vamos sair de nosso container com ***ctrl+p*** e em seguida ***ctrl+q***.<br/>***Dica:*** Não precisa soltar o ctrl.

###Conta no DockerHub
Vá até o DockerHub [https://hub.docker.com](https://hub.docker.com/) e crie sua conta.

Após isso volte para o terminal e faço o comando de login

	docker login
	
Irá pedir seu usuário e senha e feito!

###Criando Imagem
Para criar sua imagem, você vai precisar do ***ID*** do seu container, use ***docker ps*** para consultar. A primeira coluna vai te mostrar seu ***CONTAINER ID***.

Em seguida, execute o commit com o comando abaixo:

	docker commit id-do-seu-container flaviosilveira/php-nginx
	
Substitua no comando acima ***id-do-seu-container*** pelo id mostrado em ***docker ps***.

Fora o id, colocamos o nome que desejamos para nossa imagem. Escolhi php-nginx.

Repare que coloquei meu nome de usuário do DockerHub na frente do nome que quero para a imagem. Isso será necessário na hora do envio para o DockerHub.

O comando vai te retornar um hash SHA-256.

Confira sua imagem criada
	
	docker images
	
Sua imagem deve estar no topo dessa lista.

###Usando sua imagem localmente
Uma vez que vemos a imagem no comando ***docker images***, você já pode usar ela localmente.
***ATENÇÃO:*** Altere o meu nome de usuário abaixo pelo seu.

	docker run --name usando-imagem -itd -p 8080:80 flaviosilveira/php-nginx

Pontos de atenção:

- Como nossa imagem é baseada na do Debian, rodamos ela de maneira igual. Compare o comando run executado aqui com o da parte 1 desse artigo.
- Coloquei a porta 8080 do nosso host para apontar para a 80 do container (-p 8080:80), para não conflitar com a porta 80 do outro container (-p 80:80).

Outra coisa. O serviço do NGinx e do PHP5-FPM estão parados!

Você precisa iniciar eles para ver as coisas funcionando.

	docker exec minha-imagem service nginx start
	docker exec minha-imagem service php5-fpm start

Agora confira o resultado em ***localhost:8080***.

###Enviando sua imagem para o DockerHub
Já vimos em outros artigos o comando ***docker pull*** que serve para fazermos download de imagens para nossa máquina. Por padrão ele busca imagens do DockerHub, repositório padrão do docker.

Agora para enviarmos imagens para ele, temos o ***push***

	docker push flaviosilveira/php-nginx

###Testando
Antes de testar, vamos eliminar tudo que temos localmente. Parar o container e remover a imagem.

	docker stop usando-imagem
	docker rm usando-imagem
	docker rmi flaviosilveira/php-nginx
	
Agora basta tentar executar o mesmo run que fizemos acima.

	docker run --name usando-dockerhub -itd -p 8080:80 flaviosilveira/php-nginx

A imagem não será encontrada localmente e será feito download dela diretamente do docker hub.

Veja seu container rodando
	
	docker ps
	
Ou dê start no NGinx e no PHP-FPM e acesse no seu navegador na porta 8080 como colocamos acima.

###Compartilhando seus arquivos php com o container
Para compartilhar seus arquivos locais de PHP com o container, use o parâmetro de volume, como fizemos no artigo de [docker com PHP Built in](http://flaviosilveira.com/2016/docker-php7-e-php-built-in/).

	docker run --name usando-dockerhub -itd -p 8080:80 -v ~/dev/php:/var/www/app flaviosilveira/php-nginx
	
No parâmetro -v, você coloca o caminho da sua pasta local e separado por : (dois pontos) temos a pasta root que definimos no nosso NGinx.

Acesse o navegador para constatar.

###Resumo e Próximos passos?
Nesse artigo dividido em duas partes fizemos bastante coisa:
<br/>Usamos uma imagem debian, instalamos NGinx e PHP de fora do container com ***exec*** e depois entramos nele para configurar as coisas.

Criamos um login no dockerHub, criamos uma imagem nossa e agora ela está disponível para quem precisar.

Mas a maneira como fizemos não deixa claro de que imagem partimos ou ainda caso a gente desista de usar Debian e queira usar CentOS, você vai ter que novamente partir do zero dessa maneira que fizemos.

Nossos próximos passos são aprender um pouco sobre tags e criar nossa imagem usando DockerFile, que também vai nos ajudar a parar com a chatisse de ter que iniciar o php e o NGinx manualmente.

Vamos para um post sobre isso?

Até lá! Grande Abraço!