---
layout: post
title: "CodeIgniter ‘metido’ a Ruby on Rails. (ciforms.sh)"
date: 2009-04-16 00:00:00
comments: true
categories: [desenvolvimento, php, shell]
permalink: ":year/codeigniter-metido-a-ruby/"
---

<p>Salve Galera&#8230;</p>

<p>Vocês sabem, muitos projetos em sistemas são similares, sempre aquela mesma coisa&#8230;Listar, Inserir, Editar e Remover.<br/>
Isso me levou a querer criar algo para facilitar tudo isso.</p>

<p>Vendo meu Amigo <a href="http://www.fabiotomio.com" title="Fábio's Blogs">Fábio Tomio</a> mandando ver no <a href="http://www.rubyonrails.pro.br/">Ruby On Rails</a>, ele me mostrou que criava um cadastro (Listar, Inserir, Editar e Remover) muito facilmente, com apenas um comando no terminal, usando a funcão Scaffold se não me engano.</p>

<p>Inspirado nisso, resolvi fazer um Shell Script que geraria todas as views, controller e model prontas com essas opções.</p>

<p><strong>Introdução</strong></p>

<ul>
<li>Chamei de CiForms.</li>
<li>Essa é uma versão de teste. É a versão Zero.</li>
<li>Fiz esse script como estudo. Não tenho pretensões de lucros, suporte, nem nada com ele.</li>
</ul>


<p><strong>Porque não usar o Scaffolding do CodeIgniter</strong></p>

<ul>
<li>O Scaffolding do CodeIgniter não é aproveitável para o desenvolvimento de um projeto, ele não segue o padrão MVC do Framework. Como consta no manual, ele é apenas uma maneira de popular rapidamente uma tabela.</li>
</ul>


<!--more-->


<p><strong>Limitações dessa versão</strong></p>

<ul>
<li>É um shell Script. Vai rodar apenas em base Unix. Fiz testes no Linux distribuição Ubuntu 8.10 e no Leopard MAC OSX 10.5.6. Não vai rodar no Windows.</li>
<li>Por enquanto está rodando apenas em DataBase MySQL, Tive problemas com a função listFields com outros bancos.</li>
<li>Você deve estar com o módulo Rewrite do apache instalado, e usando o .htaccess como indicado no manual do CodeIgniter para fazer suas URL amigáveis, senão a navegação vai ficar super esquisita.</li>
<li>Você deverá chamar o script de dentro da sua pasta Application e as pastas Controllers, Models e Views não podem ter sido renomeadas.</li>
</ul>


<p><strong>Como Usar</strong></p>

<ul>
<li>É bem simples. Basta chamar o script, passando o nome da tabela e em seguida o de sua PK.</li>
<li>O script tem uma opção para ajuda (-h ou &#8211;help) e para verificar a versão (-V ou &#8211;version)</li>
</ul>


<p><strong>Exemplo prático</strong></p>

<p>Baixe o Sheel Script <a href="../../assets/uploads/ciforms.sh" title="Baixe o arquivo">clicando aqui</a>.</p>

<p>É necessário colocar o sheel dentro da pasta applications.<br/>
<img class="alignnone size-full wp-image-83" title="picture-1" src="../../assets/uploads/2009/04/picture-1.png" alt="picture-1" width="541" height="316" /><br style='clear: both;' /></p>

<p>Em seguida Vamos executá-lo no terminal.<br/>
Para chamar o script, apontamos o caminho atual (./) e depois seu nome (ciforms.sh).<br/>
Repare que se não passar os parâmetros corretos ele não irá executar e irá lhe oferecer o help.<br/>
<img class="alignnone size-full wp-image-91" title="picture-8" src="../../assets/uploads/2009/04/picture-8.png" alt="picture-8" width="596" height="83" /><br style='clear: both;' /></p>

<p>Colocando corretamente os parâmetros (Nome da tabela e em seguida a Primary Key da tabela)<br/>
<img class="alignnone size-full wp-image-85" title="picture-3" src="../../assets/uploads/2009/04/picture-3.png" alt="picture-3" width="598" height="76" /><br style='clear: both;' /></p>

<p>O Script é executado e você já pode conferir nas pastas que foram criados os arquivos .php.<br/>
Um controller, um model, e três views.<br/>
<img class="alignnone size-full wp-image-86" title="picture-4" src="../../assets/uploads/2009/04/picture-4.png" alt="picture-4" width="618" height="420" /><br style='clear: both;' /></p>

<p>Basta agora chamar no browser o seu site, em seguida o nome da tabela.<br/>
Aqui está a listagem, onde você tem o Id do registro e os opções para Editar ou Remover.<br/>
<img class="alignnone size-full wp-image-87" title="picture-5" src="../../assets/uploads/2009/04/picture-5.png" alt="picture-5" width="546" height="234" /><br style='clear: both;' /></p>

<p>Após Editar você volta para a listagem.<br/>
<img class="alignnone size-full wp-image-88" title="picture-6" src="../../assets/uploads/2009/04/picture-6.png" alt="picture-6" width="450" height="294" /><br style='clear: both;' /></p>

<p>Após clicar em remover, você repara na listagem com um registro a menos.<br/>
<img class="alignnone size-full wp-image-89" title="picture-7" src="../../assets/uploads/2009/04/picture-7.png" alt="picture-7" width="511" height="195" /><br style='clear: both;' /></p>

<p>Fique a vontade para abrir o código e conferir como são feitas as chamadas e tudo mais. O Shell vai gerar tudo em uma linha só. Se você usa o Eclipse ou o Aptana como editor basta dar um Ctrl+Shift+F para identar tudo automaticamente.</p>

<p>Os Arquivos php não contam com praticamente nenhum comentário, pois tive problemas do Shell em relação a eles.</p>

<p>Devo mexer em breve nele para funcionar com Postgres. Até lá, um abraço a todos.</p>