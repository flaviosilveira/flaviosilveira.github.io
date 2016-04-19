---
layout: post
title: "Comparando Arrays E Trazendo Os Valores Diferentes"
date: 2009-09-16 00:00:00
comments: true
categories: [desenvolvimento, php]
permalink: ":year/comparando-arrays-e-trazendo-os-valores-diferentes/"
---

<p>Salve pessoal.</p>

<p>Ontem precisei comparar os resultados de dois arrays e deles trazer os valores que estavam em apenas um dos arrays.</p>

<p>A princípio procurei uma função que fizesse isso pra mim, achei que o <em>array_diff</em> fizesse isso para a gente. Mas me enganei! Não achei uma função com esse resultado.</p>

<p>A função <em>array_diff</em> na verdade traz apenas os valores que constam no primeiro array, mas não constam no segundo.<br/>
Exemplo:</p>

<pre class="brush: php; title: ; notranslate" title="">&lt;?php

$array1 = array("bola", "quadrado", "triangulo");
$array2 = array("esfera", "quadrado", "triangulo");

$result = array_diff($array1, $array2);
print_r($result);

?&gt;
</pre>


<p>O resultado do código acima nos retorna um array com o valor &#8220;bola&#8221;.<br/>
Pois é o único valor que consta no primeiro array e não no segundo.</p>

<!--more-->


<p>O que eu precisava é que ele me retornasse também os valores que tinham no segundo array e que não constavam no primeiro.</p>

<p>Resolvi da seguinte forma:</p>

<pre class="brush: php; title: ; notranslate" title="">&lt;?php

$array1 = array("bola", "quadrado", "triangulo");
$array2 = array("esfera", "quadrado", "triangulo");

$result1 = array_diff($array1, $array2);
$result2 = array_diff($array2, $array1);

$full = array_merge($result1, $result2);

print_r($full);

?&gt;
</pre>


<p>Primeiro fazemos retornar os valores que estão no primeiro array e não no segundo ($result1).<br/>
Em seguida os que estão no segundo array e não no primeiro ($result2).<br/>
Após isso unimos os dois arrays através da função <em>array_merge</em>.</p>

<p>E o resultado retornado é [0] => bola [1] => esfera, como esperado.<br/>
Bola que está apenas no primeiro array, e esfera que está apenas no segundo.<br/>
Os demais valores aparecem em ambos os arrays, logo, ficam de fora.</p>

<p>Adicionem outros elementos aos arrays para testar e confiram os resultados.</p>

<p>Grande Abraço.</p>