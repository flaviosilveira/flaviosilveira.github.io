---
layout: post
title: "Habilitando Layouts No CodeIgniter (Template Engine) – Parte 1"
date: 2010-02-18 00:00:00
comments: true
categories: [desenvolvimento, php]
permalink: ":year/habilitando-layouts-no-codeigniter-template-engine-1/"
---

<div id="atencao">
  <p>
    Atenção!! Este artigo foi escrito em cima da versão 1 do Codeigniter. Para detalhes de como usar com a versão 2 do framework <a href="http://flaviosilveira.com/2011/codeigniter-2-templates-e-layouts">clique aqui</a>.
  </p>
</div>


<p>Vejo muitos desenvolvedores criticarem o CodeIgniter por ele não utilizar o conceito de Layout ou ter um Template Engine dentro dele.</p>

<p>Template engine ou o conceito Layouts , falando em um exemplo rápido e prático seria mais ou menos o seguinte:<br/>
Pense que você tem um topo e um rodapé que nunca mudam no seu portal.<br/>
Ou seja, muda apenas o meio das páginas. Veja a figura abaixo.</p>

<p><img class="alignnone size-full wp-image-345" title="Screen shot 2011-05-20 at 2.22.38 PM" src="../../assets/uploads/2010/02/Screen-shot-2011-05-20-at-2.22.38-PM.png" alt="" width="239" height="217" /><br/>
<br style="clear: both;" /><br/>
E aí? Você vai ter que colocar esse topo e esse rodapé em todas as páginas que você chamar?<br/>
Ou você é malandro e vai fazer um include dentro das telas?</p>

<!--more-->


<p>O Include seria uma solução interessante mais uma Template Engine faria isso sozinho para você.</p>

<p>Pra quem não conhece nenhuma solução para isso, o <a href="http://www.smarty.net/">Smarty</a> é uma template Engine das mais conhecidas no mundo do PHP.<br/>
Você tem uma lista com outras sugestões de Templates Engine nesse link da <a href="http://www.webresourcesdepot.com/19-promising-php-template-engines/">web Resources</a><br/>
Outros frameworks como o CakePHP tem uma solução dentro dele que faz esse trabalho.</p>

<p>Nesses tempos que desenvolvo em CodeIgniter já vi bizarrices do tipo colocar o Smarty dentro do CodeIgniter ou trazer bibliotecas de outras frameworks para o Core do CodeIgniter.</p>

<p>Mas podemos estender o Core do Framework e fazer ele trabalhar junto com a gente sem precisar de muitas manobras e malabarismos. Na documentação do CodeIgniter achamos essa prática com o nome de Hooks ou se preferir o português ganchos.</p>

<p>Há alguns anos um cara que considero um dos Gurus do desenvolvimento, <a href="http://www.mozartpetter.com/pt/">Mozart Petter</a>, o qual tive a honra de trabalhar junto, pesquisou uma solução nesse sentido para que não precisássemos abandonar o CodeIgniter.</p>

<p>Você encontra vários links pesquisando no google por Layouts in CodeIgniter, onde destaco o seguinte Blog <a href="http://hasin.wordpress.com/2007/03/05/adding-yield-codeigniter/">http://hasin.wordpress.com/2007/03/05/adding-yield-codeigniter/</a></p>

<p>Abaixo vou colocar uma solução em 7 passos para você implementar isso em seu projeto de CI.<br/>
É importante que você procure entender em cada passo como o CodeIgniter vai visualizar isso tudo.<br/>
<em>*Não se deixe confundir. É fácil. Se ficar difícil há algo errado, volte e reveja os passos.</em></p>

<p>Como os códigos são muito extensos, vou dividir em dois posts.<br/>
Parte 1 &#8211; Esse (passo 1 ao 4) e Parte 2 (passo 5 ao 7) que você <a href="http://flaviosilveira.com/2010/habilitando-layouts-no-codeigniter-template-engine-2">acessa aqui</a>.</p>

<p>Para quem não estiver com muita paciência, estou disponibilizando também um exemplo pronto de tudo funcionando que você pode <a href="../../assets/uploads/2010/02/projetoExemplo.zip">baixar aqui</a>.<br/>
Apenas confira se o .htaccess serve para o seu servidor ou máquina.</p>

