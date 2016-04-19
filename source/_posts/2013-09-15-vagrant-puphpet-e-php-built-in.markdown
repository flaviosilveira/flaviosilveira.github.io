---
layout: post
title: "Vagrant, PuPHPet E PHP Built In"
date: 2013-09-15 00:00:00
comments: true
categories: [desenvolvimento, php]
permalink: ":year/vagrant-puphpet-e-php-built-in/"
---

<p>Fala pessoal.<br/>
Hoje trago uma dica simples, talvez sem uma utilidade de pronto, mas que pode ser interessante para algum estudo.</p>

<p><strong>O que é Vagrant?</strong><br/>
Para quem ainda não conhece, Vagrant é uma ferramenta que vem revolucionando os ambientes de desenvolvimento.<br/>
Se você ainda não sabe nada sobre essa ferramenta, confira o post que escrevi aqui no blog: <a href="http://flaviosilveira.com/2012/vagrant-facil-e-util/">http://flaviosilveira.com/2012/vagrant-facil-e-util/</a>.</p>

<!--more-->


<p>Alguns pontos do Vagrant:<br/>
&#8211; Com o Vagrant você não precisa instalar apache e outras ferramentas e poluir sua máquina.<br/>
&#8211; Você pode criar uma máquina virtual para cada projeto e com isso ter uma versão igual ao seu servidor de produção, com a mesma versão de PHP, de MySQL e etc.<br/>
Com isso acaba aquela desculpa de &#8220;Na minha máquina funciona!&#8221;.<br/>
&#8211; Com o Vagrant você pode distribuir o mesmo ambiente para todo seu time de desenvolvimento, evitando funcionamentos diferentes entre pessoas do mesmo time.<br/>
&#8211; Muito mais.</p>

<p><strong>PuPHPet: Arquivos puppet</strong><br/>
Com arquivos puppet (.pp) você pode definir pacotes, programas e extensões a serem instaladas na sua máquina virtual.<br/>
Geralmente são coisas complicadas e sempre acaba surgindo um problema quando são feitos esses arquivos na mão.</p>

<p>Felizmente surge o PuPHPet <a href="https://puphpet.com/">https://puphpet.com/</a>, uma ferramenta online que cria o puppet para você. Você seleciona tudo o que você quer, incluindo pacotes PEAR, pacotes PECL, etc.<br/>
Permite também setar o XDebug, timezone, escolher versão do PHP, do MySQL, incluir o composer, muito mais.</p>

<p>Dê uma atenção especial na opção BOX IP Address. Nesse campo você define o ip da sua máquina virtual.<br/>
É esse IP que você vai digitar no browser da sua máquina e acessar o seu projeto.<br/>
Por padrão o PuPHPet traz o IP 192.168.56.101.</p>

<p><strong>O que é PHP Built In?</strong><br/>
Com a versão 5.4, o PHP trouxe uma novidade para os ambientes de desenvolvimento. O PHP Buitl In.<br/>
É um web server rodando direto em cima do PHP, mas apenas com propósitos de desenvolvimento.<br/>
Com um simples comando você define a porta da onde quer rodar o servidor, e pronto. Sem precisar de Apache, NGinx ou o que for.<br/>
Uma coisa rápida para testar seu projeto. Veja detalhes na documentação: <a href="http://www.php.net/manual/pt_BR/features.commandline.webserver.php">http://www.php.net/manual/pt_BR/features.commandline.webserver.php</a></p>

<p><strong>Mãos a Obra</strong><br/>
Instale a versão mais recente do Vagrant acessando a página de downloads em <a href="http://downloads.vagrantup.com/">http://downloads.vagrantup.com/</a>.<br/>
Uma dica é ter instalado o Virtual Box para que tudo corra bem. A instalação não tem segredos.</p>

<p>Um segundo passo é configurar a sua máquina com a ajuda do PuPHPet <a href="https://puphpet.com/">https://puphpet.com/</a>.<br/>
Escolha no mínimo uma versão 5.4 do PHP. Faça o download do arquivo e posicione onde melhor julgar na sua máquina.</p>

<p>Via console, acesse essa pasta e vamos subir a sua máquina virtual com o seguinte comando:</p>

<pre class="brush: bash; title: ; notranslate" title="">vagrant up
</pre>


<p>Esse comando irá fazer o download de tudo que você selecionou de configuração via PuPHPet e deixar a máquina online para você.<br/>
Ao final da configuração, você já é capaz de acessar a sua máquina via porta 80 por exemplo, digite em seu navegador o ip que foi setado no campo BOX IP Address no PuPHPet.</p>

<p>Mas que tal testar essa funcionalidade que veio com o PHP 5.4? Vamos colocar o PHP Built In para rodar.<br/>
Vamos acessar sua máquina virtual via ssh, com o seguinte comando:</p>

<pre class="brush: bash; title: ; notranslate" title="">vagrant ssh
</pre>


<p>Caso você precise do root para qualquer coisa, basta colocar um sudo na frente do que precisar.</p>

<p>Vamos configurar um pequeno projeto PHP apenas para ocasião de teste. Por exemplo:</p>

<pre class="brush: bash; title: ; notranslate" title="">cd /var/www
mkdir teste
cd teste
</pre>


<p>Dentro dessa pasta teste que criamos, crie um arquivo PHP simples, com um echo por exemplo.</p>

<p>Você será capaz de acessar isso digitando seu BOX IP/teste, mas, para testar o PHP Built In, entre com o seguinte comando:</p>

<pre class="brush: bash; title: ; notranslate" title="">sudo php -S 192.168.56.101:8080
</pre>


<p>Não esqueça de substituir 192.168.56.101 pelo seu BOX IP.<br/>
8080 é a porta que escolhemos aqui. Você pode definir a porta que quiser, com exceção das que já estão em uso.<br/>
** Qualquer comando executado nessa mesma janela, ou um ctrl+c irá derrubar o server.</p>

<p>Pronto, o PHP Built In está escutando na porta definida.<br/>
Você pode conferir isso abrindo um outro terminal e consultando os listenings com o comando:</p>

<pre class="brush: bash; title: ; notranslate" title="">netstat -ln
</pre>


<p>Lembrando que esse comando pode variar de acordo com a distribuição que você selecionou na sua BOX.</p>

<p>Pronto. Você pode acessar do seu browser o seu BOX IP:PORTA e acessar o seu projeto diretamente, sem barras nem nada.<br/>
Aqui eu acessei <a href="http://192.168.56.101:8080/.">http://192.168.56.101:8080/.</a></p>

<p><strong>Resumindo</strong><br/>
Escrevi esse post apenas como curiosidade. Sei que ele pode não ter nenhuma aplicação prática, mas de repente é uma para o pessoal conhecer o PHP Built In e ver até onde ele vai e porque ele está apenas disponível para desenvolvimento.</p>

<p>Grande Abraço!</p>