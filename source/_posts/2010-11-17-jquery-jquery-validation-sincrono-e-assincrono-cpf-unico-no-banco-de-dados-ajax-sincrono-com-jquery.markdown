---
layout: post
title: "JQuery / JQuery Validation / Síncrono E Assíncrono / CPF único No Banco De Dados / Ajax Síncrono Com JQuery"
date: 2010-11-17 00:00:00
comments: true
categories: [desenvolvimento, javascript]
permalink: ":year/jquery-jquery-validation-sincrono-e-assincrono-cpf-unico-no-banco-de-dados-ajax-sincrono-com-jquery/"
---

<p>Salve pessoal.</p>

<p>Hoje trago um artigo pesado e extenso, mas acredito que vá ajudar o pessoal que precisar em várias frentes. Vou Tratar aqui de JQuery, JQuery Validation, a diferença entre síncrono e assíncrono, como fazer ajax síncrono usando JQuery e também soluções para problemas em um dia de trabalho no mundo do desenvolvimento.</p>

<p>Bom, que o JQuery é um dos frameworks mais usados para javascript e que facilita muito a sua vida você já deve saber. E que o plugin para JQuery, JQuery Validation, é uma excelente maneira de validar seus formulários do lado cliente, você também deveria saber.</p>

<p>Veja um exemplo:</p>

<pre class="brush: xml; title: ; notranslate" title="">&lt;script type="text/javascript" src="jquery.js"&gt;&lt;/script&gt;
&lt;script type="text/javascript" src="jquery.validate.js"&gt;&lt;/script&gt;
&lt;script type="text/javascript"&gt;
    
function init()
{
    $("#form").validate({
        rules:
        {
            nome:{required: true},
            senha:{required: true, minlength: 5}
                }
    });
}

$(document).ready(init);
    
&lt;/script&gt;

&lt;/head&gt;
&lt;body&gt;

&lt;form id="form"&gt;
    
    &lt;p&gt;
        &lt;label for="nome"&gt;Nome&lt;/label&gt;
        &lt;input type="text" name="nome" id="nome" /&gt;
    &lt;/p&gt;
    
    &lt;p&gt;
        &lt;label for="senha"&gt;Senha&lt;/label&gt;
        &lt;input type="password" name="senha" id="senha" /&gt;
    &lt;/p&gt;
    
&lt;/form&gt;

&lt;/body&gt;

</pre>




<!--more-->


<p>Com essas poucas linhas você já tem um formulário com campo obrigatório para nome e campo obrigatório para senha exigindo um mínimo 5 caractéres.Ao não seguir qualquer uma das regras, o plugin insere uma Label com uma mensagem de erro.</p>

<p>Você tem opções para personalizar essa mensagem, além de outras várias opções oferecidas pelo plugin.<br/>
Você pode dar uma conferida nessas opções pela <a href="http://bassistance.de/jquery-plugins/jquery-plugin-validation/">documentação e exemplos no site oficial do plugin aqui</a>.</p>

<p><strong>Primeiro Problema</strong></p>

<p>O plugin JQuery Validation é gringo; Internacional se você preferir assim dizer.<br/>
Na sua condição de estrangeiro, ele não conhece o que é CPF.<br/>
Ele não tem um método para entrada e validação de CPF, o que é muito comum nos formulários de cadastro aqui no Brasil.</p>

<p>Por sorte, o JQuery validation tem uma maneira muito fácil de você inserir novos métodos a ele.<br/>
Com uma rápida busca na internet chegamos em vários blogs que nos trazem a solução, como é o caso do <a href="http://www.tidbits.com.br/">TidBits</a> escrito pelo <a href="http://twitter.com/maktuiu">Danilo Augusto</a>, que falou sobre isso em seu post <a href="http://www.tidbits.com.br/colecao-de-metodos-para-o-plugin-validate-do-jquery">Coleção de métodos para o plugin validate do Jquery</a>.</p>

<p>Primeiro vamos adicionar um campo para o CPF.<br/>
Vamos também separar o arquivo .js para ficar mais organizado a coisa toda, separando o que é Html do que é javascript.</p>

<p>Nosso Html vai ficar assim:</p>

<pre class="brush: xml; title: ; notranslate" title="">&lt;script src="jquery.js" type="text/javascript"&gt;&lt;/script&gt;
&lt;script src="jquery.validate.js" type="text/javascript"&gt;&lt;/script&gt;
&lt;!-- default.js será o arquivo separado do javaScript --&gt;
&lt;script src="default.js" type="text/javascript"&gt;&lt;/script&gt;

