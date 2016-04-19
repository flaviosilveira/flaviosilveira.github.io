---
layout: post
title: "Função Para Contar Palavras (Padrão De Caracteres) Em Uma String Microsoft SQL Server"
date: 2009-11-06 00:00:00
comments: true
categories: [desenvolvimento, sql]
permalink: ":year/funcao-para-contar-palavras-padrao-de-caracteres-em-uma-string-microsoft-sql-server/"
---

<p>Salve galera!</p>

<p>Precisei durante essa semana de uma função que contasse quantas vezes uma palavra aparecia dentro de uma String no SQL Server. Achei que já tivesse algo pelo menos similar, mais após andar pelo MSDN e pelo Books Online vi que o jeito seria fazer uma função.</p>

<p>A lógica é a seguinte:</p>

<ul>
<li>Recebo via Parâmetro a Palavra que quero buscar e a String toda ou texto.</li>
<li>Faço um loop baseado no tamanho do texto.</li>
<li>Pego o tamanho da palavra que está sendo procurada e a cada caracter do texto, andamos o tamanho da palavra e comparamos se isso é igual a palavra procurada.</li>
<li>Se for, soma um no contador de palavras e continua.</li>
</ul>


<p>Agora como fica o código disso? Repare abaixo:</p>

<!--more-->




<pre class="brush: sql; title: ; notranslate" title="">CREATE FUNCTION CountSearchPat
(
      @Word Varchar(100),
      @String Varchar(Max)
)
RETURNS int
AS
BEGIN
 
      -- Declaração Variáveis
      Declare @Count int, @CountWord int
 
      -- Contador de quantas vezes apareceu a palavra
      Set @CountWord = 0
 
      -- Contador do Loop
      Set @Count = 0
 
      -- Loop
      While @Count &lt;= Len(@String)
      Begin
 
            -- Se encontrar a palavra soma mais um para @CountWord
            Set @CountWord =
                  Case When Substring(@String, @Count, Len(@Word)) = @Word
                        Then @CountWord + 1
                        Else @CountWord
                  End
 
            -- Soma mais um ao contador
            Set @Count = @Count + 1
 
      End
 
      -- Retorna Valor
      Return @CountWord
 
END
</pre>


<p>Repare no loop da linha 30 que tem seu contador baseado no tamanho da String inteira, para percorrer cada caracter.</p>

<p>Na linha 24 temos uma variável que seu valor depende do CASE onde, se a partir daquele caracter for encontrada a palavra, soma mais um, senão continua com o mesmo valor.</p>

<p>Na linha 31 temos a soma do contador do loop. E então o retorno do valor da função.</p>

<p>Agora é só testar.<br/>
Por Exemplo: Select dbo.SearchStringPat(&#8216;teste&#8217;, &#8216;aatestehstestehjkteste&#8217;)<br/>
O resultado será 3.</p>

<p>Agora reflita comigo no próximo Exemplo sugerido pelo meu Brother Hernando Santana:<br/>
Você tem uma String da seguinte maneira &#8216;AAAAA&#8217; e procura pelo padrão &#8216;AA&#8217;. Qual valor irá retornar ?</p>

<p>A função criada aqui irá retornar 4. A resposta é uma questão de conceito. Eu ando caracter por caracter atrás da palavra. Podemos fazer andar a partir da palavra encontrada adicionando mais algumas variáveis sem problema e fazendo retornar o valor 2. Para minha necessidade não fazia diferença a princípio.</p>

<p>Idéia simples que resolveu os problemas do dia.<br/>
Até a Próxima! Abraços!</p>