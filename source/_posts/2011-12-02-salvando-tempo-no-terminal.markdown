---
layout: post
title: "Salvando Tempo No Terminal"
date: 2011-12-02 00:00:00
comments: true
categories: [desenvolvimento, shell]
permalink: ":year/salvando-tempo-no-terminal/"
---

<p>Fala pessoal!</p>

<p>No post anterior (<a href="http://flaviosilveira.com/2011/conhecendo-melhor-seu-interpretador-de-comandos/">conhecendo melhor seu interpretador de comandos</a>) vimos uma prévia sobre o que é Shell e as implementações de Shell, dentro disso a principal de todas elas que é o bash e alguns comandos que podem facilitar a sua vida enquanto trabalha com ele.</p>

<p>Seguindo o comentário do meu super brother Daniel Correa, vamos falar rapidamente aqui sobre um alguns comandos que podes salvar alguns minutos (até horas) de trabalho no terminal.</p>

<p>Quantas vezes você já não precisou daquele comando no terminal que executou há semanas, meses atrás, e não lembra de maneira alguma. O que você faz?? Inevitavelmente fica clicando na tecla da seta para cima por horas até encontrar o seu abençoado comando. Mas você deve saber que essa não é a melhor maneira de resolver isso.</p>

<!--more-->


<p><strong>Buscando comandos digitados no terminal</strong></p>

<p>Com o comando <em>back search</em>, executado através de <em>ctrl + r</em>, você faz uma busca pelos comandos que executou que estão presentes no seu histórico. Você digita algumas letras ou trecho do comando que está buscando e o resultado vai aparecendo para você na linha de comando.</p>

<p>Para usar, basta apertar a tecla <em>enter</em>.<br/>
Para editar o comando, mudar algum parâmetro por exemplo, digite <em>ctrl + j</em> ou <em>esc</em>.<br/>
Para cancelar, <em>ctrl + c</em>ou <em>ctrl + g</em>.</p>

<p><strong>Exigindo um pouco mais do histórico</strong></p>

<p>Você pode explorar mais do histórico de comandos e usar ele a seu favor durante o trabalho.<br/>
Uma das maneiras de se fazer isso é com o comando abaixo:</p>

<pre class="brush: bash; title: ; notranslate" title="">history
</pre>


<p>O comando exibe para você tudo que está presente no seu histórico.<br/>
<img src="../../assets/uploads/2011/12/Captura-de-Tela-2011-12-02-às-5.19.56-AM.png" alt="" title="Bash history" width="342" height="129" class="alignnone size-full wp-image-438" /></p>

<p>Uma maneira rápida de executar novamente esses comandos é pegar a referência deles no histórico, ou seja, pegar esse número que aparece ao lado esquerdo dos comandos (veja imagem acima) e passar ele após um ponto de exclamação, por exemplo:</p>

<pre class="brush: bash; title: ; notranslate" title="">!44
</pre>


<p>Dessa forma, eu irei executar o comando de referência 44 do meu histórico, que no meu caso aqui é um <em>clear</em>.</p>

<p>Seguindo a mesma linha, podemos por exemplo executar o comando digitado a dois comandos atrás, da seguinte forma:</p>

<pre class="brush: bash; title: ; notranslate" title="">!-2
</pre>


<p>Sinta-se à vontade para substituir esse 2 pelo número de vezes que quer voltar no histórico.</p>

<p>Para executar o comando anterior, basta colocar o 1, no lugar do 2 no comando acima, ou ainda substituir o número por uma exclamação (ficando duas exclamações).</p>

<p><strong>O que mais?</strong></p>

<p>Há muito mais a se desvendar e ganhar com o uso do history, como por exemplo: usar palavras chaves para busca, pegar parâmetros de comandos anteriores para um novo comando, entre outros. Aqui tivemos apenas uma pequena prévia das coisas. Mais sobre tudo isso você consegue no próprio manual do history.</p>

<pre class="brush: bash; title: ; notranslate" title="">man history
</pre>


<p>Espero que esse pequeno post ajude você a agilizar um pouco mais de tempo com as coisas no terminal.<br/>
Dúvidas? Sugestões? Estamos aí!<br/>
Grande Abraço!</p>