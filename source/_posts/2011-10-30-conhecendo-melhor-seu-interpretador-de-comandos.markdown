---
layout: post
title: "Conhecendo Melhor Seu Interpretador De Comandos"
date: 2011-10-30 00:00:00
comments: true
categories: [desenvolvimento, shell]
permalink: ":year/conhecendo-melhor-seu-interpretador-de-comandos/"
---

<p>Se você é usuário de sistemas operacionais baseados em unix, deve estar acostumado a abrir o terminal para tarefas simples como mover e copiar arquivos, remover arquivos em massa, criar pastas, verificar diretórios, etc. Se você conhece um pouco mais e administra sites por exemplo, deve mover seus arquivos com scp, usar conexões ssh e fazer todo seu trabalho via terminal.</p>

<p>Quem faz essa ligação entre você e o coração do sistema operacional, permitindo executar esses comandos, é o Shell. Quem interpreta e processa os comandos para você, é uma implementação do Shell, que é o que vamos conhecer melhor aqui hoje.</p>

<p>Este termo Shell, deve ter feito você lembrar sobre Shell Script, que escutamos falar muito e nada mais é do que um script com vários comandos Shell dentro dele.</p>

<p>Dentre as implementações de Shell, aquilo que interpreta seus comandos, a mais famosa hoje é o Bash (Bourne-again shell, fazendo uma referência ao Bourne Shell que você pode pesquisar sobre). Para conferir qual o interpretador padrão de seus comandos, em seu terminal digite o seguinte comando</p>

<!--more-->

<pre class="brush: bash; title: ; notranslate" title="">echo $SHELL
</pre>


<p>Se seu interpretador for o Bash, como a maioria, você vai ver a saída <em>/bin/bash</em>.</p>

<p>Entre outras implementações de Shell podemos ter <em>csh</em>, <em>tcsh</em>, <em>sh</em>, <em>ksh</em>, e várias outras. Para conferir se essas implementações estão instaladas no seu sistema operacional, basta digitar o nome delas. Por exemplo:</p>

<pre class="brush: bash; title: ; notranslate" title="">bash
</pre>


<p>Caso esteja instalada, o terminal irá permitir que execute comandos naquela implementação, caso contrário apontará como comando inexistente. Você também consegue uma listagem das implementações shell disponíveis em seu sistema operacional abrindo o arquivo shells, geralmente localizado em <em>/etc/shells</em>.</p>

<p>Acredito que se você usar outras implementações apenas por algum tempo, vai achar todas muito parecidas pois uma deriva ou usa a outra, e assim nem vai notar diferença entre elas.</p>

<p><strong>Usando o Bash</strong></p>

<p>O bash traz alguns atalhos que podem facilitar a sua vida, sendo um dos principais a tecla <em>TAB</em> (ou <em>ctrl + i</em>) para completar comandos, nomes de arquivos ou nomes de variáveis.</p>

<p>Para buscar por comandos que você tenha digitado anteriormente use <em>ctrl + r</em>.<br/>
Para anular a busca use <em>ctrl + c</em>, que também é usado para abortar outros comandos, scripts e as vezes loops infinitos.</p>

<p><em>ctrl + a</em> para ir ao início da linha do comando (também obtido com a tecla <em>home</em>, se houver), <em>ctrl + e</em> para ir ao final dela (equivalente a tecla <em>end</em>).<br/>
Perdeu a tecla <em>enter</em> ou cansou dela? Use <em>ctrl + j</em></p>

<p>Esses atalhos tendem a funcionar melhor quando se está definido o padrão de teclas <em>Emacs</em>, embora grande maioria deles funcione em outros padrões.</p>

<p>Você pode mudar esse padrão com o comando</p>

<pre class="brush: bash; title: ; notranslate" title="">set -o emacs
</pre>


<p>Você poderia usar o padrão <em>VI</em>, da seguinte maneira</p>

<pre class="brush: bash; title: ; notranslate" title="">set -o vi
</pre>


<p>Como exemplo para essa situação, temos os atalhos <em>ctrl + p</em> (equivalente a seta para cima) e <em>ctrl + n</em> (equivalente a seta para baixo) para trazer os últimos comandos executados. Eles funcionam apenas no padrão <em>emacs</em>.</p>

<p><strong>Preciso saber esses comandos?</strong></p>

<p>Muito provavelmente um marginal não vai encostar uma arma na sua cabeça lhe cobrando esses comandos no meio da rua. Mas talvez algum dia na sua carreira, você vai entrar em algum Data Center, e ter de mexer diretamente em uma máquina que estiver dentro de um hack enorme.</p>

<p>Você irá puxar uma pequena gaveta, que irá se tornar um monitor e um simples teclado. Esse teclado pode conter apenas teclas básicas, excluindo assim as suas tão usadas setas para navegar entre os caracteres e palavras, e as vezes até sem a tecla enter. Esteja preparado conhecendo alguns desses comandos. Lembre-se que o google pode não estar por perto.</p>

<p>Em breve trarei para vocês uma alternativa bem legal para o Bash, e como ela pode ajudar na produtividade de pessoas que trabalham diretamente com o terminal.</p>

<p>Até lá!</p>