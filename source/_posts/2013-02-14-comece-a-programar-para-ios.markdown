---
layout: post
title: "Comece a Programar Para iOS"
date: 2013-02-14 00:00:00
comments: true
categories: [mobile]
permalink: ":year/comece-a-programar-para-ios/"
---

<p><strong style="line-height: 1.6em;">Sem blá blá blá</strong></p>

<p><span style="line-height: 1.6em;">Sem muito blá blá blá, quero hoje começar uma pequena série sobre desenvolvimento para iOS. </span><span style="line-height: 1.6em;">Quero ajudar quem deseja conhecer a tecnologia sem a enrolação que vejo em outros materiais sobre o assunto. </span><span style="line-height: 1.6em;">Paralelo a isso também consigo me manter estudando o assunto e evoluindo junto com quem acompanha os artigos.</span><span style="line-height: 1.6em;"> </span></p>

<p>Vou pular toda aquela parte que você já deve ter lido por aí sobre precisar de um Mac, que há outras maneiras de você conseguir instalar o sistema da Apple em um PC Intel comum, que vamos usar o XCode porque ele facilita nossa vida, instalação do XCode, as camadas de desenvolvimento do iOS, etc, etc. Mas é claro, caso venha a necessidade podemos segurar e detalhar um pouco mais o que surgir.</p>

<!--more-->


<p><strong>Criando seu primeiro projeto no XCode</strong></p>

<p>Vamos começar com tudo, direto para a prática. Para isso abra o XCode e crie um novo projeto. <span style="line-height: 1.6em;">Vamos criar um projeto do tipo Single view Application, ele já vai nos trazer uma tela inicial e um controller para trabalharmos. </span><span style="line-height: 1.6em;">Na janela seguinte dê um nome qualquer para seu projeto e no último passo selecione uma pasta para ele.<br /> </span><span style="line-height: 1.6em;">Acompanhe pelas imagens abaixo:</span></p>

<p><a href="../../assets/uploads/2013/02/imagem1.png"><img class="alignnone size-medium wp-image-604" title="imagem1" src="../../assets/uploads/2013/02/imagem1-300x200.png" alt="" width="300" height="200" /></a>                 <a style="line-height: 1.6em;" href="../../assets/uploads/2013/02/imagem2.png"><img class="alignnone size-medium wp-image-606" title="imagem2" src="../../assets/uploads/2013/02/imagem2-300x234.png" alt="" width="300" height="234" /></a>            <a style="line-height: 1.6em;" href="../../assets/uploads/2013/02/imagem3.png"><img class="alignnone size-medium wp-image-605" title="imagem3" src="../../assets/uploads/2013/02/imagem3-286x300.png" alt="" width="286" height="300" /></a><span style="line-height: 1.6em;">Repare que não mudamos nada do que já veio selecionado. Estamos usando tudo como já vem configurado.</span><span style="line-height: 1.6em;"> </span></p>

<p>Dê uma atenção especial no segundo passo, na opção Devices, onde ficou selecionado <em>Universal</em>, o que significa que estamos desenvolvendo tanto para IPhone quanto para IPad. Teríamos a opção nesse passo de selecionar ou um ou outro se quisessémos.</p>

<p><strong><br/>
Estrutura do seu projeto</strong></p>

<p>Certo, vamos dar uma analisada no que o XCode criou para a gente aqui.<br/>
<span style="line-height: 1.6em;">No canto esquerdo superior temos o painel project navigator como na imagem abaixo.<br /> </span><span style="line-height: 1.6em;">Se por qualquer motivo você não estiver visualizando ele, basta ir em <em>View >> Navigators >> Show Project Navigator</em>.</span></p>

<p><span style="line-height: 1.6em;"><a href="../../assets/uploads/2013/02/imagem-4.png"><img class="alignnone size-full wp-image-607" title="imagem 4" src="../../assets/uploads/2013/02/imagem-4.png" alt="" width="257" height="241" /></a> </span></p>

