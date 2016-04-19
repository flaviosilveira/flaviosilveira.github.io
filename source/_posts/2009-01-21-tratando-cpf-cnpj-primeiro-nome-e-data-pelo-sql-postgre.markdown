---
layout: post
title: "Tratando CPF, CNPJ, Primeiro Nome E Data Pelo SQL (Postgre)"
date: 2009-01-21 00:00:00
comments: true
categories: [desenvolvimento, sql]
permalink: ":year/tratando-cpf-cnpj-primeiro-nome-e-data-pelo-sql-postgre/"
---

<p>Olhando para os códigos php no trabalho, como tem sido de costume para averiguar erros e algoritmos que possa melhorar, me deparo em vários controllers com uma série de <a href="http://br.php.net/manual/pt_BR/function.split.php">splits</a> e loops para horas tratar o cpf, horas tratar o cnpj que vem do banco de dados.</p>

<p>No banco de dados estes campos estão salvos em um domínio String, e gravados sem pontuação ou dígitos. Então quando você quer mostrar para o usuário, para não deixar aquele emaranhado de números, você deixa as coisas como ele está acustumado a ver, com os pontos e etc.</p>

<p>Para não ficar repetindo a mesma rotina em vários locais do sistema, nem mesmo criar um método que eu tenha que chamar sempre que quiser um tratamento desses, já trago a coisa toda pronta no retorno da consulta. Simples, confira&#8230;</p>

<p>Trazendo o CPF com a pontuação e o dígito antes dos dois últimos numerais</p>

<pre class="brush: sql; title: ; notranslate" title="">SELECT SUBSTR(cpf, 1, 3) || '.' || SUBSTR(cpf, 4, 3) || '.' ||
SUBSTR(cpf, 7, 3) || '-' || SUBSTR(cpf, 10) AS cpf
FROM e001_pessoas
WHERE pessoaid = 33;
</pre>




<!--more-->


<p> Explicação:</p>

<p>SELECT &#8211; estamos selecionando algo do banco SUBSTR &#8211; é uma função SQL, a mesma do PHP, a mesma do javascript que conhecemos, que serve para trazer parte de uma string.<br/>
Sintaxe &#8211; SUBSTR(campo, á partir de qual caracter começar, o máximo de caracteres a trazer) , sendo esse último opcional.</p>

<p>Então repare começo pegando do campo CPF, a partir do campo 1, 3 caracteres. Em seguida faço uma concatenação, que no SQL é feita com dois pipelines (||). Concateno com um ponto (está entre aspas pois é uma string).<br/>
Depois mais uma vez pego outro pedaço do campo cpf, dessa vez começando do 4° caracter. São mais 3 caracteres e mais uma concatenação com um ponto. Novamente mais um pedaço do cpf , começando do 7° caracter. São mais 3 caracteres e agora um dígito, o famoso <em>tracinho</em>.<br/>
Finalizo essa parte pegando o restante do CPF, que está a partir do caracter 10. Não limitei o número de caracteres nesse último, pois quero todo o restante.</p>

<p>Em seguida faço um ALIAS para o meu resultado, chamando de <em>&#8216;cpf&#8217;</em>. Caso você não o faça o nome do campo retornará como unknow ou com uma interrogação.<br/>
FROM &#8211; para indicar a tabela onde está o campo, que no meu caso é a <em>e001_pessoas</em>.<br/>
WHERE &#8211; para trazer apenas o cpf do registro <em>pessoaid = 33</em>.</p>

<p>Então a coisa toda é muito simples. Tenho meu cpf salvo no banco como um grande número. Pego 3 caracteres dele, concateno com um ponto, mais 3 caracteres, concateno a outro ponto, e assim por diante seguindo o <a href="http://en.wikipedia.org/wiki/File:Cpf2.jpg">modelo do cpf</a>.</p>

<p>Para o CNPJ funciona igual. Basta ver como é dividido o número do CNPJ, e ver quantos dígitos trazer, concatenar a que símbolo e assim por diante. Confira:</p>

<pre class="brush: sql; title: ; notranslate" title="">SELECT SUBSTR(cnpj, 1, 2) || '.' || SUBSTR(cnpj, 3, 3) || '.' ||
SUBSTR(cnpj, 6, 3) || '/' || SUBSTR(cnpj, 9, 4) || '-' ||
SUBSTR(cnpj, 13) AS cnpj
FROM t020_clientes;
</pre>


<p>Acima trouxemos todos os CNPJ&#8217;s da tabela de clientes já com a devida pontuação e a coisa toda.</p>

<p>Uma outra situação é quando queremos mostrar apenas o primeiro nome da pessoa na tela. Novamente falando, você pode tratar isso onde quiser, mas o SQL pode fazer isso para você, então porque deixar isso passar&#8230;</p>

<pre class="brush: sql; title: ; notranslate" title="">SELECT SPLIT_PART(nome, '  ', 1) AS nome
FROM e001_pessoas
WHERE pessoaid = 33;
</pre>


<p>Acima usamos a função do SQL, SPLIT_PART, que se assemelha muito a SPLIT do php e a SPLIT do javascript, dividindo a string em pedaços, de acordo com um separador comum.<br/>
Sintaxe &#8211; SPLIT_PART(campo que queremos dividir, separador entre as partes, parte que eu quero mostrar)</p>

<p>Então na SQL mostrada, a SPLIT_PART, separou o meu campo nome em partes, de acordo com o espaço em branco.<br/>
Exemplo: se o meu campo é &#8216;Maria Francisca Joana&#8217;, a função separou em 3 partes. 1 &#8211; Maria, 2 &#8211; Francisca e 3 &#8211; Joana.<br/>
Nó último parâmetro da função eu passo a parte que eu quero mostrar. No meu caso como quero apenas o primeiro nome, trago só a primeira parte.</p>

<p>Outro caso, esse já bem mais usado, é quando eu tenho um campo de domínio DATE, e quero trazer no resultado da consulta como uma string já com os separadores de dia, mês e ano.<br/>
Digamos que você queira trazer a data no seguinte formato DD/MM/AAAA.</p>

<pre class="brush: sql; title: ; notranslate" title="">SELECT TO_CHAR(dtnascimento, 'DD/MM/YYYY') AS dtnascimento
FROM e001_pessoas
WHERE pessoaid = 33;
</pre>


<p>Usando a função TO_CHAR você consegue isso.<br/>
Sintaxe &#8211; TO_CHAR(campo à transformar, formato que você quer).<br/>
Cuidado ! Repare no Y de Year, e não A de ano.</p>

<p>Experimente outras formatações. Deixem o SQL trabalhar por vocês.</p>

<p>Abraços!<br/>
Valeu !!!</p>