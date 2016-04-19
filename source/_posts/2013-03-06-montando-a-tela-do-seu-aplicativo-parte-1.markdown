---
layout: post
title: "Montando a Tela Do Seu Aplicativo – Parte 1"
date: 2013-03-06 00:00:00
comments: true
categories: [mobile]
permalink: ":year/montando-a-tela-do-seu-aplicativo-parte-1/"
---

<p><span style="line-height: 1.6em;">[Este artigo faz parte de uma série de artigos para desenvolvimento IPhone, IPad e iOS. Você pode ver os demais artigos da série através da categoria Mobile]</span></p>

<p>No artigo de hoje vamos conhecer alguns objetos para nos ajudar a criar a tela de nossos aplicativos para iOS. Para conhecer eles vamos usar o projeto que criamos nos artigos anteriores. É um projeto simples do tipo <em>Single View Application</em>, que ainda não tem nada demais, já que estamos apenas conhecendo algumas coisas. Então nada impede que você crie outro projeto do tipo <em>Single View Application</em>.</p>

<!--more-->


<p><strong>Interface Builder</strong></p>

<p>Como explicado no primeiro artigo, temos na estrutura que o XCode cria para nós arquivos do tipo StoryBoard. Como criamos nosso projeto com a opção <em>Universal</em> temos um StoryBoard para IPhone e outro para IPad, como mostra a imagem abaixo.<br/>
<span style="line-height: 1.6em;"><img class="size-full wp-image-633 alignleft" title="Estrutura do projeto" src="../../assets/uploads/2013/03/Imagem-1.png" alt="" width="296" height="115" /><br style="clear: both;" /></span><span style="line-height: 1.6em;">Ao clicar em um desses arquivos você visualiza o Interface Builder.</span></p>

<p>Vejamos por exemplo o arquivo <em>MainStoryboard_IPhone.storyboard</em>:<br/>
<span style="line-height: 1.6em;"><img class="alignnone size-large wp-image-634" title="Imagem 2" src="../../assets/uploads/2013/03/Imagem-2-1024x606.png" alt="" width="655" height="387" /></span><span style="line-height: 1.6em;">Uma pequena curiosidade aqui. As atuais versões do XCode trazem o Interface Builder acoplado ao XCode, tudo na mesma ferramenta. Em versões anteriores você tinha uma aplicação separada para isso, assim como o IPhone Simulator por exemplo. </span></p>

<p><span style="line-height: 1.6em;">Descrevendo rapidamente as janelas da imagem temos:</span></p>

<p>No canto esquerdo superior a Document Outline onde está aparecendo nossa<em>View Controller Scene</em>. É onde irá conter todos os elementos e objetos da nossa cena, da nossa tela.<br/>
<img class="size-full wp-image-631 alignleft" title="Imagem3" src="../../assets/uploads/2013/03/Imagem3.png" alt="" width="268" height="159" /><br style="clear: both;" /><br style="clear: both;" /></p>

<p>No canto direito superior é onde irão aparecer os utilitários. Nesses utilitários poderemos alterar tamanhos, identificadores, conexões com funções entre outros. Você pode navegar entre os botões para encontrar essas opções.<br/>
<img class="size-full wp-image-632 alignleft" title="Imagem4" src="../../assets/uploads/2013/03/Imagem4.png" alt="" width="241" height="198" /><br style="clear: both;" /><br style="clear: both;" /></p>

<p>Logo abaixo temos nossa Library de objetos, que é onde estão os objetos que vamos usar para montar nossas telas.<br/>
<span style="line-height: 1.6em;"><img class="size-full wp-image-629 alignleft" title="Imagem 5" src="../../assets/uploads/2013/03/Imagem-5.png" alt="" width="257" height="247" /><br style="clear: both;" /></span><span style="line-height: 1.6em;">Repare que temos uma caixa de busca logo no rodapé. Ela vai nos ajudar a encontrar mais rápido o que queremos sem que precisar ficar rolando e rolando com o mouse em busca de algo. Caso você navegue pelos botões que aparecem em cima, você irá para outras libraries que aparecem no XCode, mas não vamos usar nenhuma delas tão cedo então não se preocupe agora.</span></p>

<p>Resumindo então:</p>

<ul>
<li><span style="line-height: 1.6em;">Document outline: Mostra os objetos da nossa cena</span></li>
<li><span style="line-height: 1.6em;">Utilitários: Onde vamos alterar propiedades, características, identificadores, alinhamentos, etc…</span></li>
<li><span style="line-height: 1.6em;">Library de objects: Onde os objetos estão.</span></li>
</ul>


