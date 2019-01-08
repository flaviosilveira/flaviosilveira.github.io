---
layout: post
title: "Microserviços"
date: 2016-11-07 08:00:00
comments: true
categories: [desenvolvimento]
permalink: ":year/microservicos/"
---
Muito anda se falando sobre microserviços e trago para vocês minha experiência de como começamos a trabalhar dessa forma aqui na [LojasKD](https://www.lojaskd.com.br).

Assim como meu post anterior sobre [Ansible e automação](http://flaviosilveira.com/2016/ansible-desperte-a-automacao-em-voce/), esse assunto também faz parte de uma palestra que apresentei durante 2016, um dos meus grandes orgulhos desse ano que encerro com esse post.

###Microserviços - O que é?
Para falar sobre microserviços eu sempre empresto a frase do [@tiagodolphine](https://twitter.com/tiagodolphine): "O menor possível, porém grande o suficiente para representar seu domínio".
<!--more-->
Pequenas aplicações que representem seus domínios. Parece fácil ah?
Mas a linha para que isso se torne um **macroserviço** é tênue. Se você descuidar da organização dos seus serviços eles podem começar a dar mais trabalho do que você gostaria.

###Seus problemas não acabaram
Não existe solução perfeita, tudo tem seu uso ideal, seu lado bom e seu lado ruim.

Microserviços não são uma bala de prata que vai resolver todos os problemas de seus projetos. Assim como você escolhe uma linguagem para desenvolver um projeto, qual banco de dados vai usar e etc, o mesmo deve servir para sua arquitetura.

**Não vá de microserviços simplesmente pelo modismo!**

Aliás, microserviços pode ser comparado ao que acontecia com APIs em SOAP (Simple Object Access Protocol) com seus WSDLs para lá e para cá, que tem seus primeiros registros de uso no fim dos anos 90. Tecnologia tem muito disso, coisas que voltam com nomes diferentes ou um buzz que surge com coisas que já fazemos.

Acompanhem comigo os prós e contras de uma arquitetura monolítica versus uma de microserviços.

###Monolítico
Há não tantos anos atrás, na hora de iniciar nossos projetos era certo que eles seriam de uma forma única. Como estamos falando da KD aqui, vamos pegar o exemplo de ECommerce.

Um banco de dados, uma aplicação MVC em cima de uma linguagem. Um controller para a Vitrine, outro para o Carrinho, outro para o Checkout. Tudo em um lugar só.

Mas então quando seu serviço cai? Tudo cai, tudo fica fora. **-1 aqui para o monolítico**. Mas, na hora de colocar isso em produção? Demais! Tudo em um só lugar, um único deploy. **+1 para o monolítico**.

Se uma das partes do seu sistema ficava lento, grande chance de ele ficar lento por inteiro. E a parte que está deixando lento, que digamos seja lá na visualização de produtos, está impedindo que pessoas fechem suas compras. **-1 para o monolítico**.

Vamos monitorar para que não caia novamente? Vamos ter que monitorar uma única aplicação, Ótimo! **+1 para o monolítico**.

Achar desenvolvedores para um projeto com uma linguagem só é um outro ponto positivo aqui e também o conhecimento em cima de como servir uma única aplicação. **+2 para o monolítico**. Mas a curva de aprendizagem em cima de regras de negócio que estão todas juntas e misturadas podem complicar. **-1 para o monolítico**.

###Os Microserviços
Em microserviços não vamos pensar como uma coisa só, vamos pensar como várias pequenas partes para formar um objetivo comum. Nosso Carrinho, nossa Vitrine, nosso Checkout que estavam todos juntos, aqui se separam em pequenas aplicações cada uma com sua função.

Se um dos nossos serviços caírem, outros serviços continuam funcionando e nosso ECommerce não fica totalmente fora. **+1 para os microserviços**.

Mas fazer deploy de tudo, várias aplicações. E se uma depender de outra em determinada funcionalidade? E se... É, a orquestração de entregas com microserviços pode não ser simples. **-1 para os microserviços**.

Lentidão em um dos serviços? Não deve afetar o restante. **+1 para os microserviços**. Ainda você pode escalar as funcionalidades de uma maneira mais flexível. Exemplo: Você tem muito mais acessos na vitrine do que no carrinho? Coloque mais máquinas para servir sua parte de vitrines, deixe a parte do carrinho com menos máquinas. É uma maneira de otimizar custos usando microserviços.

Agora, monitorar várias aplicações, ter uma arquitetura maior para cuidar. **-1 para os microserviços**.

###Tecnologias Agnósticas
Dei a entender em um dos pontos acima que com microserviços teremos várias linguagens. Isso não é regra, claro! Mas com uma arquitetura em microserviços fica muito mais fácil você experimentar uma nova linguagem para solucionar algum problema. Se não der certo, tudo bem! O Serviço está pequeno o suficiente para você rescrever ele em uma linguagem do seu domínio em pouco tempo.

Coloco isso como dois pontos positivos dos microserviços: Você poder experimentar novas linguagens, poder colocar junto linguagens que não acreditam umas nas outras, descobrir novos conceitos de programação de maneira fácil sem complicar todo um negócio. E a facilidade em reescrever se for necessário. É pequeno, é rápido reescrever. **+2 para os microserviços**.

Mas, na hora de contratar pessoal para mexer com várias linguagens você pode ter um problema. **-1 para os microserviços**.

###Quem ganhou?
Se você está fazendo a matemática dos pontos acima, você está perdendo. Veja o que se aplica melhor para sua necessidade e o que você pode ganhar com cada uma. Novamente, não há melhor ou pior, são soluções distintas.

O que você usaria para provar um conceito de uma ideia para startup? Para um hot site? Um portal de notícias? Um site institucional? Um sistema administrativo?

Recomendo aqui a audição do Episódio #1 do Hipsters ponto tech, [http://hipsters.tech/tecnologias-no-nubank-hipsters-01/](http://hipsters.tech/tecnologias-no-nubank-hipsters-01/) onde o pessoal do NuBank comenta sobre a escolha de microserviços desde o início, e suposições do que poderia ter acontecido se não tivessem ido por esse caminho.

###Comunicação entre microserviços
Várias aplicações, várias linguagens, como uma vai conversar com a outra?

Estamos em 2016 e para comunicar linguagens diferentes hoje temos padrões como REST, JSON que são simples de trabalhar e estão presentes em todo o lugar. Diferente dos antigos e trabalhosos XMLs com WSDLs que infelizmente ainda encontramos por aí.

###Bancos de dados Agnósticos
Muito do que falamos acima para aplicações e linguagens, podem vir de encontro também ao pensar em banco de dados. Porque um banco de dados monolítico? Se ele ficar comprometido pode comprometer todo seu negócio.

Você poder experimentar bancos de dados diferentes em busca de soluções diferentes, performances de cada um e etc. Um banco de dados para produtos, outro banco de dados para pedidos e assim por diante.

Ah, mas como vou tirar relatórios para os meus diretores com várias bases? Como vou unir os dados de uma base com a outra? A resposta aqui pode ser BI. Business Inteligence. Una as informações que sua empresa precisa para seus KPIs e OKRs em um único ponto, onde eles possam montar seus relatórios em uma única ferramenta.

###Na KD
Agora que já comentamos alguns pontos gerais de microserviços e estruturas monolíticas. Segue alguns pontos da nossa experiência com microserviços aqui na LojasKD:

- Os Microserviços chegaram na KD para resolver um problema de software legado. Foi a maneira que encontramos para ir substituindo as funcionalidades de uma grande aplicação monolítica aos poucos, até que não tenhamos mais ela. Estamos nesse rumo.

- Como não tinhamos nenhuma experiência com microserviços, começamos com algo minúsculo. Um serviço que apenas trazia as informações de um pedido quando passado seu ID.

- Começamos a experimentar linguagens e bases de dados diferentes em busca de soluções melhores para problemas conhecidos. 

- Já erramos e tivemos que reescrever microserviços inteiros novamente, mas não levou mais que uma semana.

- Para serviços mais críticos, mantemos em nossa linguagem de maior domínio hoje, PHP.

- Sofremos um pouco com monitoramento. É bastante coisa  para monitorar, disparar alertas e ficar de olho. Custo e trabalho em cima disso são altos.

- A manutenção dos servers não é tão crítica, temos receitas em puppet e dockerfiles que nos ajudam nessa área.

- Os deploys estão automatizados, mas as vezes precisamos fazer uma orquestração verbal para evitar conflitos.

- Nosso time de desenvolvedores trabalham em cima de todos os microserviços e em suas diferentes linguagens. Temos Node, Python, Ruby, Java, GOLang e o já citado PHP. Sofremos um pouquinho na hora de contratar pessoas hoje. Não queremos desenvolvedores que saibam todas essas linguagens, mas o que acontece é que os candidatos acabam assustados com a diversidade. 

-É natural que um desenvolvedor entenda mais de uma linguagem do que de outra e vá guiando o time.

- Não descuide do tamanho dos microserviços. Mantenha uma documentação básica no mínimo.

- Estude sobre API Gateway.

Espero que minha abordagem para explicar microserviços tenha ajudado.
Mas e vocês, como estão usando microserviços? Ou como estão pretendendo usar?
Dúvidas? Outras ideias? Só comentar.
Grande Abraço!