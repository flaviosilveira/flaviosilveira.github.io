---
layout: post
title: "Objective-C: A Linguagem Por Trás Do iOS – Parte 2"
date: 2013-04-13 00:00:00
comments: true
categories: [mobile]
permalink: ":year/objective-c-a-linguagem-por-tras-do-ios-parte-2/"
---

<p>[Este artigo faz parte de uma série de artigos para desenvolvimento IPhone, IPad e iOS.<br/>
<span style="line-height: 1.6em;">Você pode ver os demais artigos da série através da categoria Mobile]</span></p>

<p><span style="line-height: 1.6em;">Nessa parte 2 vamos continuar dando os primeiros passos e criando os primeiros exemplos com a linguagem Objective-C. Como discutido no primeiro artigo, essa linguagem veio evoluindo mas ainda mantém a linguagem C por trás dela, e é com isso que estamos criando nossos primeiros exemplos.</span></p>

<!--more-->


<p><span style="line-height: 1.6em;">[Acompanhe a primeira parte desse artigo em </span><a style="line-height: 1.6em;" href="http://flaviosilveira.com/2013/objective-c-a-linguagem-por-tras-do-ios-parte-1/"><a href="http://flaviosilveira.com/2013/objective-c-a-linguagem-por-tras-do-ios-parte-1/">http://flaviosilveira.com/2013/objective-c-a-linguagem-por-tras-do-ios-parte-1/</a></a><span style="line-height: 1.6em;">]</span></p>

<p><strong style="line-height: 1.6em;">Lição de casa da parte 1<br /> </strong><span style="line-height: 1.6em;">No primeiro artigo deixei uma Lição de Casa que na verdade era uma pegadinha. Imprimir uma variável do tipo Boleana com o printf. Rapidamente o pessoal sacou e colocou nos comentários de que isso não existe. O </span><em style="line-height: 1.6em;">Boolean</em><span style="line-height: 1.6em;"> ou </span><em style="line-height: 1.6em;">Bool</em><span style="line-height: 1.6em;">, aparece em linguagens mais modernas. Para utilizar isso com C, fazemos uma simulação usando por exemplo um inteiro (0 e 1) ou também definindo um tipo qualquer e usando </span><em style="line-height: 1.6em;">enum</em><span style="line-height: 1.6em;">.</span></p>

<p><span style="line-height: 1.6em;">Hoje vamos Criar algumas condicionais e alguns loops.<br /> </span><span style="line-height: 1.6em;">Não tem novidade para quem já programa em outras linguagens, basta checar a sintaxe.<br /> </span><span style="line-height: 1.6em;">Mas caso você não se encaixe nesse grupo, siga o artigo.</span></p>

<p><span style="line-height: 1.6em;">Caso não lembre onde testar o seu código, que arquivo estamos mexendo e etc, consulte a parte 1!</span></p>

<p><strong style="line-height: 1.6em;">IF<br /> </strong><span style="line-height: 1.6em;">O IF não é segredo. Traduzindo do inglês = SE.<br /> </span><span style="line-height: 1.6em;">Se a condição bater, executa o código entre as chaves. Veja o exemplo:<br /> </span></p>

<pre class="brush: cpp; title: ; notranslate" title="">int valor = 5;
if(valor &lt; 10)
{
    printf("Menor que dez!");
}
</pre>


<p>&nbsp;</p>

<p><span style="line-height: 1.6em;">Definimos um variável inteira com valor 5. Se o valor for menor que 10, o printf é executado, caso contrário esse trecho é ignorado. </span><span style="line-height: 1.6em;">Simples não?</span></p>

<p><span style="line-height: 1.6em;">Para fazer comparações com a variável de valor, você pode usar no lugar do menor:<br /> </span><em style="line-height: 1.6em;">> Maior<br /> </em><em style="line-height: 1.6em;">&lt;= Menor ou Igual<br /> </em><em style="line-height: 1.6em;">>= Maior ou Igual<br /> </em><em style="line-height: 1.6em;">== Igual<br /> </em><em style="line-height: 1.6em;">!= Diferente</em></p>

<p><strong style="line-height: 1.6em;">ELSE<br /> </strong><span style="line-height: 1.6em;">Para os casos onde você quer executar algo quando o IF não bater, temos o ELSE. Traduzindo SENÃO.<br /> </span></p>

<pre class="brush: cpp; title: ; notranslate" title="">int valor = 15;
if(valor &lt; 10)
{
    printf("Menor que dez!");
}
else
{
    printf("Maior que dez!");
}
</pre>


<p>&nbsp;</p>

<p><span style="line-height: 1.6em;">Alteramos o valor da variável para 15. Em seguida adicionamos um ELSE.<br /> </span><span style="line-height: 1.6em;">Como valor é Maior que 10, esse trecho é pulado e o que está dentro das chaves do ELSE é executado.</span></p>

<p><strong style="line-height: 1.6em;">Combinando IFs e ELSEs<br /> </strong><span style="line-height: 1.6em;">Você pode combinar o If com o Else quantas vezes quiser, como no seguinte exemplo:<br /> </span></p>

<pre class="brush: cpp; title: ; notranslate" title="">int valor = 7;
if(valor == 7)
{
    printf("Valor Igual 7");
}
else if(valor &lt; 10)
{
    printf("Um numero menor que dez!");
}
else
{
    printf("Um numero maior que dez!");
}
</pre>


<p>&nbsp;</p>

<p><span style="line-height: 1.6em;">Alteramos a variável para 7, o que faz ela cair no primeiro IF. Caso contrário o código iria passando até bater com uma das condicionais. </span><span style="line-height: 1.6em;">Caso não bata com nenhum das condições ela cai no último ELSE. Lembrando que esse ELSE final não é obrigatório.</span></p>

<p><strong style="line-height: 1.6em;">SWITCH<br /> </strong><span style="line-height: 1.6em;">É recomendado evitar o uso de muitas combinações de IF e ELSE, para ficar mais fácil de manter o código ou até para entendimento do mesmo. </span><span style="line-height: 1.6em;">Veja o exemplo:</span></p>

<pre class="brush: cpp; title: ; notranslate" title="">int valor = 16;
    
switch (valor) 
{
    case 7:
        printf("Sete!");
    break;
        
    case 9:
        printf("Nove!");
    break;    
        
    case 16:
        printf("Dezesseis!");
    break;    
        
    case 10:
        printf("Dez!");
    break;    
            
    default:
        printf("Outro!");
    break;
}
</pre>


<p><span style="line-height: 1.6em;">Entramos com o valor a ser analisado dentro do Switch.<br /> </span><span style="line-height: 1.6em;">Então usando o Case, entramos com as condicionais.<br /> </span><span style="line-height: 1.6em;">Caso não bata com nenhuma, temos a opção </span><em style="line-height: 1.6em;">DEFAULT</em><span style="line-height: 1.6em;">.</span></p>

<p><strong style="line-height: 1.6em;">FOR<br /> </strong><span style="line-height: 1.6em;">Quando temos a necessidade de executar uma ação várias vezes ou iterar um valor, surgem para nós os Loops.<br /> </span><span style="line-height: 1.6em;">E o FOR é um dos primeiros que encontramos.<br /> </span></p>

<pre class="brush: cpp; title: ; notranslate" title="">for(int i = 0; i &lt;= 10; i++)
{
    printf("Valor de i: %d", i);
}
</pre>


<p>&nbsp;</p>

<p><span style="line-height: 1.6em;">Para entender o FOR, leia da seguinte maneira. i é igual a 0, enquanto i é menor ou igual que 10, vá aumentando i.</span></p>

<p><span style="line-height: 1.6em;">Esse i++, significa que estamos somando 1 ao valor de i, chamamos isso de incremento. Teremos mais detalhes sobre isso em próximos artigos.</span></p>

<p><span style="line-height: 1.6em;">Está é a maneira mais simples do FOR. Temos outros variações, mais complexas, com mais, com menos parâmetros.<br /> </span><span style="line-height: 1.6em;">Mas se você está começando fique com essa por enquanto.</span></p>

<p><strong style="line-height: 1.6em;">WHILE<br /> </strong><span style="line-height: 1.6em;">While, que traduzindo significa enquanto, é uma outra opção de loop. Veja o exemplo:<br /> </span></p>

<pre class="brush: cpp; title: ; notranslate" title="">int i = 0;
while (i &lt;= 10) 
{
    printf("Valor de i: %d", i);
    i++;
}
</pre>


<p>&nbsp;</p>

<p><span style="line-height: 1.6em;">Seguindo a mesma ideia do FOR, definimos o valor de i, mas dessa vez for da função. Enquanto i for menor igual que 10, o que temos dentro das chaves do while será executado.</span></p>

<p><span style="line-height: 1.6em;">Cuidado! Não esqueça de somar 1 ao valor de i cada vez que passarmos dentro do while.<br /> </span><span style="line-height: 1.6em;">Caso contrário teremos um loop infinito, e isso irá exceder o limite de memória e te causar problemas.</span></p>

<p><span style="line-height: 1.6em;">No exemplo acima, se i fosse por exemplo 15, o </span><em style="line-height: 1.6em;">WHILE</em><span style="line-height: 1.6em;"> não seria executado nenhuma vez.</span></p>

<p>Há situações onde precisamos executar ao menos uma vez o loop, mesmo que o valor não bata. Para essas situações temos o <em>DO WHILE</em>.</p>

<p><strong>DO WHILE<br/>
</strong></p>

<pre class="brush: cpp; title: ; notranslate" title="">int i = 15;
    
do 
{
    printf("Valor de i: %d", i);
    i++;
}
while (i &lt;= 10); 
</pre>


<p>O código é executado uma vez, independente se o valor bate com a condicional ou não.</p>

<p>No exemplo acima, como o valor está setado para 15, ele já não bate com nosso <em>WHILE</em> que pede um número menor igual a 10. Mesmo assim o código é executado uma vez, por conta do <em>DO</em>, traduzindo <em>FAÇA</em>.<span style="line-height: 1.6em;"> </span></p>

<p><strong>Resumindo<br/>
</strong><span style="line-height: 1.6em;">Os exemplos são bem simples e ainda não refletem exemplos muito reais. São exemplos fáceis de entender para que venham no futuro encaixar em problemas que você vai encontrar. </span></p>

<p>Pratique, mude valores das variáveis, faça seus exemplos, crie outras situações.<br/>
Esse é o caminho nesse estágio.</p>

<p>Até o próximo!</p>