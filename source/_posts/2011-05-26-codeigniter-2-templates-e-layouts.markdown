---
layout: post
title: "Codeigniter 2 – Templates E Layouts"
date: 2011-05-26 00:00:00
comments: true
categories: [desenvolvimento, php]
permalink: ":year/codeigniter-2-templates-e-layouts/"
---

<p>Fala pessoal!</p>

<p>O que mais gera acessos aqui no Blog são os artigos sobre Codeigniter, e principalmente a parte de layouts. É o artigo <em>Habilitando Layouts no CodeIgniter (Template Engine)</em> que está dividido em <a href="http://flaviosilveira.com/2010/habilitando-layouts-no-codeigniter-template-engine-1/">parte 1</a> e <a href="http://flaviosilveira.com/2010/habilitando-layouts-no-codeigniter-template-engine-2/">parte 2</a>.</p>

<p>Como esse artigo tem mais de um ano, resolvi dar um upgrade nele com algumas observações.</p>

<!--more-->


<p>Desde que ele foi escrito temos algumas novidades. A principal dela é  o lançamento de uma versão crítica do Codeigniter. Mas não se preocupe, a mecânica do artigo continua funcionando.<br/>
Apenas atente para alguns detalhes.</p>

<p>Preste atenção para a parte do seu controller:</p>

<ul>
<li>Agora ele extende da classe CI_Controller e não mais da classe Controller.</li>
<li>Agora você não tem de ter mais um método construtor com o mesmo nome da classe. Pode arrancar fora aquilo sem medo.</li>
</ul>


<p>Outros:</p>

<ul>
<li>No tutorial anterior há uma correção porque eu tratava minha pasta system diferente do convencional. Com a ajuda e os comentários de vocês, foi feita uma correção que está no final do post. Agora na versão 2 está tudo ok. A pasta system vem separada da pasta application.</li>
<li>Na versão 2 temos agora arquivos .htaccess, arquivos de configuração, dentro das pastas application e da pasta system. Dentro deles há uma regra para recusar qualquer coisa que tentar acessar a pasta. Certifique-se que, em caso de colocar seus arquivos de estilo, ou seus arquivos javascript dentro de application por exemplo, alterar essa regra no .htaccess.</li>
</ul>


<p>Então você pode seguir normalmente o tutorial, apenas adapte os detalhes citados acima.<br/>
Está com dificuldades ou preguiça? <a href="../../assets/uploads/2011/05/ci2exemplo1.zip">Clique aqui para baixar um exemplo com Layouts em cima do Codeigniter 2</a>.</p>

<p>É isso galera. Abraço!!</p>