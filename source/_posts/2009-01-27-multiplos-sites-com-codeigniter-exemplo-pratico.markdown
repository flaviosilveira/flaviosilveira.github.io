---
layout: post
title: "Múltiplos Sites Com CodeIgniter – Exemplo Prático"
date: 2009-01-27 00:00:00
comments: true
categories: [desenvolvimento, php]
permalink: ":year/multiplos-sites-com-codeigniter-exemplo-pratico/"
---

<p>Devido a muita procura do post sobre a restruturação do CodeIgniter para trabalhar com múltiplos sites (<a href="http://flaviosilveira.com/2008/alterando-configuracao-do-codeigniter/">Múltiplos sites com CodeIgniter</a>), fiz um passo a passo aqui da estrutura para o pessoal entender melhor.</p>

<p>Estava recebendo muitas dúvidas, vamos ver se com este exemplo consigo deixar as coisas mais claras para todos.</p>

<p><strong>Começando do zero.</strong></p>

<p>Baixei a <a href="http://codeigniter.com/downloads/">última versão do CodeIgniter</a>.<br/>
Descompacto ela no meu <em>desktop</em>.</p>

<p>Dentro dessa pasta veio o <em>system</em>, o <em>user_guide</em>, o <em>index.php</em> e o <em>license.txt</em>.<br/>
Costumo deletar o User_guide, pois uso a documentação online.</p>

<p><strong>Atenção agora ! </strong><br/>
Dentro da pasta system temos a pasta <em>application</em>. É esta pasta que faz o seu site funcionar. Com esta informação em mente vamos em frente.</p>

<p>Para começar a trabalhar com o servidor. Começe criando uma pasta para cada site. Como exemplo <em>site1</em> e <em>site2</em>.<br/>
<img class="alignnone size-full wp-image-61" title="ex1" src="../../assets/uploads/2009/01/ex1.jpg" alt="ex1" width="99" height="77" /><br/>
<br style="clear: both;" /></p>

<!--more-->


<p>O que o site vai precisar para funcionar ? Sim, como vimos acima é a pasta <em>application</em>. Dentro da pasta de cada site vamos precisar de uma application.<br/>
<img class="alignnone size-full wp-image-62" title="ex2" src="../../assets/uploads/2009/01/ex2.jpg" alt="ex2" width="160" height="486" /><br/>
<br style="clear: both;" /><br/>
A pasta <em>application</em>, claro, deve ir com a estrutura que vem por padrão nela, como você deve ter reparado na imagem acima.</p>

<p>Agora que já temos o local dos sites prontos, precisamos do que faz o Codeigniter funcionar, que é todo o restante da pasta <em>system</em>. Essa pasta deve estar no mesmo nível dos seus sites.<br/>
<img class="alignnone size-full wp-image-63" title="ex3" src="../../assets/uploads/2009/01/ex3.jpg" alt="ex3" width="99" height="86" /><br/>
<br style="clear: both;" /><br/>
Ok. Quase lá.<br/>
Agora, sabe aquele <em>index.php</em> que veio quando descompactamos o codeIgniter ? Como digo no <a href="http://flaviosilveira.com/2008/alterando-configuracao-do-codeigniter">outro post</a>, é ele quem indica o caminho da pasta <em>application</em> do seu site, e também do core do codeIgniter. Logo, vamos precisar de um deles para cada site.<br/>
<img class="alignnone size-full wp-image-64" title="ex4" src="../../assets/uploads/2009/01/ex4.jpg" alt="ex4" width="139" height="150" /><br/>
<br style="clear:both;" /><br/>
Agora precisamos editar esse arquivo index.php. Vamos começar pelo do site1.<br/>
Procure pela linha</p>

<pre class="brush: php; title: ; notranslate" title="">$system_folder = "system"
</pre>


<p>Esta variável indica aonde está o core do seu sistema, a pasta <em>system</em>.<br/>
No nosso caso ela está um nível acima, então basta mudar para</p>

<pre class="brush: php; title: ; notranslate" title="">$system_folder = "../system"
</pre>


<p>Logo na sequência você deve ver a linha</p>

<pre class="brush: php; title: ; notranslate" title="">$application_folder = "application"
</pre>


<p>Essa é a variável que indica onde está a pasta application desse site (lembrando&#8230;estamos alterando o site1). O caminho está correto, então, mantemos assim.</p>

<p>Faça o mesmo para o site2, indicando onde está o core do codeIgniter(pasta <em>system</em>) e a pasta <em>application</em>.</p>

<p>Está feito!</p>

<p>Agora, apenas para ficar mais explícito, vamos alterar a view de cada site.<br/>
Dentro de <em>Application</em> > <em>views</em>, temos o arquivo <em>welcome_message.php</em>.<br/>
<img class="alignnone size-full wp-image-65" title="ex5" src="../../assets/uploads/2009/01/ex5.jpg" alt="ex5" width="203" height="213" /><br/>
<br style="clear:both;" /><br/>
Dentro desse arquivo, vem a mensagem padrão de boas vindas do codeIgniter. Na do site1 tirei tudo que havia (ctrl + a &#8211; del) e coloquei apenas o título</p>

<pre class="brush: xml; title: ; notranslate" title="">&lt;h1&gt;::: SITE 1 :::&lt;/h1&gt;
</pre>


<p>e na do site2 apenas o título</p>

<pre class="brush: xml; title: ; notranslate" title="">&lt;h1&gt;::: SITE 2 :::&lt;/h1&gt;
</pre>


<p>Agora basta acessar as pastas para conferir o resultado.</p>

<p>Para detalhes mais técnicos desse step by step, confira o <a href="http://flaviosilveira.com/2008/alterando-configuracao-do-codeigniter">antigo post</a>.</p>

<p>Ainda com dúvida ? <a href="http://www.flaviosilveira.com/assets/uploads/multiplosSitesCI.rar">Faça aqui o download dos arquivos</a>.</p>

<p>Caso ainda tenha sobrado dúvidas&#8230;entre em contato.<br/>
Abraços !!!</p>