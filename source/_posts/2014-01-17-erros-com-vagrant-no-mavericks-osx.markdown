---
layout: post
title: "Erros No Vagrant No Mavericks OSX?"
date: 2014-01-17 00:00:00
comments: true
categories: [shell]
permalink: ":year/erros-com-vagrant-no-mavericks-osx/"
---

<p>Há algum tempo a Apple liberou a nova versão de seu sistema operacional, o Mavericks OSX. Se você usa Macs e Vagrant para desenvolvimento deve ter percebido que as coisas de repente não rodaram mais.</p>

<p>[Ainda não sabe o que é Vagrant? Confira esses meus dois posts: <a href="http://flaviosilveira.com/2012/vagrant-facil-e-util/" title="Vagrant fácil e útil">http://flaviosilveira.com/2012/vagrant-facil-e-util/</a> e <a href="http://flaviosilveira.com/2013/vagrant-puphpet-e-php-built-in/" title="Vagrant, PuPHPet e PHP Built In">http://flaviosilveira.com/2013/vagrant-puphpet-e-php-built-in/</a>]</p>

<!--more-->


<p>Correndo atrás do que estava acontecendo cheguei no post do Stu Miller <a href="http://www.stumiller.me/fixing-vagrant-osx-mavericks-update/" title="Stu Miller : Fixing Vagrant after an Mavericks Update">http://www.stumiller.me/fixing-vagrant-osx-mavericks-update/</a> que mostra os comandos para sair desse problema.</p>

<p>Porém você vai descobrir, seja lendo os comentários no blog do Stu ou na prática, que a cada vez que desligar seu Mac terá que executar esses comandos. Para diminuir um pouco o saco de ter que fazer isso sempre, criei um Shell Script que você pode colocar para rodar automaticamente quando sua máquina liga ou ao menos não ter que ficar lembrando quais eram os comandos.</p>

<p><a href="../../assets/uploads/fix-mavericks.sh" title="Fix Mavericks Shell Script">Faça o download aqui!</a></p>

<p>Execute-o com SUDO.<br/>
Você passa um primeiro parâmetro com o caminho da sua máquina virtual.<br/>
O segundo parâmetro é opcional, caso a sua versão do <em>VirtualBox</em> seja maior ou igual que 4.3 apenas passe um <em>true</em>.<br/>
Exemplo:</p>

<pre class="brush: bash; title: ; notranslate" title="">sudo ./fix-maverick.sh seu-diretorio true
</pre>


<p>O script não está a prova de balas, é apenas uma ajuda para resolver o problema.<br/>
Abrindo o script você vê um código bem simples, checando se o <em>vagrant</em> está instalado, se você executou o comando como SUDO e se o caminho passado é válido.</p>

<p>Qualquer sugestão é só enviar. Abraços!</p>