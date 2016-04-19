---
layout: post
title: "JQuery E JQuery Price Para Formatar Seus Campos De Valor Monetário"
date: 2010-10-15 00:00:00
comments: true
categories: [desenvolvimento, javascript]
permalink: ":year/jquery-e-jquery-price-para-formatar-seus-campos-de-valor-monetario/"
---

<p>Salve pessoal.</p>

<p>Muita gente me manda emails ou mensagens no twitter achando que eu escrevi o Plugin JQuery Price para JQuery, que ajuda você a formatar seus campos de texto com valores monetários, valores de preço. Se você ler bem certinho na <a href="http://meiaduzia.com.br/cuducos2/priceformat/">página oficial do Plugin</a> (<a href="http://meiaduzia.com.br/cuducos2/priceformat/">http://meiaduzia.com.br/cuducos2/priceformat</a>), e também no código ao baixar ele, verá que eu apenas colaborei com uma nova função do plugin, uma necessidade minha no início do ano de 2009.</p>

<p>O Autor do Plugin é o <a href="http://www.meiaduzia.com.br/cuducos/">Eduardo Cuducos</a>, Um tremendo Designer e Desenvolvedor Web do estado de Santa Catarina que conheci por meio desse Plugin. <a href="http://www.meiaduzia.com.br/cuducos/">Aqui</a> você pode conhecer mais dele ou seguir seu <a href="http://twitter.com/cuducos">twitter</a> (<a href="http://twitter.com/cuducos">http://twitter.com/cuducos</a>) para pegar suas idéias, sejam de designer, política ou pensamentos de vida, que também valem a pena.</p>

<p>Para usar o Plugin é fácil.<br/>
Na <a href="http://meiaduzia.com.br/cuducos2/priceformat/">página oficial</a> consta alguns exemplos bem explicativos.<br/>
Mas se você ainda tem dúvidas vou reproduzí-los aqui.</p>

<p>Primeiro crie seu Html com o campo que quer formatar.<br/>
Não preciso dizer para você carregar a JQuery e o Plugin JQuery Price preciso ?</p>

<pre class="brush: xml; title: ; notranslate" title="">&lt;script type="text/javascript" src="jquery.js"&gt;&lt;/script&gt;
&lt;script type="text/javascript" src="jprice.js"&gt;&lt;/script&gt;
&lt;script type="text/javascript"&gt;
    
    function init()
    {
        
    }

    $(document).ready(init);
    
&lt;/script&gt;

&lt;/head&gt;
&lt;body&gt;

    &lt;h1&gt;Exemplo&lt;/h1&gt;

    &lt;label for="price"&gt;Valor:&lt;/label&gt;
    &lt;input type="text" id="price" /&gt;

&lt;/body&gt;

</pre>




<!--more-->


<p>Ok.<br/>
Reparem que eu já acrescentei um código JavaScript para chamar a funcão init assim que a página terminar de carregar. Isso evita que o JavaScript tente fazer algo com algum campo do Html que não esteja criado ainda. Uma outra solução para isso poderia ser colocar esse código ao final do Html.</p>

<p>Para o uso básico do Plugin, basta fazer a chamada do campo (no meu caso chamei pelo id) e acrescentar o método priceFormat veja:</p>

<pre class="brush: jscript; title: ; notranslate" title="">function init()
{
    $('#price').priceFormat();
}

$(document).ready(init);

</pre>


<p>Com isso seu input já formata automaticamente os números inseridos nele para as configurações padrões do Jquery Price. Ah sim, ele impede que você digite letras e alfanuméricos nesse campo também.</p>

<p>Ficou legal não?<br/>
Mas você não quer esse valor em doláres, você está lidando com o seu Brasil Brasileiro.<br/>
Vamos personalizar isso então.</p>

<pre class="brush: jscript; title: ; notranslate" title="">function init()
{
    $('#price').priceFormat({
        prefix: 'R$ ',
        centsSeparator: ',',
        thousandsSeparator: '.'
    });
}

</pre>


<p>Passando parâmetros para funcão em formato de array, conseguimos personalizar nosso input conhecendo algumas propiedades do plugin.</p>

<p>Com a propiedade prefix, alteramos o que vem antes dos números.<br/>
Repare que foi dado um espaço após o cifrão para ficar melhor visivelmente dentro do input.<br/>
Em seguida foi modificado o separador de centavos para uma vírgula e o separador de milhar para um ponto.</p>

<p>Muito fácil não ??</p>

<p>E chegamos ao momento mais esperado (Ou não).<br/>
Qual foi a minha colaboração com o Plugin ? Qual foi meu problema ?</p>

<p>Eu precisava limitar o valor que o usuário digitava.<br/>
Se você testar os exemplos que fizemos até aqui, verá que você pode inserir números até cansar.</p>

<p>Na época fiz um código meio xulo para resolver o problema, porque estava começando com JQuery e não tinha muita desenvoltura para alterar seus plugins. Mandei o código para o Cuducos que fez as devidas adaptações, não estragando a facilidade de uso do plugin.<br/>
Vamos a um exemplo:</p>

<pre class="brush: jscript; title: ; notranslate" title="">function init()
{
    $('#price').priceFormat({
        prefix: 'R$ ',
        centsSeparator: ',',
        thousandsSeparator: '.',
        limit: 6
    });
}

</pre>


<p>Passando mais uma propiedade para o método, chamada limit, agora você só pode inserir 6 numerais dentro do seu input.</p>

<p>Um outro limitador que temos é o de casas para os centavos.</p>

<pre class="brush: jscript; title: ; notranslate" title="">function init()
{
    $('#price').priceFormat({
        prefix: 'R$ ',
        centsSeparator: ',',
        thousandsSeparator: '.',
        limit: 6,
        centsLimit: 4
    });
}

</pre>


<p>Difícil ? Acredito que não certo ?<br/>
Experimente outros valores e confira os resultados.</p>

<p>Por hoje é isso pessoal.<br/>
Demos uma passada por todo o uso do plugin JQuery Price além de conhecer a história de como colaborei para o plugin. Espero ter tirado as dúvidas do pessoal que me manda emails e afins.</p>

<p>Agradecimentos imensos para o <a href="http://www.meiaduzia.com.br/cuducos/">Eduardo Cuducos</a> que adicionou meu nome dentro do projeto do plugin pela minha pequena colaboração, tornando o meu nome mais visível para a comunidade de desenvolvimento.</p>

<p>Qualquer coisa é só entrar em contato.<br/>
Abraços!</p>