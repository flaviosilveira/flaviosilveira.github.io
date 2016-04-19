---
layout: post
title: "Objective-C: A Linguagem Por Trás Do iOS – Parte 1"
date: 2013-02-21 00:00:00
comments: true
categories: [mobile]
permalink: ":year/objective-c-a-linguagem-por-tras-do-ios-parte-1/"
---

<p>Fala pessoal!</p>

<p>Este é segundo artigo, que faz parte da série sobre desenvolvimento para iOS que estou fazendo. Se você perdeu o primeiro post siga esse link <a href="http://flaviosilveira.com/2013/comece-a-programar-para-ios/">http://flaviosilveira.com/2013/comece-a-programar-para-ios/</a> para acompanhar nossos passos desde o início.<span style="line-height: 1.6em;"> </span></p>

<p>Em nosso primeiro post criamos um projeto simples e entendemos a sua estrutura de pastas. Partindo desse ponto, vamos hoje conhecer um pouco da linguagem que vamos usar para desenvolver para iOS. É! XCode não é só arrastar e soltar, tem que codificar. E para isso usamos a linguagem Objective-C.</p>

<!--more-->


<p><strong>Rápida História</strong></p>

<p>Você deve achar que o Objective-C não é tão antigo, já que não faz tanto tempo que temos pessoas com IPhones desfilando por aí não é mesmo? Mas não, o Objective-C está na área desde o início dos anos 80 e foi idealizado e criado pelo PHD em Matemática biológica Brad Cox e pelo (também) PHD em Ciência cognitiva Tom Love.</p>

<p>Como com esses títulos eles caíram na programação eu não sei, mas outros detalhes da história deles, de como eles estavam preocupados com a falta de reutilização de código em cima do Smaltalk dentro da ITT e de como eles começaram a criação de um processador em C para resolver esses problemas, você pode encontrar dando aquela rápida pesquisada no Google. Se você está com seu listening de inglês em dia você pode conferir o próprio Tom Love falando sobre o assunto nesse vídeo no Youtube <a href="http://youtu.be/adI6-liGXqE">http://youtu.be/adI6-liGXqE</a> (Há outros vídeos e keynotes de Tom que você pode encontrar no youtube).</p>

<p>No vídeo, Love também comenta sobre como o Objective-C sobreviveu através dos anos até ele ser popularizado pela NeXT, empresa de Steve Jobs. A NeXT extendeu o GCC para compilar Objective-C e também criou as primeiras ferramentas de desenvolvimento para ele que vão evoluindo até chegar no XCode que temos em mãos hoje.</p>

<p>E aproveitando que comentei sobre o XCode, vale dizer que visto que o Objective-C é uma linguagem que já vem de algum tempo, você encontra vários compiladores para ela de modo que consiga estudar ela em separado. Mas como aqui vamos focar em IPhones, IPads e em ambiente Apple, nada melhor que o XCode na hora de te ajudar a desenvolver para esses fins.<span style="line-height: 1.6em;"> </span></p>

<p><strong>C</strong></p>

<p>Tom Love comenta que apesar de tudo que eles desenvolveram, o C continua lá sem nenhuma alteração. E é verdade. Os tipos prímarios de dados em cima de Objective-C são exatamente os mesmos que no C puro. Para experimentar isso abra em seu projeto o arquivo <em>ViewController.m</em> e procure pelo método <em>viewDidLoad</em> (view carregada), dentro dele você pode experimentar alguns tipos de dados no melhor estilo C.</p>

<p>Os principais tipos de dados em C são <em>char</em>, <em>int</em>, <em>float</em>, <em>double</em> e <em>bool</em>. Para definir eles usamos a seguinte sintaxe:</p>

<pre class="brush: cpp; title: ; notranslate" title="">tipo nome_da_variavel;
tipo nome_da_segunda_variavel = valor_da_variavel;
</pre>


<p>Repare que no primeiro exemplo de sintaxe apenas iniciamos a variável, sem nenhum valor inicial. Já no segundo exemplo, aproveitamos e já definimos um valor para ela. Vejamos alguns exemplos abaixo:</p>

<pre class="brush: cpp; title: ; notranslate" title="">// Char
char caracter;
char letra = 'a';
char nome[7] = 'Flavio;

// Int
int idade;
int ano = 2013;

// Float
float peso = 81.30;

// Double
// que tal você pesquisar a diferença do float para o double?
double pi = 3.1415926535;

// Bool --de booleano
bool aceite = TRUE;
</pre>


