---
layout: post
title: "Erro 500, Timeout Apache, Max_execution_time PHP"
date: 2008-12-26 00:00:00
comments: true
permalink: ":year/erro-500-timeout-apache-max_execution_time-php/"
categories: [desenvolvimento, php]
---

<p><strong>Cenário:</strong> Site que funciona como um painel do cliente, onde ele adiciona produtos que necessita para seu negócio. Há uma área onde de um lado é listado os produtos já adicionados, e do outro os que ele ainda pode adicionar.</p>

<p><strong>Ocorrência:</strong> &#8220;Sempre demorou para carregar. Funcionava normal. Mas agora quando um cliente tem muitos produtos, não abre. Dá erro 500.&#8221;<br/>
&#8220;No servidor de testes está funcionando, no do ar não. &#8221;</p>

<p><strong>Pesquisa:</strong> Fui atrás do tal erro 500. Claro já havia o visto antes, mas não sou daqueles que sabe de cor o significado dos erros de servidor e do apache, e nem dos bips de erro da placa mãe. No <a href="http://www.google.com">segundo cérebro</a> há muitas inconstantes sobre o erro 500. Uns dizem ser erro de permissão, outros de configuração. Felizmente meu <a href="http://delicious.com/flaviosilveira">Delicious</a> me salvou. Eu tinha salvo <a href="http://suporte.bs2.com.br/questions/83/P%E1ginas+de+erro+de+servidores+Web.">esse link</a> com uma lista sobre os erros de servidor há algum tempo.</p>

<p>Agora sim. Erro 500: Algo não foi compreendido pelo servidor.<br/>
Certo. Muito bom. Não ajudou muito. Em nada melhor dizendo.<br/>
<strong>E agora?</strong></p>

<!--more-->


<p>Eu e a programadora responsável pelo job, dando uma andada pelo sistema, nos deparamos com uma Consulta SQL cavalar, com várias linhas, Joins e com funções recursivas.</p>

<p><strong>Primeiro chute:</strong> Inspirado pelo nosso supervisor de desenvolvimento, vamos ver o <em>Timeout do apache</em>. Vamos comparar o timeout dos dois servidores. Como fazer isso ?<br/>
No arquivo de configuração do apache (http.conf no Apache ou apache2.conf no Apache2) você deve encontrar uma linha com o seguinte comentário e em seguida a declaração da variável como abaixo.</p>

<pre class="PROGRAMLISTING">#
# Timeout: The number of seconds before receives and sends time out.
#
    Timeout 300</pre>


<p>300 é o default da configuração. E é assim que estava setado nas duas máquinas. Não foi dessa vez.</p>

<p><strong>Segundos passos:</strong> Eu e a Analista de sistemas já estavamos nos preparando para fazer backups dos arquivos do ar e subir os do servidor de teste. Afinal, estava funcionando local, não adiantava ficar rodando o código e dando print() e print_r() pra tudo quanto é lado. O que você faria ?</p>

<p>Mas foi quando um dos técnicos da TI ganhou a tarde. Mudou o <em>max_execution_time</em> no arquivo de configuração do PHP, o php.ini. <strong><br/>
O que é isso ?</strong> O nome diz tudo não ? É o máximo de tempo que o PHP vai tentar ficar executando um script.<br/>
<strong>Onde arrumo isso ?</strong> No php.ini, você vai encontrar as variáveis de Limites de recurso, como abaixo.<br/>
;;;;;;;;;;;;;;;;;;;<br/>
; Resource Limits ;<br/>
;;;;;;;;;;;;;;;;;;;</p>

<p>max_execution_time = 30 ; Maximum execution time of each script, in seconds<br/>
max_input_time = 60 ; Maximum amount of time each script may spend parsing request data<br/>
;max_input_nesting_level = 64 ; Maximum input variable nesting level<br/>
memory_limit = 16M ; Maximum amount of memory a script may consume (16MB)</p>

<p>Repare, aqui na minha configuração está com 30. Esse é o padrão. O Parceiro da TI setou para 60.</p>

<p><strong>Testando: </strong>Olha só, o Cliente que tem mais de 100 produtos agora consegue entrar na sua lista. Apesar da demora. Xiiii&#8230;. mas o cliente com 500 produtos não :(</p>

<p><strong>Solução:</strong> Sim, é isso mesmo. Vamos aumentar mais ainda o <em>max_execution_time</em>.<br/>
<strong>Qual o máximo que podemos setar ? </strong>Segundo dizem, os monges shaolins já ficaram esperando por 8 horas a execução de um script PHP, para exercitar a paciência. Talvez não tenha limite, você pode testar e me dizer.<br/>
<strong>Resolveu ? </strong>Resolveu! Setamos para 300. Apesar da absurda demora (O loading do IE7 se manteve firme por aproximadamente uns 3 a 4 minutos), apareceu a lista de itens do cliente. O cliente não reclama mais que não aparece, apenas da demora.</p>

<p><strong>Próximos passos:</strong> Estudar uma melhor performace para essa SQL. Ela parece ser a grande vilã de tudo. Conseguimos uma solução imediata. Nunca e jamais ideal.<br/>
<strong>Como conseguir essa melhor performance ?</strong> Particularmente não sei. Refazer a consulta sem tantos JOINS ou quebrar em partes podem ser algumas alternativas.</p>

<p>Fica aqui o meu relato de algumas horas de trabalho. Quem sabe surge esse problema por ai né?<br/>
Abraços.</p>