---
layout: post
title: "Limitando O SELECT Do SQL Em Diferentes Bancos De Dados"
date: 2009-02-27 00:00:00
comments: true
categories: [desenvolvimento, sql]
permalink: ":year/limitando-o-select-do-sql-em-diferentes-bancos-de-dados/"
---

<p>Olá pessoal&#8230;</p>

<p>Atualmente tenho tido o privilégio de trabalhar com vários data bases, e com isso está dando para ver as diferenças de sintaxe, performance, ferramentas e demais coisas de um para outro.</p>

<p>Tenho trabalhado com Microsoft SQL, Postgres e Oracle.</p>

<p>Uma coisa que me chamou a atenção foi a maneira de limitar a consulta em cada um deles. Tenho feito bastante consultas limitadas pois ainda estou conhecendo a base de dados da empresa e não sei ao certo quantos registros tem certas tabelas. Para evitar que a coisa caia ou trave, faço consultas limitadas.</p>

<p>Repare as diferenças de um banco para outro abaixo:</p>

<pre class="brush: sql; title: ; notranslate" title="">SELECT * FROM tabela LIMIT 20
</pre>




<!--more-->


<p>Essa é a sintaxe para o postgres, que acho que deve ser a mais conhecida por ser software livre e etc.<br/>
Basta adicionar o parâmetro LIMIT e passar o valor de máximo de registros que você quer.</p>

<pre class="brush: sql; title: ; notranslate" title="">SELECT TOP 20 * FROM tabela
</pre>


<p>Essa é a maneira como o Microsoft limita sua consulta.<br/>
Você adiciona o parâmetro TOP passando o valor do máximo de registros que você quer. Isso deve vir logo após o SELECT.</p>

<pre class="brush: sql; title: ; notranslate" title="">SELECT * FROM tabela WHERE ROWNUM &lt; 20
</pre>


<p>E por último o Oracle.<br/>
Você deve usar o parâmetro ROWNUM junto a um operador (&lt;, >, &lt;=, >=, =) e em seguida o valor máximo de registros que você quer para sua consulta.<br/>
Traduzindo este exemplo acima ficaria mais ou menos assim:<br/>
<em>Selecione tudo da tabela chamada &#8216;tabela&#8217; onde o número de tuplas seja menor que 20</em></p>

<p>Por hoje é isso ai rapaziada. Valeu !</p>