---
layout: post
title: "Ansible - Desperte a automação em você"
date: 2016-10-17 00:00:00
comments: true
categories: [desenvolvimento]
permalink: ":year/ansible-desperte-a-automacao-em-voce/"
---
{% raw %}
Automação vem se tornando um tema essencial em empresas que querem crescer com mais cérebro e menos braço. Aquela tarefa que você repete mais de duas vezes já deve ser pensada em uma maneira de ser automática, concorda?

No universo do desenvolvimento, quantas são as tarefas que repetimos quando se trata de máquinas? Deploys, extração de logs, instalação e configuração de ferramentas, etc. Ansible pode ser a ferramenta que vai te ajudar a automatizar tudo isso.
<!--more-->
Durante esse ano de 2016 apresentei a palestra ***Automações com Ansible*** onde o objetivo principal foi uma iniciação ao Ansible. Como usar ele de maneira bem básica e se iniciar na automação. Estrutura de um projeto básico, como criar as primeiras tarefas, passar argumentos, variáveis, e usar includes. Essa vai ser a agenda desse longo post técnico e assim também encerrando as apresentações dessa palestra para dar lugar a outras :-).


####Ansible
Ansible ([https://www.ansible.com/](https://www.ansible.com/)) é uma ferramenta Open Source em Python para automatizar ações em máquinas. Ela é super simples, e esse é sempre um dos meus lemas quando se trata de desenvolvimento e tecnologia. Se está difícil, tem alguma coisa errada. Pare e analise. Tecnologia não é mágica, tem que fazer sentido.

Não vou falar da instalação do Ansible. É fácil você fazer download dele e sair rodando ou ainda usar **yum install** ou **apt-get install**.


####Um projeto básico
Há várias maneiras de estruturar um projeto ansible. Algumas sugestão com arquiteturas de pastas super elaboradas, onde podem fazer sentido para algumas soluções. Para agora, para começarmos, dois arquivos vão resolver nosso problema.

	- projeto.yml
	- hosts

Um arquivo com extensão .yml (yet another markup language) e um arquivo hosts, sem extensão.
No arquivo yml você vai colocar o passo a passo da sua automação. Tecnicamente ele tem o nome de playbook. No arquivo hosts vamos apontar as máquinas onde as tarefas serão executadas.


####Arquivo hosts
Vamos primeiro configurar as máquinas que serão afetadas pelas nossas tarefas.
	
	#This is the Host File.
	
	[projeto]
	192.168.5.6 ansible_ssh_user=user ansible_ssh_pass=pass
	
É isso que vocês precisam no arquivo hosts quando falamos de acesso que o ansible vai fazer usando ssh. O IP da máquina, seguido de um usuário e senha. Esse nome em colchetes vai te ajudar a gerenciar as coisas em um futuro, mantenha ele ali.

Vai fazer uso de portas? Acesso a máquinas com chave? Chamar mais de uma máquina?

	#This is the Host File.
	
	###################
	# Projeto servers #
	###################
	[projeto-homologacao]
	222.222.222.222:2123 ansible_ssh_private_key_file=/.ssh/chave.pem ansible_ssh_pass=pass
	123.123.123.123:2123 ansible_ssh_private_key_file=/.ssh/chave.pem ansible_ssh_pass=pass
	
	[projeto-local]
	192.168.5.6 ansible_ssh_user=user ansible_ssh_pass=pass
	
Para acessar as máquinas usando chaves use **ansible_ssh_private_key_file**. Se seu acesso tem portas diferentes, basta adicionar elas ao final do IP.

Notem que fiz uma separação entre as máquinas de homologação e a máquina local. Essa organização pode te ajudar no futuro a gerenciar essas máquinas e usar isso em suas automações.


####Rodando o Ansible
Para rodar o ansible o comando é fácil

	ansible-playbook -i hosts projeto.yml

Ansible-playbook é o comando. -i  é o parâmetro que significa inventory, para inventário, onde passaremos nosso arquivo hosts. Por último nosso arquivo de tarefas. Sim! Não temos nenhuma tarefa, já vamos chegar lá.

Caso precise rodar o ansible com mais saidas de log, em um momento para resolver problemas por exemplo, você pode usar -v, de verbose.

	ansible-playbook -i hosts projeto.yml -v
	ansible-playbook -i hosts projeto.yml -vv
	ansible-playbook -i hosts projeto.yml -vvv
	ansible-playbook -i hosts projeto.yml -vvvv

As opções vão até 4 Vs. Onde cada um a mais, te mostra mais detalhes dos comandos e dos erros se houver.


####Criando tasks
Vamos começar com um exemplo bem simples de tarefa, um hello world por assim dizer.

	--
	# Projeto
	- hosts: "projeto"
	
	tasks:
	- name: "Vamos dar echo"
	  shell: 'echo teste'
	  
Lembra no nosso arquivo hosts a separação que fizemos com os colchetes? Use o nome que você definiu lá, aqui na opção hosts.

Em seguida criamos uma tarefa com o nome **Vamos dar echo**. E é isso que ela se dispõe a fazer. Rodando o playbook acima, ele vai acessar as máquinas presente no seu host e executar um **echo teste**.

Reparem que usamos o módulo **shell** do ansible para executar o comando. Vamos falar mais disso depois.

Vamos criar uma nova tarefa, agora usando o módulo **script** do ansible. Você deve ir aninhando as suas tarefas uma abaixo da outra como segue:

	--
	# Projeto
	- hosts: "projeto"
	
	tasks:
	  - name: "Vamos dar echo"
	    shell: 'echo teste'
	  
	  - name: "Executar um script"
	    script: '/bin/usr/meu.sh'
	  
Adicionamos a tarefa chamada **Executar um script**, que vai executar o .sh presente no caminho passado.


####Módulos
Ansible tem vários módulos como você pode conferir na documentação em [http://docs.ansible.com/ansible/modules_by_category.html](http://docs.ansible.com/ansible/modules_by_category.html). 

Esses módulos vem para te ajudar a criar tarefas das mais diferentes naturezas que você imaginar. Execução de linhas de comando, criação de arquivos, acesso a repositórios de versionamento, filas (rabbit, sqs, kafka), checar acesso a outras redes, instalação de programas, acesso a Amazon, Azure, Google Cloud, etc. Esses exemplos são poucos. Dê uma boa navegada na página acima para conferir a real gama de facilidades que o ansible nos dá.

Retorne os olhos nas tasks que fizemos acima e veja os módulos em ação. Usamos Shell e Script que fazem parte da categoria **Commands Modules** ([http://docs.ansible.com/ansible/list_of_commands_modules.html](http://docs.ansible.com/ansible/list_of_commands_modules.html)).

Para efeitos didáticos, não vamos usar em nossos exemplos aqui módulos muito diferentes e ousados. Mas não se limite! A documentação do Ansible é excelente e fácil de compreender e vai te ajudar com toda certeza.


####Argumentos
Os módulos podem ter argumentos / parâmetros. Alguns são nativos a todos os módulos do Ansible, outros são específicos. Confira a documentação para ir ficando a par disso.

	tasks:
	  - name: "Ver se existe a pasta do projeto criada"
	    shell: 'mkdir projeto'
	    args:
	      chdir: '/home'
	      creates: 'projeto'

Aqui com **args**. Usamos **chdir** para dizer aonde queremos executar nossa tarefa.
Também usamos **creates**, que nos ajuda checando se o mkdir vai ser necessário mesmo ou não.


####Variáveis
Podemos e devemos definir variáveis no topo de nossos playbooks para usá-las em nossas tasks.

	---
	# Projeto
	- hosts: "projeto"
	
	vars:
    	repo: git@bitbucket.org/flaviosilveira/primeiro-jogo-html5.git
    	document_root: /var/www
    	releases_folder: releases
    	
    - name: "Clone/Update projeto"
      git: 'repo=ssh://{{repo}} dest={{document_root}}/{{releases_folder}} clone=yes update=yes accept_hostkey=yes force=yes'	

Usamos as variáveis com seus nomes entre chaves duplas **{{nome_da_variavel}}**.

Repare como se compõe o comando para clonar ou atualizar nosso projeto usando o módulo git do ansible. Esse módulo faz clone se o projeto git não existir na máquina ou atualiza se ele já estiver lá.


####Passando variáveis pela linha de comando
Você consegue passar variáveis através da chamada do ansible, o que pode te dar ainda mais ideas em suas automações.

	ansible-playbook -i hosts projeto.yml -e "env=homologacao"
	
Com -e, passamos a variável **env** para nosso playbook. De dentro dele, vamos usar {{env}} para resgatar.

	---
	# Projeto
	- hosts: "projeto-{{env}}"
	
Lembram na definição de nossos hosts, quando fizemos uma variação com máquinas de homologação e uma máquina local? Aqui está um uso para essa organização, facilitando em você não ter de ficar alterando seus playbooks todo o tempo.


####Salvando saídas de tarefas como variável
Outra coisa legal é armazenar saídas de tarefas para variáveis e assim poder usá-las posteriormente.

	- name: "Contar pastas"
      shell: 'ls | wc -l'
      args:
        chdir: '{{document_root}}/{{releases_folder}}'
      register: to_remove

Na tarefa acima, usamos um comando Shell para contar um número de pastas.
Estamos usando argumentos para o módulo e também variáveis. Coisas que já vimos acima.

Em seguida registramos a saída desse comando para a variável **count**.
Para usá-la? {{count}}.

As vezes o que você coloca na variável é um objeto. Confira a saída em verbose (-vvvv) caso tenha problemas usando como acima. Talvez você precise de alternativas:

	{{count.stdout}} #Saída do ansible
	{{count.stdout | int}} #Mesmo que acima, mas convertendo para inteiro
	


####Condicionais
Uma task pode ser executada ou não baseado em uma condional.

	- name: "Remove pastas"
      shell: 'ls -t | tail -n $(($(ls | wc -l)-3)) | xargs rm -rf'
      args:
        chdir: '{{document_root}}/{{releases_folder}}'
      when: '{{count.stdout | int}} > 3'
      
Reparem na última linha, no **when**. Se a variável nos trouxer um resultado maior que 3, executaremos a tarefa, caso contrário não.

Para curiosidade, esse comando ordena as pastas por data, e deixa apenas as últimas 3, removendo o restante.


####Ignorando erros
As vezes algumas tarefas nos trarão erros, mas que por algum motivo não precisamos nos preocupar. Para isso, use **ignore_errors**.

	--
	# Projeto
	- hosts: "projeto"
	
	tasks:
	  - name: "Vamos dar echo"
	    shell: 'echo teste'
	    args:
	       chdir: '{{document_root}}/{{releases_folder}}'
	    ignore_errors: true
	    
Pronto, erros serão ignorados e seu playbook continuará em execução. 

Isso pode ser útil também para algum comando que tem uma saída de comando muito grande. O ansible as vezes considera isso como um erro.


####Usando Includes
Alguma tarefa que vai ser executada em mais de um playbook? Use Includes.
Crie uma pasta chamada **includes** e dentro dela crie um arquivo chamado **outro.yml**.

Dentro do seu arquivo **outro.yml**, você trabalha como se ele fosse uma tarefa normal

	---
	# Include responsavel pela criacao da pasta
	
	- name: "Ver se existe a pasta do projeto criada"
	  shell: 'mkdir projeto'
	  args:
	    chdir: '/home'
	    creates: 'projeto'
	    
Para usar o include em outros playbooks faça:

	tasks:
	  - include: 'includes/outro.yml'
	  
Quer passar variáveis para seus includes?
	
	tasks:
	  - include: 'includes/outro.yml variavel=3 variavel2={{document_root}}'
Reparem que definimos uma variável no momento de chamar o include e para a variável chamada **variavel2**, usamos uma variável que pode ter sido definida no topo de nosso playbook ou ainda que pode ter vindo da saída de uma task.


####That's It
É isso por hoje pessoal! Cobrimos aqui o bé-a-bá no ansible, criamos tarefas, definimos nossas máquinas afetadas, aprendemos sobre módulos, argumentos, variáveis e includes.

Exercite em sua infraestrutura. Se não tem uma infraestrutura para testar, experimente com máquinas virtuais ou ainda com containers em Docker, tema que viemos discutindo aqui no Blog recentemente ([http://flaviosilveira.com/2016/comece-com-docker/](http://flaviosilveira.com/2016/comece-com-docker/), [http://flaviosilveira.com/2016/docker-php7-e-php-built-in/](http://flaviosilveira.com/2016/docker-php7-e-php-built-in/)).

Desperte a automação em você! Grande Abraço!
{% endraw %}