<p>Certo, certo. Estamos aqui definindo variáveis. Mas que coisa sem graça. Vamos colocar um pouquinho mais de diversão nisso?</p>

<p><span style="line-height: 1.6em;">No XCode vamos abrir nosso console e exibir nossas animadas variáveis. Para exibir o console você pode ir até o menu </span><em style="line-height: 1.6em;">View >> Debug Area >> Active Console</em><span style="line-height: 1.6em;"> ou em </span><em style="line-height: 1.6em;">View >> Debug Area >> Show Debug Area. </em><span style="line-height: 1.6em;">Outra opção é clicar em um pequeno botão no rodapé do XCode que contém uma seta apontando para cima como mostra a figura abaixo:<br /> <a href="../../assets/uploads/2013/02/Imagem-1.png"><img class="alignnone size-full wp-image-617" title="Imagem 1" src="../../assets/uploads/2013/02/Imagem-1.png" alt="" width="174" height="52" /></a></p></p>

<p>
  </span>
</p>




<p>
  Seu console deve parecer como na imagem abaixo:<br /> <a href="../../assets/uploads/2013/02/Imagem-2.png"><img class="alignnone size-large wp-image-618" title="Imagem 2" src="../../assets/uploads/2013/02/Imagem-2-1024x102.png" alt="" width="655" height="65" /></a>
</p>




<p>
  Console ativado, é hora de exibir as variáveis. Qual a função que exibi variávies no C? A mais conhecida que você já deve ter visto por aí é o printf. Fazendo um teste com o array de char que definimos acima temos o seguinte código:
</p>




<pre class="brush: cpp; title: ; notranslate" title="">

- (void)viewDidLoad
{
[super viewDidLoad];

// Do any additional setup after loading the view, typically from a nib.

// Char
char nome[7] = "Flavio";

printf("Nome: %s", nome);
}
</pre>




<p>
  </span><span style="line-height: 1.6em;">Compile o seu projeto para ver a variavel sair no output. (Caso não lembre como compilar o projeto, dê uma olhada no final do primeiro post da série </span><a style="line-height: 1.6em;" href="http://flaviosilveira.com/2013/comece-a-programar-para-ios/">http://flaviosilveira.com/2013/comece-a-programar-para-ios/</a><span style="line-height: 1.6em;"> ).<br /> </span>
</p>




<p>
  Repare bem na sintaxe do printf. No primeiro parâmetro da função colocamos a string mais um identificador <em>%s</em>. Esse identificador será substituído pelo segundo parâmetro da função, no caso aqui nossa variável nome. Esse <em>s</em> em nosso identificador é um indicador para o tipo da nossa variável, no caso aqui String. Para imprimir um inteiro utilize o identificador <em>%d</em>, onde <em>d</em> se refere a decimal:
</p>




<pre class="brush: cpp; title: ; notranslate" title="">
- (void)viewDidLoad
{
[super viewDidLoad];
// Do any additional setup after loading the view, typically from a nib.

// Char
int ano = 2013;

printf("Ano: %d", ano);
}
</pre>




<p>
  </span><span style="line-height: 1.6em;">Sim, sim. É verdade que </span><em style="line-height: 1.6em;">%i</em><span style="line-height: 1.6em;"> tambem funciona para inteiros, mas em materiais por aí é mais comum ver o </span><em style="line-height: 1.6em;">%d</em><span style="line-height: 1.6em;">.</span>
</p>




<p>
  Continue seus testes com floats e doubles. Use o Identificador <em>%f </em>para esses dois tipos. Se quiser formatar seu numero utilize %.3f, onde 3 é o numero de casas decimais que você quer. <em>%lf </em>ou <em>%g</em> também servem para esses tipos.
</p>




<p>
  <strong>Lição de casa</strong>
</p>




<p>
  O que? Quer só ler o artigo com os códigos prontos e sair mandando ver? Aqui não! Para aprender tem que ir começando a se virar sozinho certo?
</p>




<p>
  A primeira lição que deixo é a de imprimir uma variável do tipo boleana usando o printf. Fácil não? Só dar aquela googada aí ou pegar aquela Barsa da estante.
</p>




<p>
  Para aqueles que já tem uma noções de lógica, que tal experimentar alguns IFS, ELSES, WHILE, CASE, DO…WHILE, FOR ??
</p>




<p>
  Para os demais, é isso que veremos no próximo post.
</p>




<p>
  Grande Abraço!
</p>