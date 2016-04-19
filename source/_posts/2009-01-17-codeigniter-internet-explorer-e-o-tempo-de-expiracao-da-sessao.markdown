---
layout: post
title: "CodeIgniter, Internet Explorer E O Tempo De Expiração Da Sessão"
date: 2009-01-17 00:00:00
comments: true
permalink: ":year/codeigniter-internet-explorer-e-o-tempo-de-expiracao-da-sessao/"
categories: [desenvolvimento, php]
---

<p>Nesta Quinta-feira antes de sair do trabalho me deparo com uma surpresa no novo sistema que estou trabalhando. O login de acesso havia parado de funcionar no Internet Explorer. No Firefox tudo normal. Chata mania de ficar testando só no Firefox por conta das facilidades como Firebug e WebDeveloper, ai quando vamos testar no browser do usuário acontece essas coisas.</p>

<p>Sexta pela manhã, foi minha primeira tarefa do dia. Achei que seria algo bobo. Realmente era, mas levei 4 horas para descobrir.</p>

<p>Comecei pelos arquivos de JavaScript vendo se estava tudo ok.<br/>
Os retornos via ajax do banco estavam ok.<br/>
Parti para os controllers que gravam a sessão no browser.<br/>
Comentei a biblioteca que faz verificação da sessão para deixar eu acessar livremente a aplicação. Dei um print no valor da sessão, que pelo codeIgniter se verifica assim:</p>

<pre class="brush: php; title: ; notranslate" title="">//Não esqueça de chamar o helper session
// Login é o valor que eu estava gravando na sessão
print($this-&gt;session-&gt;userdata('login'));

// A tradicional global session não funcionará no codeIgniter
print($_SESSION['login']);
</pre>


<p>No Firefox tudo ok. No Internet Explorer em branco. Que beleza, o Internet Explorer não está deixando escrever na sessão&#8230;</p>

<!--more-->


<p>Navegando pelo <a href="http://www.google.com">segundo cérebro</a> não tive nenhuma resposta conclusiva. As soluções propostas não se encaixavam para mim. Atualizar versão do apache, tirar Underlines da url, tirar números do nome do servidor, nada disso fez sentido pra mim.</p>

<p>Sem idéias, me juntei ao meu amigo <a href="http://www.ronieneubauer.com">Ronie</a> e ao Rafael que também faz parte da minha equipe nesse projeto para caçar uma solução.</p>

<p>Tiramos o redirecionamento do Login, para manter na mesma página. E demos ali também um print, dessa vez em todos os valores da sessão</p>

<pre class="brush: php; title: ; notranslate" title="">//Print_r por se tratar de array
print_r($this-&gt;session-&gt;userdata);
</pre>


<p>Os valores estavam ali, o problema estava no redirecionamento então.</p>

<p>Quebramos a cabeça demais, e como antes estava funcionando no IE, resolvemos rever tudo de brusco que mudamos no sistema.<br/>
Verificamos rotas, Jquery e seus plugins, Verificações de nível de acesso, nada.<br/>
Até que me lembrei que havia mudado a configuração da sessão, para expirar em meia hora (1800 segundos) tirando do padrão de duas horas (7200 segundos) que vem no CodeIgniter. Esses valores são alterados no config.php, ali você dá de encontro com outras configurações para sua sessão, como nome dela e etc.</p>

<p>E, Sim, era isso. Voltamos ao default do codeIgniter e tudo voltou a funcionar. Me lembro de ter tido uns problemas similares trabalhando com PHP sem frameworks, mas nem suspeitava. Fomos testando para ver o mínimo que o IE iria aceitar de tempo de expiração. Chegamos no valor de 3835 segundos. Mesmo assim continuou muita instável, e setamos em 4000 segundos.</p>

<p>Problema resolvido após 4 horas de Prints, Alerts, Pesquisa, Palpites e Indignação&#8230;</p>

<p>Valeu..<br/>
Abraços !!!</p>