&lt;form id="form"&gt;
        
    &lt;p&gt;
        &lt;label for="nome"&gt;Nome&lt;/label&gt;
        &lt;input type="text" name="nome" id="nome" /&gt;
    &lt;/p&gt;
    
    &lt;p&gt;
        &lt;label for="senha"&gt;Senha&lt;/label&gt;
        &lt;input type="password" name="senha" id="senha" /&gt;
    &lt;/p&gt;

    &lt;p&gt;
        &lt;label for="cpf"&gt;CPF&lt;/label&gt;
        &lt;input type="text" name="cpf" id="cpf" /&gt;
    &lt;/p&gt;
    
&lt;/form&gt;

</pre>


<p>Ok, adicionamos o Input para o CPF em nosso HTML.<br/>
Agora vamos adicionar o método para o Jquery Validation no nosso arquivo default.js, seguindo o exemplo que pegamos no <a href="http://www.tidbits.com.br/colecao-de-metodos-para-o-plugin-validate-do-jquery">Blog do Danilo</a>.</p>

<pre class="brush: jscript; title: ; notranslate" title="">function init()
{
    $("#form").validate({
        rules:
        {
            nome:{required: true},
            senha:{required: true, minlength: 5}
           }
    });
}

jQuery.validator.addMethod("verificaCPF", function(value, element) {
value = value.replace('.','');
value = value.replace('.','');
cpf = value.replace('-','');
while(cpf.length &lt; 11) cpf = "0"+ cpf;
var expReg = /^0+$|^1+$|^2+$|^3+$|^4+$|^5+$|^6+$|^7+$|^8+$|^9+$/;
var a = [];
var b = new Number;
var c = 11;
for (i=0; i&lt;11; i++){
    a[i] = cpf.charAt(i);
    if (i &lt; 9) b += (a[i] * --c);
}
if ((x = b % 11) &lt; 2) { a[9] = 0 } else { a[9] = 11-x }
b = 0;
c = 11;
for (y=0; y&lt;10; y++) b += (a[y] * c--);
if ((x = b % 11) &lt; 2) { a[10] = 0; } else { a[10] = 11-x; }
if ((cpf.charAt(9) != a[9]) || (cpf.charAt(10) != a[10]) || cpf.match(expReg)) return false;
return true;
}, "Informe um CPF válido.");

$(document).ready(init);

</pre>


<p>Agora falta chamar o método para o seu campo.<br/>
Para isso adicione a seguinte validação no seu código javascript:</p>

<pre class="brush: jscript; title: ; notranslate" title="">$("#form").validate({
    rules:
    {
        nome:{required: true},
        senha:{required: true, minlength: 5},
        cpf:{required: true, verificaCPF: true}
       }
});
</pre>


<p>Repare:<br/>
Chamamos o método verificaCPF, e passamos o valor que queremos, no caso, true para que seja um CPF válido.<br/>
Faça seus testes.</p>

<p><strong>Segundo Problema</strong></p>

<p>Legal! Temos o formulário validando, inclusive com um campo de CPF, sem muito trabalho pois estamos contando com o JQuery Validation. Mas então nos surgi outro problema. No seu banco de dados você tem um campo onde CPF tem de ser único.</p>

<p>E para ajudar seu usuário, além de mostrar se o CPF é válido ou não, você quer mostrar se é um CPF cadastrado ou não.<br/>
E então, como fazemos ?</p>

<p>Para pesquisas no banco de dados sem refresh na página a resposta é fácil não? Ajax!<br/>
Mas como juntar isso no Jquery validation?</p>

<p>Você conhecendo a <a href="http://api.jquery.com/category/ajax/">facilidade do Ajax no Jquery</a>, pode sair logo de cara transformando o seu método de validação de CPF para o seguinte:</p>

<pre class="brush: jscript; title: ; notranslate" title="">jQuery.validator.addMethod("verificaCPF", function(value, element) {
    
value = value.replace('.','');
value = value.replace('.','');
cpf = value.replace('-','');

while(cpf.length &lt; 11) cpf = "0"+ cpf;
var expReg = /^0+$|^1+$|^2+$|^3+$|^4+$|^5+$|^6+$|^7+$|^8+$|^9+$/;
var a = [];
var b = new Number;
var c = 11;

for (i=0; i&lt;11; i++)
{
    a[i] = cpf.charAt(i);
    if (i &lt; 9) b += (a[i] * --c);
}

if ((x = b % 11) &lt; 2) { a[9] = 0 } else { a[9] = 11-x }

b = 0;
c = 11;

for (y=0; y&lt;10; y++) b += (a[y] * c--);

if ((x = b % 11) &lt; 2) { a[10] = 0; } else { a[10] = 11-x; }

if ((cpf.charAt(9) != a[9]) || (cpf.charAt(10) != a[10]) || cpf.match(expReg)) return false;

var verifica = false;
$.get('verificaCpf.php', {cpf : cpf}, function(data){
    if(data == 0) verifica = true;
});

if(!verifica) return false;

return true;
}, "CPF inválido ou já cadastrado!");
</pre>


