---
layout: post
title: "Criando seu Container NGinx + PHP (Parte 1)"
date: 2017-01-14 00:00:00
comments: true
categories: [desenvolvimento, php]
permalink: ":year/criando-seu-container-nginx-php-1/"
---
Fala pessoal!<br/>Esse já é nosso terceiro artigo sobre docker:

- Já vimos como podemos iniciar com o Docker no artigo [http://flaviosilveira.com/2016/comece-com-docker](http://flaviosilveira.com/2016/comece-com-docker/). 
- Em seguida vimos como iniciar um Container com PHP 7 e usar seu servidor embutido (built in) em [http://flaviosilveira.com/2016/docker-php7-e-php-built-in](http://flaviosilveira.com/2016/docker-php7-e-php-built-in/).

Com isso já conseguimos trabalhar com o PHP, mas o servidor Built-in não é a maneira ideal para isso. Como podemos colocar o PHP como um todo rodando em um container Docker para a gente? Vamos responder a isso.

Para quem não leu os primeiros dois artigos citados acima, recomendo. Acredito que vá ficar melhor de entender o que vem abaixo. Temos bastante *tecnês*.
<!--more-->
###Sim, tem pronto por aí!

Nos artigos anteriores falamos sobre o DockerHub, repositório oficial de imagens para criarmos nossos containers. Estamos buscando um container que tenha para a gente um PHP e um NGinx, e claro que tem várias imagens prontas disso por aí.

Inclusive a que criamos nesse tutorial [https://hub.docker.com/r/flaviosilveira/php-nginx](https://hub.docker.com/r/flaviosilveira/php-nginx/).

Mas, para aprendermos algo novo, vamos construir nosso próprio container e com ele criar nossa imagem. Se você entendeu o conceito de containers e o que ele pode te trazer, pare e pense as maneiras que você teria para fazer isso. 

Conseguiu pensar em algumas?

###Nossa maneira
Que tal partirmos de um sistema operacional? Vamos de Debian. Acredito que é o meio caminho entre o que muitos conhecem, que é o Ubuntu, e legal para sair um pouco do mesmo. 

Todos os comandos abaixo já foram explicados nos artigos anteriores. Volta lá se perdeu algo! 

Lembrem-se do que sempre digo: ***Não é complicado! Se ficar complicado demais tem algo errado, volte e leia novamente, com mais calma***.

####SO
Rodando um container Debian, vmaos chamar ele de ***server***:

	docker run --name server -itd -p 80:80 debian

Confira seu container rodando
	
	docker ps
	
Vamos dar um update no Debian para dessa maneira ele atualizar os caminhos dos pacotes:

	docker exec server apt-get update

####NGinx
Terminado, podemos partir para a instalação do NGinx:<br/>**ATENÇÃO:** não esqueça do -y abaixo, ele serve para confirmar que você quer instalar o pacote. As vezes sem essa opção a saída não vem corretamente do container para sua máquina.

	docker exec server apt-get install nginx -y
	
Vamos checar se instalou tudo certo?

	docker exec server nginx -v
	
A saída deve ser algo como:

	nginx version: nginx/1.6.2
	
O NGinx está instalado, mas ainda não está rodando. Vamos iniciar ele?

	docker exec server service nginx start
	
Agora que o NGinx está rodando, você já é capaz de ir ao seu localhost e ver a página inicial do NGinx.

####PHP
Vamos agora instalar o PHP. Antes disso, vamos checar quais versões do PHP temos disponível para o Debian nessa versão.

	docker exec server apt-cache search php | grep fpm
	
Aqui retornou a versão 5 do FPM. Vamos com ela.<br/>**ATENÇÃO:** não esqueça do -y.

	docker exec server apt-get install php5-fpm -y

Vamos checar se instalou tudo certo?	
	
	docker exec server php --version

A saída deve ser algo como:

	PHP 5.6.29-0+deb8u1 (cli) (built: Dec 13 2016 16:02:08) 
	Copyright (c) 1997-2016 The PHP Group
	Zend Engine v2.6.0, Copyright (c) 1998-2016 Zend Technologies
    	with Zend OPcache v7.0.6-dev, Copyright (c) 1999-2016, by Zend Technologies

Para fechar igual a instalação do NGinx que fizemos acima, vamos iniciar o php-fpm?

	docker exec server service php5-fpm start

Feito!
    	
Sim! Você pode adicioanar os caminhos no debian para instalar a versão 7 do PHP. Aqui fizemos com a versão que havia disponível para facilitar esse tutorial.

###Hora de Configurar
Sistema Operacional, NGinx e PHP ok. Hora de configurar as coisas para rodarem.
Acima executamos todos os comandos de fora do container com ***docker exec***. Agora como vamos editar arquivos de configuração, acho que é melhor irmos para dentro do container.

	docker attach server
	
Seu terminal deve ter ficado com algo como ***root@id-do-seu-container***. Estamos dentro do container!

Para editar arquivos vamos precisar de um editor. Vou de ***Vim***, e vocês? Instalem o editor que você tiverem facilidade.

***ATENÇÃO:*** Lembra do -y nos comandos acima? Aqui não passamos esse parâmetro. Então você terá que responder com ***Y*** se você deseja instalar o pacote quando for questionado por isso. Ou adicione o ***-Y*** no comando abaixo ;-)

	apt-get install vim
	
Com o editor em mãos, vamos configurar o NGinx.
Vamos ao arquivo default de configuração. Nessa versão ele está no seguinte caminho:

	vim /etc/nginx/sites-available/default

O Arquivo vem com várias linhas comentadas para facilitar o seu entendimento.
Segue o meu arquivo abaixo. Deixei o mais enxuto para ele funcionar na porta 80.

	server {
    	listen   80;

    	root /var/www/app;
    	index index.php index.html;

    	location ~ \.php$ {
        	try_files $uri =404;
        	fastcgi_split_path_info ^(.+\.php)(/.+)$;
        	fastcgi_pass unix:/var/run/php5-fpm.sock;
        	fastcgi_index index.php;
        	fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        	include fastcgi_params;
    	}
	}

Após editar o arquivo, reinicie o ***NGinx***

	service nginx restart

Repare que colocamos como raiz o caminho ***/var/www/app***.
Vamos até ***/var/www***
	
	cd /var/www
	
Agora criamos a pasta app

	mkdir app
	
Vamos criar um arquivo ***index.php*** com uma função ***phpinfo*** dentro dele para fazermos um teste.

	<?php phpinfo(); ?>

Acesse localhost e veja o resultado.

###Hmm.. mas quando eu derrubar esse container?
É, você vai ter que fazer tudo novamente. Mas não entre em pânico! Que tal criarmos nossa própria imagem, e sempre que quisermos um container com NGinx+PHP, podemos usar nossa própria imagem. Como te parece?

Vamos para a parte 2 desse artigo para pegar essa ideia [http://flaviosilveira.com/2017/criando-seu-container-nginx-php-2](http://flaviosilveira.com/2017/criando-seu-container-nginx-php-2).