<div>
  <p>
    <strong>Primeiros Objetos</strong>
  </p>
  
  <p>
    <span style="line-height: 1.6em;">Vamos agora conhecer 4 objetos básicos para montar nossas telas: Um botão, label, campo texto e um slider.<br /> </span><span style="line-height: 1.6em;">Esses são os objetos que mais devem surgir em seus projetos, mas claro que isso pode variar de projeto para projeto.</span><span style="line-height: 1.6em;"> </span>
  </p>
  
  <p>
    <strong>Botão</strong>
  </p>
  
  <p>
    <span style="line-height: 1.6em;">No campo de busca da library de objetos digite </span><em style="line-height: 1.6em;">Round Rec Button</em><span style="line-height: 1.6em;">. Ao começar a digitar você já vai ver o objeto surgir para você. Clique em cima dele e arraste para a sua tela. Posicione como preferir.</span>
  </p>
  
  <p>
    Você pode trabalhar o alinhamento, largura e altura diretamente com o objeto, mas se preferir pode fazer isso também pelas janelas de utilitários. O mesmo para alterar o label do botão, você pode dar um duplo clique em cima dele ou alterar pelos utilitários. Experimente essas e algumas outras opções na janela de utilitários chamada <em>Attributes Inspector</em>.
  </p>
  
  <p>
    <strong>Label</strong>
  </p>
  
  <p>
    Devolta ao campo de busca da library de objetos, dessa vez vamos buscar por label. A label é uma simples etiqueta, um texto para nos indicar alguma coisa. Da mesma maneira que o botão você pode alterar algumas de suas características diretamente sobre o elemento, ou fazer isso pelas janelas utilitárias.  Tente por exemplo alterar a cor da fonte para vermelho.
  </p>
  
  <p>
    Repare que ao mover diretamente os objetos pelo nosso protótipo de tela, algumas linhas quase que como réguas aparecem para te ajudar no alinhamento dos seus objetos. Use disso para manter tudo alinhado e bem distribuído.
  </p>
  
  <p>
    <strong>Campo de texto</strong>
  </p>
  
  <p>
    Para adicionar um campo de texto vamos devolta ao campo de busca da library de objetos, e digite Text Field. Nesse objeto o usuário poderá entrar com um texto. É aquele famoso objeto que quando ativo exibe um teclado na tela. Logo, além de todas as opções dos objetos anteriores, como cor da fonte, alinhamento, tamanho, você pode selecionar qual o tipo de teclado que o usuário irá ter disponível.
  </p>
  
  <p>
    Outra opção ainda é setar um placeholder no campo de texto e tentar com isso economizar um label para explicar do que se trata aquele campo.
  </p>
  
  <p>
    <strong>Slider</strong>
  </p>
  
  <p>
    Um slider pode servir como marcador de alguma coisa, um projeto onde por exemplo o usuário deve entrar sua altura ou seu peso pode ser melhor apresentado com um slide. Na caixa de busca da library procure por <em>slider</em>.
  </p>
  
  <p>
    Um detalhe é que o slider não traz um indicador de em que ponto ele está, como por exemplo 50% ou 100%. Então uma boa ideia é colocar junto do Slide uma Label para indicar esse valor.
  </p>
  
  <p>
    <strong>Exercício</strong>
  </p>
  
  <p>
    Com o objetos que aprendemos acima, você deve ser capaz de montar uma tela como essa:<br /> <img class="alignnone size-medium wp-image-630" title="Imagem6" src="../../assets/uploads/2013/03/Imagem6-152x300.png" alt="" width="152" height="300" />
  </p>
  
  <p>
    <strong>Difícil? Vou te ajudar</strong>
  </p>
  
  <p>
    Esses são os 4 objetos que temos para hoje. Achou complicado de entender? Não te culpo já que é um tema totalmente visual. Por isso estou anexando a esse artigo o vídeo abaixo que segue os passos executados no texto. Com a leitura e o visual da coisa você deve entender tudo sem problemas.<br />
  </p>
  
  <p>
    <br style="clear: both;" />Mas, caso ainda tenha dúvidas é só mandar. Grande Abraço!
  </p>

  <iframe src="https://player.vimeo.com/video/61175405" width="640" height="360" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>
<p><a href="https://vimeo.com/61175405">Montando a tela do seu aplicativo - Parte 1</a> from <a href="https://vimeo.com/user9814221">Fl&aacute;vio Silveira</a> on <a href="https://vimeo.com">Vimeo</a>.</p>