<p>Vamos ver o que foi feito aqui. Acompanhe da linha 30 em diante.<br/>
Adicionamos uma variável dentro do nosso método chamada <em>&#8220;verifica&#8221;</em>, e definimos o valor de false para ela.</p>

<p>Em seguida fazemos uma chamada para um arquivo PHP através de Ajax.<br/>
Esse arquivo PHP deve fazer uma consulta no seu banco de dados pelo CPF digitado.<br/>
Por ser algo simples de fazer e para não estender ainda mais esse post ,não vou tratar desse código PHP aqui.</p>

<p>Para entendimento, basta saber que nosso código PHP retorna o número de linhas onde encontrou aquele CPF.<br/>
Esse valor vai vir para o javascript pela variável data.<br/>
Repare que é feito uma comparação na resposta do Ajax, que, caso o número de linhas encontradas no banco seja 0, mudamos a variável para true. E fim do Ajax.</p>

<p>Em seguida, verificamos a variável <em>&#8220;verifica&#8221;</em>.<br/>
Se ela for diferente de verdadeira, o método verificaCPF retorna false e será acusado erro em seu formulário.</p>

<p>Ufa! Certo. Vamos testar?<br/>
Problemas acontecem não? Está sempre retornando erro.<br/>
O que está acontecendo?</p>

<p><strong>Terceiro Problema</strong></p>

<p>Vamos entender:<br/>
Seu código PHP é chamado. Ele vai lá no banco de dados, faz a consulta e está retonando o resultado.<br/>
Mas enquanto isso, o código javascript já continuou sua execução, e quando a resposta do ajax chegar, a execução do método terá acabado. Com isso ele vai retornar o valor que tinha na variável, false.</p>

<p>Isso acontece, pois o ajax padrão do JQuery, como foi usado acima, é assíncrono.<br/>
Você está se perguntando o que é isso? Vou tentar ser claro.<br/>
É o fato de não importar quando a resposta do ajax vai vir. Não precisar de sincronismo, compreende?</p>

<p>Porém veja que esse é exatamente o nosso problema aqui. Precisamos desse sincronismo.<br/>
Precisamos da resposta do nosso Ajax antes de continuar a execução do código.</p>

<p>Como fazer?<br/>
Vamos fazer o Ajax Síncrono.<br/>
A execução do javascript só pode continuar depois da resposta do ajax.</p>

<p>Procurando pela internet, achei alguns desenvolvedores falando que não é possível fazer ajax síncrono com JQuery. Isso não é verdade. É uma das primeiras coisas que <a href="http://api.jquery.com/jQuery.ajax/">encontramos na documentação</a>.</p>

<p>Veja como fazer:</p>

<pre class="brush: jscript; title: ; notranslate" title="">jQuery.ajax({
        url: 'verifica_cpf.php?cpf='+cpf,
        async: false,
        success: function(data) {
           if(data == 0) verifica = true; 
       }});
</pre>


<p>Passando o valor false para a propiedade async do ajax, temos nosso ajax síncrono.<br/>
Repare que o código segue o padrão JQuery e é fácil de entender.<br/>
Ao invés de passar as variáveis em uma propiedade, as adicionei no padrão GET diretamente na url.<br/>
Uma opção a isso seria usar a propiedade data.</p>

<p>Substituindo esse trecho de código no lugar do nosso ajax assíncrono anterior, temos nosso problema corrigido.</p>

<p>Uma observação importante, é você reparar que a execução dá página dá uma travada enquanto espera a resposta do javascript. Fique atento para não deixar de dar uma resposta em situações de erro ou sucesso. Caso contrário sua página vai ficar travada nesse ponto.</p>

<p><strong>Quarto problema</strong></p>

<p>Não não…brincadeira… hahaha</p>

<p>Legal! Acredito que chegamos finalmente ao final.<br/>
Dúvidas? Dicas para melhorar todo esse processo? Não deixem de comentar pessoal…<br/>
Grande Abraço!</p>