<p>Vamos ver primeiro a pasta que leva o nome do seu projeto.<br/>
<span style="line-height: 1.6em;">Repare que vamos ter extensões de arquivo .h e .m.<br /> </span><span style="line-height: 1.6em;">Nos arquivos .h temos assinaturas e características e no .m vamos ter as implementações dos métodos. (Se você não entendeu muito bem isso agora não se preocupe, mas lembre-se disso).</span><span style="line-height: 1.6em;"> </span></p>

<p>O AppDelegate recebe notificações do sistema operacional iOS.<br/>
<span style="line-height: 1.6em;">Informações como se seu aplicativo terminou de carregar ou se o usuário fechar seu aplicativo caem nesse arquivo.</span><span style="line-height: 1.6em;"> </span></p>

<p>O StoryBoard, é a interface gráfica do seu aplicativo.<br/>
<span style="line-height: 1.6em;">Lembra da opção </span><em style="line-height: 1.6em;">Universal</em><span style="line-height: 1.6em;"> quando criamos o projeto?<br /> </span><span style="line-height: 1.6em;">Por termos optado por </span><em style="line-height: 1.6em;">universal</em><span style="line-height: 1.6em;"> o XCode preparou para a gente um storyBoard para IPhone e outro para IPad.</span></p>

<p>No ViewController é onde entraremos com código para fazer as interações com nossa interface gráfica.<br/>
<span style="line-height: 1.6em;">Na Pasta Support Files temos alguns arquivos gerais do seu aplicativo, com ícones, imagens e também arquivos com informações do app.</span><span style="line-height: 1.6em;"> </span></p>

<p>Em seguida você vê a pasta para os testes, dentro dela arquivos que devem ser usados para os testes unitários.<span style="line-height: 1.6em;"> </span></p>

<p>A pasta frameworks serve para armazenar todas as bibliotecas usadas no seu projeto. Você pode expandir ela e reparar que o XCode já adicionou algumas bibliotecas para a gente usar aqui.</p>

<p>E finalmente a pasta products, que vai conter nosso produto final.<br/>
<span style="line-height: 1.6em;">Se você pretende colocar seu aplicativo na Apple Store, é daqui que as coisas vão sair.</span><span style="line-height: 1.6em;"> </span></p>

<p><strong><br/>
Compilando seu projeto</strong></p>

<p>É hora de colocar o seu projeto em ação. Para isso vamos compilar ele.</p>

<p><span style="line-height: 1.6em;">Antes de tudo você deve escolher em qual tipo de device quer ver seu aplicativo.<br /> </span><span style="line-height: 1.6em;">No canto superior esquerdo do XCode você pode selecionar entre o simulador do IPad (que vem por padrão selecionado) ou o simulador do IPhone, como mostrado na imagem.</span></p>

<p><a href="../../assets/uploads/2013/02/imagem5.png"><img class="alignnone size-medium wp-image-608" title="imagem5" src="../../assets/uploads/2013/02/imagem5-300x57.png" alt="" width="300" height="57" /></a><span style="line-height: 1.6em;"> </span></p>

<p>Feito isso, clique no botão Run, o primeiro botão no canto esquerdo do XCode, ou pressione <em>CMD + R</em>. <span style="line-height: 1.6em;">O resultado deve ser como da imagem abaixo.<br /> <a href="../../assets/uploads/2013/02/imagem6.png"><img class="alignnone size-medium wp-image-611" title="imagem6" src="../../assets/uploads/2013/02/imagem6-151x300.png" alt="" width="151" height="300" /></a> </span></p>

<p>Como não escrevemos nenhum código e ainda não colocamos nada em nosso storyboard, temos essa tela em branco.<br/>
<span style="line-height: 1.6em;">Vamos descobrir como mudar isso no próximo post.</span><span style="line-height: 1.6em;"> </span></p>

<p>Abraço!</p>