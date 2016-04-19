---
layout: post
title: "Redirecionando Usuários Do IPhone Para a Versão Mobile Do Seu Site – JavaScript"
date: 2009-07-19 00:00:00
comments: true
categories: [desenvolvimento, javascript, mobile]
permalink: ":year/redirecionando-para-versao-mobile/"
---

<div id="atencao">
  Atenção! O post abaixo foi escrito em uma época onde o desenvolvimento de sites mobile estava começando e as técnicas para se fazer isso ainda eram muito poucas. Embora a solução abaixo possa funcionar para alguns casos específicos, recomendo que você pesquise outras formas de trazer seu site para o mundo mobile, como Css-Query e outros.
</div>


<p>As pessoas que me acompanham sabem que há pouco mais de um mês adquiri um IPhone.<br/>
A minha operadora me ligou oferecendo alguns pontos que valiam desconto na aquisição do aparelho. Não perdi tempo e corri lá buscar.</p>

<p>Desde então as minhas leituras diárias começaram a se voltar mais para IPhone.<br/>
Desenvolvimento de aplicativos, desenvolvimento de sites, &#8216;manhas&#8217; para usar o aparelho, dicas para economizar bateria, e por ai vai.</p>

<p>O que trago hoje aqui faz parte dos meus estudos para criação de sites para o público que usa IPhone, que é, identificar que seu visitante está usando o aparelho e redirecioná-lo para a versão mobile do seu site.</p>

<p>A ideia é bem simples, e, para colocar ela em prática usamos JavaScript.</p>

<p>Primeiro crie um arquivo HTML e o prepare para receber um javaScript dentro das tags do cabeçalho.</p>

<pre class="brush: xml; title: ; notranslate" title="">&lt;html&gt;
&lt;head&gt;
&lt;title&gt;::: Teste IPhone :::&lt;/title&gt;
&lt;script type='text/javascript'&gt;
&lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;/body&gt;
&lt;/html&gt;

</pre>




<!--more-->


<p>Deixei apenas o necessário para o HTML funcionar acima.<br/>
Coloquei um título para constar, e abri as tags de script onde vai entrar o nosso JavaScript.</p>

<p>Em JavaScript temos um objeto que traz propiedades e métodos do nosso navegador, que é o <strong>navigator</strong>.<br/>
Você pode vê-lo em ação adicionando o seguinte código dentro das tags script:</p>

<pre class="brush: jscript; title: ; notranslate" title="">alert(navigator);
</pre>


<p>Esse objeto tem propiedades que nos trazem dados como o nome do browser, sua versão, dizer se os cookies estão habilitados e outros.</p>

<p>A propiedade que vamos usar é a <em>userAgent</em>, que traz um conjunto de informações do browser e do dispositivo que está acessando, que é o que precisamos.</p>

<pre class="brush: jscript; title: ; notranslate" title="">alert(navigator.userAgent);
</pre>


<p>Veja o resultado do código acima ao acessarmos a página. Repare nas informações retornadas:<br/>
<strong>No Firefox do Linux:</strong><br/>
<img class="alignnone size-full wp-image-103" title="linux-firefox" src="../../assets/uploads/2009/07/screenshot.png" alt="linux-firefox" width="628" height="313" /><br  style='clear:both;' /><br/>
<strong>No Safari do Mac:</strong><br/>
<img class="alignnone size-full wp-image-104" title="safari-mac" src="../../assets/uploads/2009/07/picture-2.png" alt="safari-mac" width="514" height="222" /><br  style='clear:both;' /><br/>
<strong>No Simulador do IPhone:</strong><br/>
<img class="alignnone size-full wp-image-105" title="simulador" src="../../assets/uploads/2009/07/picture-3.png" alt="simulador" width="299" height="586" /><br  style='clear:both;' /><br/>
<strong>No própio IPhone:<br/>
<img class="alignnone size-full wp-image-106" title="iphone" src="../../assets/uploads/2009/07/img_0095.png" alt="iphone" width="298" height="447" /></strong><br  style='clear:both;' /></p>

<p>Reparou que quando estamos lidando com o Iphone, essa informação aparece para a gente na propiedade do objeto ?<br/>
Caso estivessemos no IPod Touch, apareceria <em>IPod</em> ao invés de <em>IPhone</em> nas informações.</p>

<p>Agora basta fazer uma verificação para ver se a palavra Iphone ou Ipod está presente nas informações, e, se estiver, redirecionar para sua versão mobile.<br/>
Veja o código:</p>

<pre class="brush: jscript; title: ; notranslate" title="">if ((navigator.userAgent.indexOf('iPhone') != -1) || (navigator.userAgent.indexOf('iPod') != -1))
{
alert('IPhone!!!');
//Essa linha redireciona você para o endereço que você colocar
document.location = "http://www.flaviosilveira.com";
}
</pre>


<p>Qualquer dúvida estamos aí&#8230;Abraços!!!</p>