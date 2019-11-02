---
layout: post
title: "Entenda como funciona o PHP! (Do código fonte até a renderização)"
permalink: ":year/entenda-como-funciona-o-php-do-codigo-fonte-ate-a-renderizacao"
date: 2019-02-27 00:00:00
comments: true
categories: [desenvolvimento]
---

Esse artigo é quase uma tradução fiel do artigo [How PHP Executes from Source Code to Render](https://www.sitepoint.com/how-php-executes-from-source-code-to-render) de [Thomas Punt](https://twitter.com/tpunt94), revisado por [Younes Rafie](https://twitter.com/rafieyounes).

No original o autor coloca os pedaços de códigos para você testar por conta. Aqui, além disso, adicionei como rodar os mesmos com um único comando, usando docker. Assim você não precisa de muito esforço para ver os exemplos. 

Criei uma imagem no dockerhub com tudo necessário para rodar os exemplos desse artigo. Basta ter o docker instalado e rodar os comandos como mostrados.

Acaba não sendo uma tradução fiel, pois tomei a liberdade de adicionar e tirar algumas partes de texto em relação ao original. E por ter muitos termos técnicos, posso ter pisado na bola ao traduzir ou manter no inglês algum termo em específico. Fiz isso para tentar deixar mais didático do meu ponto de vista. E isso não foi tão simples. Então, não deixe de comentar caso veja algo errado / estranho...

<!-- more -->

## 4 etapas

Bastante coisa acontece quando você executa um pequeno trecho de código PHP. De maneira geral podemos dizer que o Interpretador do PHP passa por 4 etapas quando o código é executado:

* Tokenização (Ou Lexing ou Scanning)
* Parsing
* Compilação
* Interpretação

Abaixo vamos passar por cada um dessas etapas e ver como podemos checar a saída de cada um deles para entender o que realmente acontece. Para isso vamos usar algumas extensões que já vem com PHP nativamente (como Tokenizer e o OPCache) e outras que não (como php-ast e o VLD). 


## Tokenização

Também chamada de Lexing ou de Scanning por alguns outros autores.

Essa etapa faz um processo de pegar um texto (um código PHP nesse caso) e transformar ele em uma sequência de tokens. Um token é simplesmente um identificador, e esse identificador vai indicar um valor. 

O PHP usa o [re2c](http://re2c.org/) para gerar esses tokens a partir do arquivo de configuração [zend_language_scanner.l](https://github.com/php/php-src/blob/master/Zend/zend_language_scanner.l).

Vamos ver a saída dessa etapa usando a extensão [Tokenizer](http://php.net/manual/en/book.tokenizer.php), nativa no PHP.

```
$code = <<<'code'
<?php
$a = 1;
code;

$tokens = token_get_all($code);

foreach ($tokens as $token) {
    if (is_array($token)) {
        echo "Line {$token[2]}: ", token_name($token[0]), " ('{$token[1]}')", PHP_EOL;
    } else {
        var_dump($token);
    }
}
```

Salve o código acima em um arquivo (por exemplo, tokenizer.php), em seguida rode o container para executar ele.

`docker run --rm -v "$PWD":/myapp -w /myapp flaviosilveira/php-source-to-render php tokenizer.php`

Explicando rapidamente o comando docker acima:

- **--rm** para remover o container automaticamente.
- **-v "$PWD":/myapp** para compartilhar seu diretório atual com o diretório 'myapp' do container.
- **-w /myapp** é uma opção para indicar o local de trabalho para o php, workspace, o document root.
- **flaviosilveira/php-source-to-render** é a imagem para construir o container.

Saída:

```
Line 1: T_OPEN_TAG ('<?php
')
Line 2: T_VARIABLE ('$a')
Line 2: T_WHITESPACE (' ')
string(1) "="
Line 2: T_WHITESPACE (' ')
Line 2: T_LNUMBER ('1')
string(1) ";"
```

Coisas para considerarmos da saída acima: 

- Nem todos os pedaços do código se transformam em Tokens. Alguns símbolos já são considerados tokens por si só (=, ;, :, ?, e outros). 
- Será armazenado o valor correspondente do token e o número da linha desse token para o stack trace. Aquele mesmo que vemos em algumas mensagens de erro tentando nos ajudar quando temos problemas.

## Parsing

Essa etapa de parsing, pega a saÃ­da da etapa de tokenização e executa duas tarefas:

A primeira tarefa: Valida a ordem dos tokens com as regras da linguagem definidas no [BNF grammar file](https://github.com/php/php-src/blob/master/Zend/zend_language_parser.y). Isso garante que as regras de sintaxe da linguagem estão sendo seguidas. Essa etapa conta com o [Bison](https://www.gnu.org/software/bison/) (Não é Street Fighter, é Open Source) e usa o contexto **LARL**, Look Ahead, Left to right, ou seja, faz a leitura em frente, enquanto achar tokens, da esquerda para a direita.

A segunda tarefa: Gerar uma árvore de sintaxe abstrata, no inglês AST (Abstract Sintaxe Tree), uma árvore do código fonte que será usada durante a próxima etapa.

Podemos ver a forma dessa AST produzida pelo parser usando a extensão [php-ast](https://github.com/nikic/php-ast) do excelente [Nikita Popov](https://github.com/nikic).

```
$code = <<<'code'
<?php
$a = 1;
code;

print_r(ast\parse_code($code, 60));
```

##### Importante
O número 60 dentro do print_r acima, se refere a versão. 60 é a versão no momento de escrita dese artigo (Na versão original em inglês era 30). Caso dê erro, a saída do mesmo te mostrará a versão atual. Basta trocar.

Salve o código acima em um arquivo (por exemplo, parsing.php), em seguida rode o container para executar ele:

`docker run --rm -v "$PWD":/myapp -w /myapp flaviosilveira/php-source-to-render php parsing.php`

Saída:

```
ast\Node Object (
    [kind] => 132
    [flags] => 0
    [lineno] => 1
    [children] => Array (
        [0] => ast\Node Object (
            [kind] => 517
            [flags] => 0
            [lineno] => 2
            [children] => Array (
                [var] => ast\Node Object (
                    [kind] => 256
                    [flags] => 0
                    [lineno] => 2
                    [children] => Array (
                        [name] => a
                    )
                )
                [expr] => 1
            )
        )
    )
)
```

A árvore de nós, que geralmente são do tipo **ast\Node**, tem várias propriedades:

- kind - Um valor inteiro para representar o tipo de nó. Cada um tem uma constante correspondente (AST_STMT_LIST => 132, AST_ASSIGN => 517, AST_VAR => 256).
- flags - Um inteiro que específico comportamento de sobrecarga. Por exemplo, um nó ast\AST_BINARY_OP terá flags para diferenciar qual operação binária está ocorrendo.
- lineno - O número da linha, como visto na informação do token anteriormente.
- children - Sub-Nós. Por exemplo uma função vai apresentar como children: parâmetros, tipo do retorno, corpo, etc.

Essa saída AST dessa etapa é útil para ferramentas como analisadores de código, por exemplo o [Phan](https://github.com/phan/phan).

## Compilação

A etapa de compilação consome a AST gerada acima. Gerando Opcodes (Operation Codes) recursivamente enquanto percorre a árvore. Opcodes são operações a serem executadas.

Essa etapa também executa algumas otimizações. Isso inclui resolver algumas chamadas de função com argumentos literais (strlen("abc") para int(3)) e expressões matemáticas (60 * 60 * 24 para int(86400)).

Há algumas maneiras de vermos os Opcodes gerados nessa etapa. Mas hoje vamos de [VLD](https://derickrethans.nl/projects.html#vld), criada pelo [Derick Rethans](https://twitter.com/derickr). Essa ferramenta mostra a saída de uma maneira mais amigável do que as demais, e isso ajuda no nosso entendimento.

Vamos ver a saída para o seguinte código:

```
if (PHP_VERSION == '7.2.15') {
    echo 'Yay', PHP_EOL;
}
```

Salve o código acima em um arquivo (por exemplo, compilation.php), em seguida rode o container para executar ele:

`docker run --rm -v "$PWD":/myapp -w /myapp flaviosilveira/php-source-to-render php -dvld.active=1 compilation.php`

Saída:

```
line     #* E I O op                           fetch          ext  return  operands
-------------------------------------------------------------------------------------
   3     0  E > > JMPZ                                                     <true>, ->3
   4     1    >   ECHO                                                     'Yay'
         2        ECHO                                                     '%0A'
   6     3    > > RETURN                                                   1
```

De certa forma os Opcodes se parecem com o código fonte original, permitindo acompanhar as operações básicas. (Esse artigo não tem a pretensão de detalhar Opcodes.) Nenhuma otimização foi aplicada no nível do código de operação no script acima, mas podemos ver que essa etapa de compilação resolveu por exemplo a condição (1 == '1') para true.

Nessa etapa também, entram em ação ferramentas que fazem o cache dos Opcodes, evitando assim refazer as etapas de tokenização, parsing e compilação com frequência. Entre essas ferramentas temos o apc e o OPCache.

O OPCache, além de fazer isso também tem alguns passos de otimização. Alterando o parâmetro dopcache.optimization_level, podemos aumentar o nível de otimização e ver o que acontece:

##### Importante
Precisamos também habilitar o OPCache para cli, com o parâmetro dopcache.enable_cli para vermos a saída.

`docker run --rm -v "$PWD":/myapp -w /myapp flaviosilveira/php-source-to-render php -dopcache.enable_cli=1 -dopcache.optimization_level=1111 -dvld.active=1 -dvld.execute=0 code/compilation.php`

Saída:

```
line     #* E I O op                           fetch          ext  return  operands
-------------------------------------------------------------------------------------
   4     0  E >   ECHO                                                     'Yay%0A'
   6     1      > RETURN                                                   1
```

Vemos que a condicional foi removida e as duas instruções com ECHO se tornaram uma só. Isso é só um gostinho das otimizações que o OPCache aplica. Esse artigo não vai entrar nos detalhes dos níveis de otimização por ser um assunto extenso.

##### Importante
Você pode adicionar os parâmetros -dvld.save_paths e -dvld.save_dir para salvar essa saída com os Opcodes em um arquivo que você poderá abrir com o [Graphiz](http://graphviz.org/). Fica muito legal para estudar!


## Interpretação

A útima etapa é a interpretação dos Opcodes. Aqui os Opcodes são executados na VM Zend Engine (ZE). Não há muito o que dizer sobre essa etapa (ao menos de um ponto de vista de alto nível). A saída é praticamente igual a saída de seus códigos usando comandos como echo, print, var_dump e etc.


Então, ao invés de entrar em algo muito complexo nessa etapa, aqui está um fato divertido: o PHP chama a si mesmo como uma dependência quando gera sua própria VM. Isso porque a VM é gerada por um script PHP, para ser mais simples de escrever e mais fácil de manter.


## Conclusão

Demos aqui uma rápida olhada pelas 4 etapas que o interpretador do PHP passa quando executa um código. Isso envolveu o uso de algumas extensões como Tokenizer, OPCache, php-ast e VLD para manipular e ver a saída de cada etapa.

Que esse artigo ajude a espalhar um melhor entendimento sobre o interpretador do PHP, e também que mostre a importância do estágio de cache na etapa de compilação.

Abraço!