---
layout: post
title: "Docker, PHP7 e PHP Built In"
date: 2016-10-10 00:00:00
comments: true
categories: [desenvolvimento, php]
permalink: ":year/docker-php7-e-php-built-in/"
---
No artigo anterior ([Comece com Docker!](http://flaviosilveira.com/2016/comece-com-docker/)) descrevemos juntos alguns passos iniciais com o Docker. Criamos containers, usamos attached, detached, entramos, saímos, executamos comandos. Se você não está familiarizado a isso, te convido a visitar o artigo.

Sendo repetitivo, meu desejo com esses artigos sobre docker é passar para as pessoas as facilidades que containers nos dão para experimentar tecnologias. Que tal hoje experimentarmos o PHP7? Se você não teve a oportunidade de mexer um pouco com ele o Docker está aqui para facilitar as coisas. E para facilitar ainda mais vamos usar o recurso Built In, presente desde a versão 5.4, que nos traz um servidor web embutido. Assim não vamos precisar instalar nada mais.
<!--more-->
###PHP no DockerHub

No final do artigo anterior falamos sobre o [DockerHUB](https://hub.docker.com/), repositório oficial de imagens para criarmos nossos containers.

O [PHP tem um reposítorio oficial no Docker hub](https://hub.docker.com/_/php/) e é de lá que vamos começar. Nessa página temos várias informações desde o que é PHP até como usar a imagem, contribuir, instalar extensões e etc.

Nos comandos que usamos, fizemos ***Docker Run*** que verifica se já temos a imagem em nossa máquina e caso não tenha faz o download dela. Vamos aprender um comando novo.

	docker pull php
	
Com docker pull vamos fazer apenas o download da imagem, ele não vai iniciar um container para a gente direto como ***docker run*** faz, apenas o download.

Nesse comando temos a opção de especificar a versão que queremos do PHP. Não passando nada, vai vir para a gente a última. Exatamente o que estamos querendo aqui certo?

###Subindo Container PHP
Uma vez que a imagem está em nossa máquina, é hora de rodar o container. Vamos ver em que versão estamos?

	docker run php php --version

**Docker run** é nosso comando. **php** é o nome da nossa imagem e em seguida o comando que queremos executar no nosso container, **php --version**.

Ao final desse comando o container terá subido, executado **php --version**, mostra uma saída e mata o container. A saída dada para mim na data de hoje foi versão **PHP7.0.11**.

O Container morre, porque o comando que passamos executou e finalizou. Comprovamos isso rodando **docker ps**.

###PHP CLI
Na mesma pegada, vamos testar o PHP CLI com nosso container. PHP CLI é o php em linha de comando.

Mas antes vamos criar um script php para rodar no CLI. Criei uma pasta chamada **php** no meu diretório de desenvolvimento e dentro dele vou criar um script chamado **spaceship.php**.

	<?php

	// Testing Spaceship Operator
	echo 2 <=> 2; // 0
	echo 5 <=> 6; // -1
	echo 6 <=> 5; // 1

	echo "a" <=> "a"; // 0
	echo "a" <=> "b"; // -1
	echo "b" <=> "a"; // 1
	
O objetivo desse script é simplesmente testarmos o Spaceship, novo operador que veio com o PHP7. Vamos rodar ele em um container?

	docker run -v ~/dev/php:/usr/src/wd -w /usr/src/wd php php spaceship.php
	
**Docker run** é nosso comando. Com **-v** vamos fazer share do nosso diretório da nossa máquina local com um diretório de nosso container. Os dois vão estar espelhados. Com **-w** vamos dizer para nosso container php qual é nosso Working directory, nosso diretório de trabalho. Repare que coloquei o mesmo diretório que em nosso container é equivalente ao diretório em nossa máquina.

**php** é o nome da nossa imagem que vai servir de base para nosso container e **php spaceship.php** é nosso comando que vai rodar em nosso working directory.

A saída esperada é **0-110-11**, como nos comentários do script acima.
Já conhecia o Spaceship? Vale uma lida na documentação em [novas features PHP7](http://php.net/manual/en/migration70.new-features.php).

###PHP Built In
Finalmente, vamos finalizar com o PHP Built In.

Vamos primeiro lembrar como é o comando do PHP Built In. Para consultar o help do PHP Cli podemos fazer

	docker run -v ~/dev/php:/usr/src/wd -w /usr/src/wd php php --help

Com -S maiúsculo, temos o que procuramos:
	
	php -S 127.0.0.1:8080

Simples não? -S, IP e a porta para acessar.

Dessa vez vou explicar o comando que vamos fazer antes:
**Docker run** que é nosso comando para subir o container. **-p** vai mapear a porta 8080 da nossa máquina para a porta 8080 do container. **-v** como vimos anteriormente vai fazer o share do nosso diretório. **-w** especifica onde vai ser o working directory do container php. **php** é o nome da nossa imagem que vai servir de base para nosso container. E o comando que vamos executar dentro do container será **php -S 0.0.0.0:8080**. 

	docker run -p 8080:8080 -v ~/dev/php:/usr/src/wd -w /usr/src/wd php php -S 0.0.0.0:8080
	
Em meu exemplo eu estou usando uma docker machine que tem um IP **192.168.99.100**, quando passo para o comando do container um IP **0.0.0.0** ele é traduzido para o IP da minha docker machine.

Ao executar o comando, ele vai ficar esperando.

Acesso no navegador o seu IP passando a porta 8080, e acrescente **/spaceship.php**. O mesmo resultado visto anteriormente no terminal, agora está no seu navegador.

Para matar o container basta retornar ao terminal e dar um **CTRL+C**.

###Fechando
Hoje usamos a imagem do PHP. Para quem nunca havia provado o PHP7, fica a sugestão de fazer esse experimento bem facilmente usando containers e Docker. Aprendemos o comando para simplesmente fazer download de uma imagem e exploramos a imagem do PHP usando CLI e Built In.

Espero que sua cabeça esteja com ideias em cima do que foi passado aqui.

Grande Abraço!