<p><strong>DETALHE IMPORTANTE:</strong><br/>
Esse projeto de exemplo foi atualizado no dia 20 de novembro de 2010. Sugestão do <a href="http://diegofelix.com.br/">Diego Felix</a> (<a href="http://twitter.com/diegofelix">@diegofelix</a>).<br/>
Confira a explicação da alteração no final da segunda parte ou <a href="http://flaviosilveira.com/2010/habilitando-layouts-no-codeigniter-template-engine-2/#explicacao">clicando aqui</a>.</p>

<p><strong>1 &#8211; Habilitando o Codeigniter para estender o Core</strong></p>

<p>A primeira coisa a fazer é habilitar o codeIgniter para estender o Core, permitir os hooks.<br/>
Isso é feito no arquivo config.php dentro da pasta config.<br/>
Procure a variável $config[&#8216;enable_hooks&#8217;] e troque seu valor para TRUE, ficando como abaixo.</p>

<pre class="brush: php; title: ; notranslate" title="">/*
|--------------------------------------------------------------------------
| Enable/Disable System Hooks
|--------------------------------------------------------------------------
|
| If you would like to use the "hooks" feature you must enable it by
| setting this variable to TRUE (boolean).  See the user guide for details.
|
*/
$config['enable_hooks'] = TRUE;
</pre>


<p>Pronto! Próximo passo.</p>

<p><strong>2 &#8211; Definindo um Hook</strong></p>

<p>Dentro da pasta config temos um arquivo onde deve ser feitas as definições dos hooks que você quer utilizar.<br/>
É o arquivo hooks.php. Para cada hook é preciso definir um array com alguns parâmetros para que o CodeIgniter saiba o que fazer.</p>

<p><em>Importante:</em> O índice do array vai funcionar apenas como nome do seu hook. Você não vai usá-lo em nenhum lugar a princípio.</p>

<p>Para o nosso Hook vamos definir.</p>

<ul>
<li>O nome da Classe que você precisa.</li>
<li>O nome do método da classe que você deseja chamar.</li>
<li>O nome do arquivo onde está desenvolvida a classe.</li>
<li>O directório onde ela se encontra.</li>
</ul>


<p>Fica da seguinte forma:</p>

<pre class="brush: php; title: ; notranslate" title="">$hook['display_override'][] = array('class' =&gt; 'Layout',
'function' =&gt; 'init',
'filename' =&gt; 'Layout.php',
'filepath' =&gt; 'hooks');
</pre>


<p>Esses itens podem variar de acordo com o que você quiser ou precisar fazer.<br/>
O manual é uma grande referência para te ajudar com isto e traz alguns detalhes que não abordo aqui.</p>

<p>Certo! Você habilitou e definiu um Hook, ou gancho. Vamos para o próximo passo.</p>

<p><strong>3 &#8211; Adicionando algumas constantes necessárias</strong></p>

<p>No arquivo index da aplicação são definidas algumas constantes que ajudam no desenvolvimento da nossa aplicação, como por exemplo,<br/>
a extensão dos arquivos que serão usados, constante EXT, e o BASEPATH que traz o caminho da pasta do sistema.</p>

<p>Vamos adicionar aqui mais 3 constantes que vai nos facilitar lá na frente quando formos fazer nossa classe.</p>

<ul>
<li>LAYOUTPATH &#8211; Caminho onde ficará os layouts que construirmos.</li>
<li>JSPATH &#8211; Caminho onde ficará os arquivos com javascript.</li>
<li>CSSPATH &#8211; Caminho onde ficará os arquivos de estilo. CSS.</li>
</ul>


<p>Ficando da seguinte forma:</p>

<pre class="brush: php; title: ; notranslate" title="">/*
|---------------------------------------------------------------
| DEFINE APPLICATION CONSTANTS
|---------------------------------------------------------------
|
| EXT       - The file extension.  Typically ".php"
| SELF      - The name of THIS file (typically "index.php")
| FCPATH    - The full server path to THIS file
| BASEPATH  - The full server path to the "system" folder
| APPPATH   - The full server path to the "application" folder
|
*/
define('EXT', '.php');
define('SELF', pathinfo(__FILE__, PATHINFO_BASENAME));
define('FCPATH', str_replace(SELF, '', __FILE__));
define('BASEPATH', $system_folder.'/');
define('LAYOUTPATH', $application_folder.'/layouts/');
define('JSPATH', $application_folder . '/js/');
define('CSSPATH', $application_folder . '/css/');
</pre>


<p>Reparem que usei a variável <em>$application_folder</em>, que é definida no mesmo arquivo, para completar o caminho das minhas constantes.<br/>
Você pode e deve mudar isso de acordo com seu projeto.</p>

<p>Essas constantes vão facilitar também para caso você precise mudar o caminho dos arquivos CSS por exemplo. Basta alterar aqui.</p>

<p><strong>4 &#8211; Construindo seu Layout</strong></p>

<p>Vamos agora construir o seu Layout.<br/>
Seria aquele topo e aquele rodapé que você não quer mexer. Ou um menu lateral.<br/>
Você pode construir o que quiser.</p>

<p>O local onde vamos criar nossos layouts foi definido na constante LAYOUTPATH.</p>

<p>Você pode ter quantos layouts quiser e nomeá-los como quiser.<br/>
Mas quando formos construir a classe você verá que definimos um Layout default para quando nenhum for chamado.<br/>
É esse que vamos criar agora. default.php</p>

<p>No exemplo abaixo eu criei um topo que tem um menu e um rodapé simples.</p>

<pre class="brush: xml; title: ; notranslate" title="">&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN"
"http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd"&gt;
&lt;html&gt;
&lt;head&gt;

&lt;meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1"&gt;
&lt;title&gt;{title_for_layout}&lt;/title&gt;

{css_for_layout}
            {js_for_layout}

&lt;/head&gt;
&lt;body&gt;
&lt;div id="geral"&gt;

&lt;div id="topo"&gt;
&lt;ul id="menu"&gt;
&lt;li&gt;&lt;a href="#"&gt;Link&lt;/a&gt;&lt;/li&gt;
&lt;li&gt;&lt;a href="#"&gt;Link&lt;/a&gt;&lt;/li&gt;
&lt;li&gt;&lt;a href="#"&gt;Link&lt;/a&gt;&lt;/li&gt;
&lt;li&gt;&lt;a href="#"&gt;Link&lt;/a&gt;&lt;/li&gt;
&lt;li&gt;&lt;a href="#"&gt;Link&lt;/a&gt;&lt;/li&gt;
&lt;li&gt;&lt;a href="#"&gt;Link&lt;/a&gt;&lt;/li&gt;
&lt;li&gt;&lt;a href="#"&gt;Link&lt;/a&gt;&lt;/li&gt;
&lt;/ul&gt;
&lt;/div&gt;

&lt;div id="meio"&gt;

{content_for_layout}

&lt;/div&gt;

&lt;br style="clear: both;" /&gt;

&lt;div id="rodape"&gt;
&lt;p class="rodape"&gt;
Todos os direitos reservados - Bla Bla Bla
&lt;/p&gt;
&lt;/div&gt;

&lt;/div&gt;
&lt;/body&gt;
&lt;/html&gt;

</pre>


<p>É necessário prestar atenção em 4 variáveis que deixamos soltas no meio desse HTML do Layout.</p>

<ul>
<li>Primeira &#8211; {title_for_layout}</li>
<li>Segunda &#8211; {css_for_layout}</li>
<li>Terceira &#8211; {js_for_layout}</li>
<li>Quarta &#8211; {content_for_layout}</li>
</ul>


<p>Explicando rapidamente:<br/>
Essas Strings vão ser substituídas de acordo com o que definirmos no Controller em um próximo passo.</p>

<p>No lugar de {title_for_layout} irá o título da página. É legal podermos definir um título pelo controlador para deixá-lo dinâmico e assim ajudar no SEO.</p>

<p>No lugar de {css_for_layout} e {js_for_layout} entrarão os arquivos de CSS e JavaScript que definirmos para nossa página.<br/>
Você não precisa chamar todos os CSS ou JavaScripts se não for usá-los. Essa é uma grande sacada dessa solução.<br/>
Lembro de pegar projetos em Smarty onde estavão definidos inúmeros JavaScripts e CSS em um top.php onde em várias páginas eles nem era usados.</p>

<p>Por último, no lugar de {content_for_layout} irá o conteúdo da nossa View.<br/>
É o meio, o que muda.<br/>
É o que vamos fazer no próximo passo que está no <a href="http://flaviosilveira.com/2010/habilitando-layouts-no-codeigniter-template-engine-2">próximo post</a>.</p>