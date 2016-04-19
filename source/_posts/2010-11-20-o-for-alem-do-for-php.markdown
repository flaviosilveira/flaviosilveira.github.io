---
layout: post
title: "O for Além Do for – PHP"
date: 2010-11-20 00:00:00
comments: true
categories: [desenvolvimento, php]
permalink: ":year/o-for-alem-do-for-php/"
---

<p>Salve pessoal!</p>

<p>O Post que trago hoje trata de algo bem simples mas que pode não ser muito comum para algumas pessoas.<br/>
São usos não muito populares de um de nossos laços de repetição, o FOR.</p>

<p>Quando estamos aprendendo uma linguagem, bem no início, os manuais parecem mais nos confundir do que ajudar.<br/>
O que fazemos ?? Saímos em busca de uma comunicação mais direta em Blogs ou Sites.</p>

<p>Essas fontes resolvem nosso problema mais podem acabar deixando alguns vácuos quando se trata de estruturas básicas, como é o caso do FOR.</p>

<p>E sobre o FOR eu te pergunto o seguinte:<br/>
Você sabia que os parâmetros passados para ele são opcionais ??<br/>
Você sabia que pode passar quantas variáveis quiser para os parâmetros ??</p>

<p>Se já sabe maravilha, caso não, vamos ver como isso funciona.</p>

<!--more-->


<p>Nesse primeiro exemplo temos nosso FOR comum, como todos aprendemos:</p>

<pre class="brush: php; title: ; notranslate" title="">&lt;?php

        for($i = 0; $i &lt; 5; $i++)
        {
                echo $i;
                echo '&lt;br /&gt;';
        }
</pre>


<p>Nesse segundo exemplo, retiramos o primeiro parâmetro do FOR, e deixamos a variável $i definida fora do laço:<br/>
Repare que o resultado que vai sair na tela, vai ser o mesmo do exemplo anterior.</p>

<pre class="brush: php; title: ; notranslate" title="">&lt;?php

        $i = 0;

        for(; $i &lt; 5; $i++)
        {
                echo $i;
                echo '&lt;br /&gt;';
        }

</pre>


<p>Agora, vmaos tirar o terceiro parâmetro, e incrementar a variável dentro do laço.</p>

<pre class="brush: php; title: ; notranslate" title="">&lt;?php

        $i = 0;

        for(; $i &lt; 5;)
        {
                echo $i;
                echo '&lt;br /&gt;';
                $i++;
        }

</pre>


<p>Por último, vamos retirar o segundo parâmetro.</p>

<pre class="brush: php; title: ; notranslate" title="">&lt;?php

        $i = 0;

        for(; ; )
        {
                echo $i;
                echo '&lt;br /&gt;';

                if($i == 5)
                {
                        break;
                }

                $i++;
        }

</pre>


<p>Repare que em todos esses exemplos acima, fugimos do Loop infinito com alguma condição ou mecanismo que colocamos dentro do laço. Tome cuidado. Esse último exemplo se não for feito nada dentro do laço, gera facilmente um Loop infinito.</p>

<p>Outra opção que temos é usar mais de uma variável para cada parâmetro.<br/>
Confira:</p>

<pre class="brush: php; title: ; notranslate" title="">&lt;?php

        $w = 2;

        for($i = 1, $j = 9; $j &gt; 0; $j - $i, $w*=2)
        {
                echo $w;
                echo '&lt;br /&gt;';
        }
</pre>


<p>Vamos analisar o exemplo acima.<br/>
Definimos para o loop a variável <em>$i</em> e a variável <em>$j</em>.<br/>
O segundo parâmetro, que define até quando nosso loop vai rodar, nos mostra que será enquanto <em>$j</em> for maior que zero.<br/>
E no último parâmetro, definimos que a cada volta <em>$j</em> vai diminuir o valor de <em>$i</em>, e que <em>$w</em>, que é uma variável que está definida fora do loop, será multiplicada por 2.<br/>
Dentro do loop, pedimos para exibir <em>$w</em>.<br/>
Faça o teste. Confira a saída.</p>

<p>Com esses exemplos acredito que já conseguimos absorver mais usos do que aquele que estamos acostumados do FOR. Todos eles são tratados na <a href="http://br.php.net/manual/pt_BR/control-structures.for.php">documentação</a> e também tem uns exemplos bem bacanas nos comentários dela que valem a pena olhar.</p>

<p>E aí você me pergunta… &#8220;E um uso prático disso?? Uma situação real ??&#8221;</p>

<p>De cara assim não consigo dar uma resposta, um exemplo.<br/>
Mas com isso eu lembro de uma entrevista que um dos melhores guitarristas do mundo, Yngwie Malmsteen, deu há alguns anos para a Guitar Player americana. Ele disse:<br/>
<em>&#8220;As pessoas falam que eu sou muito técnico e etc. Mas eu preciso conhecer a técnica para fazer virar música. Assim como um escritor deve conhecer várias palavras para escrever um livro&#8230;&#8221;</em></p>

<p>Pense nisso!<br/>
Devemos conhecer as possibilidades que a linguagem nos dá, e assim ficamos preparados para montar as lógicas que cruzarem nosso caminho.</p>

<p>Grande Abraço!</p>