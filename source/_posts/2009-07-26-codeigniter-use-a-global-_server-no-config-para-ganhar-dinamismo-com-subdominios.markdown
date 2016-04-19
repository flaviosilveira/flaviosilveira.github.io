---
layout: post
title: "CodeIgniter: Use a Global $_SERVER No Config Para Ganhar Dinamismo Com Subdomínios"
date: 2009-07-26 00:00:00
comments: true
categories: [desenvolvimento, php]
permalink: ":year/codeigniter-use-a-global-_server-no-config-para-ganhar-dinamismo-com-subdominios/"
---

<p>Cenário:</p>

<p>Você compra o domínio principal, <em>www.site.com.br</em>. E você vai ter duas versões desse site, uma para cada cliente, que vai usar todas as regras de negócio iguais. A única diferença será o layout. Os clientes pediram os subdomínios <em>branco.site.com.br</em> e <em>preto.site.com.br</em>.</p>

<p>Você pode fazer duas cópias do site em pastas diferentes, mas levando em consideração que eles tem o mesmo CORE, isso não é muito inteligente. Pense se você tiver que fazer uma atualização, você vai ter de mexer em ambos os projetos.</p>

<p>Porque não fazer os subdomínios como links simbólicos para uma mesma pasta? De lá você pode fazer uma verificação. Se for um site, pega o layout branco, se for o outro pega o layout preto.</p>

<p>Problema:</p>

<p>No Codeigniter você define a URL principal do seu projeto nos arquivos de configuração, na variável <em>$config[&#8216;base_url&#8217;]</em>. Você não vai ter como colocar os subdomínios lá. O que fazer?</p>

<p>Solução:<br/>
Usar a Global <em>$_SERVER</em>.</p>

<p>Essa Global traz informações como o host que você está acessando, o email do administrador da máquina, o software usado, a configuração do TimeOut entre outras.</p>

<p>Para que você mesmo visualize tudo isso faça o seguinte. Abra o seu config.php do CodeIgniter e logo acima de onde está setado a variável <em>$config[&#8216;base_url&#8217;]</em> de um print_r, como abaixo:</p>

<pre class="brush: php; title: ; notranslate" title="">|--------------------------------------------------------------------------
| Base Site URL
|--------------------------------------------------------------------------
|
| URL to your CodeIgniter root. Typically this will be your base URL,
| WITH a trailing slash:
|
|       http://example.com/
|
*
print_r($_SERVER);
die;
$config['base_url']     = "http://www.site.com.br/";

</pre>




<!--more-->


<p>Veja em seu browser todas as opções que você tem nessa global.</p>

<p>Dê uma atenção na primeira opção que vêm no array, o <em>HTTP_HOST</em>. Ele traz o endereço primário que você está acessando. É o que você precisa para setar seu config de acordo com a url que seu visitante acessar.</p>

<p>Dando um print apenas nesse cara,</p>

<pre class="brush: php; title: ; notranslate" title="">|--------------------------------------------------------------------------
| Base Site URL
|--------------------------------------------------------------------------
|
| URL to your CodeIgniter root. Typically this will be your base URL,
| WITH a trailing slash:
|
|       http://example.com/
|
*
print_r($_SERVER['HTTP_HOST']);
die;
$config['base_url']     = "http://www.site.com.br/";

</pre>


<p>ele retorna o seu subdomínio.</p>

<p>Agora é só fazer uma adaptação.</p>

<pre class="brush: php; title: ; notranslate" title="">|--------------------------------------------------------------------------
| Base Site URL
|--------------------------------------------------------------------------
|
| URL to your CodeIgniter root. Typically this will be your base URL,
| WITH a trailing slash:
|
|       http://example.com/
|
*

$config['base_url']     = "http://" . $_SERVER['HTTP_HOST'];

</pre>


<p>Seja lá qual subdomínio você acessar, ele vai setar como <em>base_url</em> para você.</p>

<p>Caso você não use subdomínios, esse artifício pode ser usado para você deixar o base_url automatizado para seus projetos.</p>

<p>Espero que tenham curtido a idéia.<br/>
Qualquer dúvida só mandar.<br/>
Abraços!!</p>