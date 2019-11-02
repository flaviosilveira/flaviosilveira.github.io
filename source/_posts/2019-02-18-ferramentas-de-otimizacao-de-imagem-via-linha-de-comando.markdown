---
layout: post
title: 'Ferramentas de otimização de imagem via linha de comdo'
permalink: ':year/ferramentas-de-otimizacao-de-imagem-via-linha-de-comando'
date: 2019-02-18 00:00:00
comments: true
categories: [desenvolvimento]
---
Na última semana durante um trabalho de otimização de performance para um site, chegou a hora das imagens. Muitas imagens antigas de produtos e também peças de layout que tinham bom espaço para ganho. Diminuir o tamanho dos arquivos sem perder tanto as cores e a qualidade gráfica das imagens.

Eu estava procurando por ferramentas para otimizar as imagens de uma maneira que eu pudesse fazer diretamente no servidor, via terminal. Dessa forma eu não precisaria fazer o download de tudo para minha máquina, depois subir novamente e nem nada similar. Apenas um Backup no próprio servidor e rodar os comandos.
<!--more-->
Haviam imagens das famílias PNG, GIF e JPG e acabei chegando nas seguintes ferramentas:

* jpegoptim
* optiPNG
* gifsicle

Todas as três instaladas via apt-get e similares, super leves, fácéis de instalar e também de usar, como mostro a seguir:

### jpegoptim

Uso simples:

``jpegoptim filename.jpg``

Seu arquivo pode ser jpg, jpeg, JPG, JPEG, ...

O comando acima, faz a otimização mantendo a qualidade da imagem, o que queremos. Mas você pode também passar um parâmetro para controlar isso.

Tive excelentes resultados sem muita perda de qualidade e com excelentes ganhos de compressão com o seguinte comando:

``jpegoptim --max=80 filename.jpg``

### optiPNG

Uso simples:

``optipng filename.png``

Seu arquivo pode ser png, PNG, etc.

Diferente da ferramenta anterior para jpg, essa não permite parâmetros considerando perda de qualidade por conta do formato PNG e como ele foi concebido.

### gifsicle

Uso simples:

``gifsicle --batch --optimize=3 filename.gif``

**--batch** é o parâmetro para dizer que você quer manter o arquivo no mesmo lugar e com o mesmo nome.

**--optimize** é um parâmtro que determina o nível de otimização. 3 é uma opção que tenta vários métodos em cima da imagem. Consulte o manual parr
a as outras opções.

Seu arquivo pode ser gif, GIF, ..

Em caso de gifs animados, dê uma lida no manual. Existem alguns parâmetros adicionais para otimização de animações.

### Várias imagens de uma vez só

Para rodar os comandos acima em várias imagens, dentro de vários diretórios, use a opção **-exec** do comando **find**

``find -name '*.png' -exec optipng {} \;``

**-name** para buscar por nome dos arquivos

**.png** irá buscar por arquivos com a extensão .png. Não esqueça das aspas.

Após o **-exec** adicione o comando que você quer executar para todas as ocorrências que serão encontradas.

**{}** As chaves representam as ocorrências encontradas.

Feche com **\;**

Antes de sair executando essa combinação, teste com um *ls -l* no lugar do comando. Assim você verá o que o **find** vai retornar. E claro, faço um backup das imagens em outra pasta para evitar maiores problemas.

### man

Todas as ferramentas acima possuem um manual bem completo e fácil de compreender. Basta digitar **man** e o nome da ferramenta para acessar.

Grande Abraço!
