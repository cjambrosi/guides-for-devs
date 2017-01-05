

Instalando e Configurando Ambiente de Desenvolvimento PHP para o CakePHP | Pilha LAMP - Apache, MySQL/Postegres, PHP5 | Ubuntu
===============================================

--------------------

## Primeiramente, atualizar os repositórios e gatilhos do Ubuntu:

> sudo apt-get update

> sudo apt-get upgrade

--------------------

## Apache

1. Instalando:

	> sudo apt-get install apache2 apache2-doc apache2-utils


2. Configurando:

	- Quando uma pasta é requisitada, o Apache olha/busca primeiramente um arquivo chamado **"index.html"**, mas queremos que ele dê preferência aos arquivos PHP, então faremos o Apache olhar/buscar um arquivo **"index.php"**, para isso basta configurarmos o arquivo **"dir.conf"** com privilégios de root:

		> sudo nano /etc/apache2/mods-enabled/dir.conf

	- Ele terá está aparência:

		`<IfModule mod_dir.c>
		    DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
		</IfModule>`

	- Então movemos o arquivo **"index.php"** para a primeira posição, ficando assim:

		`<IfModule mod_dir.c>
		    DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
		</IfModule>`

	- Depois disso, precisamos reiniciar o servidor web Apache de forma que nossas alterações sejam reconhecidas. Você pode fazer isto digitando o seguinte comando:

		> sudo service apache2 restart

	- Para saber se o servidor já está respondendo, abra seu navegador e acesse a URL:

		 > "localhost/" ou "127.0.0.1/" 

		- Deverá aparecer a página de configuração padrão do Apache. 

	- Devemos habilitar o módulo **mod_rewrite**, o Módulo de Redirecionamento de URL’s do Apache, também conhecido como "URL’s amigáveis".

		> sudo a2enmod rewrite

	- Feito isso, reinicie seu apache:

		> sudo service apache2 restart

	- O módulo **rewrite** foi ativado, mas o apache não configurou nada além da linha que ativa o módulo no arquivo de configuração do módulo, deixando assim por conta de você editar manualmente os arquivos dos sites padrões. Acesse:

		> sudo nano /etc/apache2/sites-available/000-default.conf

		- Insira as linhas de código a baixo e salve:

			`<Directory />`</br>
			    `Options FollowSymLinks`</br>
			   ` AllowOverride All`</br>
			`</Directory>`</br>
			`<Directory /var/www>`</br>
			    `Options Indexes FollowSymLinks MultiViews`</br>
			    `AllowOverride All`</br>
			    `Order Allow,Deny`</br>
			    `Allow from all`</br>
			`</Directory>`

	- Depois de ter salvado o arquivo, reinicie novamente o Apache com o comando:

		> sudo service apache2 restart

--------------------

## MySQL

1. Instalando:

	> sudo apt-get install mysql-server libapache2-mod-auth-mysql

- Siga os seguintes passos para a instalação:

	- Nova palavra-passe para o utilizador **"root"** de MySQL: </br>
		`<Inserir senha escolhida>`

	- Repita a palavra-passe para o utilizador **"root"** de MySQL: </br>
		`<Repetir senha escolhida>`

	- Configurar a base de dados para phpmyadmin com dbconfig-commom? </br>
		`<Sim>`

	- Palavra-passe do utilizador administrativo da base dados: </br>
		`<Inserir senha escolhida e ok>`

	- Palavra-passe da aplicação MySQL para phpmyadmin: </br>
		`<Inserir senha escolhida e Ok>`

	- Confirmação de senha: </br>
		`<Confirmar senha escolhida e Ok>`

	- Servidor web a configurar automaticamente: </br>
		[*****] Apache2
		[ ]	lighttpd

2. Configurando:

	- Acesse via terminal com seu usuário e senha para saber se está conectando ao banco MySQL com o seguinte comando:

		> mysql -uroot -p

	- O comando **"-u"** serve para passar o usuário, no caso **"root"** (sem espaço entre os dois) e o comando **"-p"** vai pedir a senha do usuário. Para sair do banco na linha de comando pressione:

		> mysql> Ctrl + d

	- Quando a instalação estiver concluída, precisaremos executar alguns comandos adicionais para ter nosso ambiente MySQL configurado de forma segura. 

	- Primeiro, precisamos dizer ao MySQL para criar sua estrutura de diretório de banco de dados, onde ele irá armazenar suas informações. Ele prepara o terreno, criando a base de dados **"mysql"** (usada para armazenar a configuração do servidor MySQL, incluindo informações sobre os usuários e sobre as demais bases de dados) e também uma base de dados chamada **"test"**, que pode ser usada para testar o servidor. Você pode fazer isto digitando:

		> sudo mysql_install_db

	- Depois, iremos executar um script simples de segurança que vai remover alguns padrões perigosos e bloquear um pouco o acesso ao nosso sistema de banco de dados. Inicie o script interativo executando:

		> sudo mysql_secure_installation
		
	- Siga os seguintes passos para a configuração:

		- Enter current password for root (enter for name): </br>
			`<sua senha escolhida para o BD MySQL>`

		- Change the root password? (Mudar senha do root?)[y/n]: **n**

		- Remove anonymous users? (Remover usuários anônimos?)[y/n]: **y**

		- Disallow root login remotely? (Não permitir que o usuário root faça login de outro local que não seja da própria máquina)[y/n]: **y**

		- Remove test database and access to it? (Remover o teste database?)[y/n]: **y** 

		- Reloaded privilege tables now? (Reloaded dos privilégios?)[y/n]: **y**

	- Corrigir erro **"Not Found"** do phpmyadmin, quando acessada a URL **"localhost/phpmyadmin"** ou **"127.0.0.1/phpmyadmin"**.

		- Abra o arquivo **"apache2.conf"** no modo root com qualquer editor e texto:

			> sudo nano /etc/apache2/apache2.conf

		- No final do arquivo inserir as linhas de código a baixo e salvar.

			` Include /etc/phpmyadmin/apache.conf`

		- Salvado o arquivo, reiniciar o Apache com o comando:

			> sudo service apache2 restart

--------------------

# PostgreSQL

1. Instalando:

	> sudo apt-get install postgresql-9.3 postgresql-contrib-9.3

	> sudo apt-get install pgadmin3
		

2. Configurando:

	- Depois de instalado o SGBD Postgres, vamos criar o primeiro usuário do Banco de Dados. Logue-se como usuário **root** usando o comando a baixo: 

		> sudo -i

	- Entre como usuário postgres com o comando:

		> su postgres

	- Conecte no banco com o comando (deve aparecer a mensagem de boas vindas):

		> postgres=# psql

	- Para criar o Usuário, entre com o comando a baixo (troque **"nomedousuario"** pelo seu usuário) e tecle enter:

		> postgres=# CREATE USER nomedousuario SUPERUSER INHERIT CREATEDB CREATEROLE;

	- Para criar uma Senha ao usuário já criado, entre com o comando a baixo (troque **"nomedousuario"** pelo seu usuário e troque **'senha'** pela sua senha escolhida) e tecle enter: 

		> postgres=# ALTER USER nomedousuario PASSWORD 'senha';

	- Usuário e senha foram criados. Tecle o comando a baixo para sair da linha de comando do PostegreSQL:

		> postgres=# \q

	- Tecle o comando a baixo para sair do usuário postegres:

		> exit

--------------------

## PHP

1. Instalando:

	- **MySQL:**
	
		> sudo apt-get install php5 php5-geoip php5-imagick php5-intl php5-mysql php5-mcrypt php5-readline phpmyadmin

	- **PostgreSQL:**

		> sudo apt-get install php5 php5-geoip php5-imagick php5-intl php5-pgsql php5-mcrypt php5-readline

2. Configurando:

	- Ativar a extensão do php5-mcrypt:

		> sudo php5enmod mcrypt

	- Depois de ativada a extensão do php5-mcrypt, reiniciar o Apache:

		> sudo service apache2 restart

	- Somente testar se a instalação do PHP está correta. Criar um arquivo **"info.php"** no diretório dos projetos **"/var/www/html"** e dentro do arquivo inserir a função a baixo e salvar.

		`<?php phpinfo(); ?>`

	- Ir no navegador e acessar o arquivo pela URL: 
			
		> "localhost/info.php" ou "127.0.0.1/info.php" 

	- Se abrir a página de informações do PHP, a instalação da linguagem está correta.

--------------------

## O que foi instalado?!

**apache2 =>** Servidor web livre mais utilizado no mundo, onde rodam suas aplicações;

**pgadmin3 =>** Software gráfico para administração do SGBD PostgreSQL;
	
**php5 =>** Linguagem de programação na qual serão feitos os projetos;

**apache2-doc =>** Documentação completa do Apache;

**apache2-utils =>** Contém diversos utilitários de gerenciamento do Apache que possívelmente serão utilizados;

**mysql-server =>** Banco de Dados MySQL;
	
**postgresql-9.3 =>** Banco de Dados PostgreSQL, instalar a versão estável mais atualizada;
	
**phpmyadmin =>** Aplicação web para o gerenciamneto do SGBD MySQL;
	
**php5-geoip =>** Módulo do PHP que permite que você encontre a localização de um endereço IP - Cidade, Estado, País, Longitude, Latitude e outras informações, como o ISP e o tipo de conexão;
	
**php5-imagick =>** É uma extensão nativa do PHP para criar e modificar imagens usando a API do ImageMagick;
	
**php5-intl =>** Contém um módulo para facilitar a internacionalização de scripts PHP;

**php5-pgsql =>** Drive que irá fazer conexão com o Banco de Dados PostgreSQL diretamente de scripts PHP;

**php5-mysql =>** Este pacote fornece módulos para conexões de banco de dados MySQL diretamente de scripts PHP. Inclui o módulo genérico "mysql", que pode ser usado para conectar-se a todas as versões do MySQL;

**php5-mcrypt =>** Pacote que contém um módulo para funções mcrypt em scripts PHP;

**php5-readline =>** Pacote que contém um módulo para funções readline (baseado em libedit) em scripts PHP;

**postgresql-contrib-9.3 =>** Contém diversos utilitários do Banco de Dados PostgreSQL;

**libapache2-mod-auth-mysql =>** Módulo para o servidor web Apache 2, que permite a autenticação HTTP contra as informações armazenadas em um banco de dados MySQL.

--------------------

# Fontes:

- All Packages:

	https://www.debian.org/

- Habilitar mod_rewrite:

	http://gilbertoalbino.com/linux-habilitar-mod_rewrite-no-ubuntu/

	http://book.cakephp.org/3.0/pt/installation.html

- php5-readline:

	http://php.net/manual/pt_BR/function.readline.php

- Criando Usuário PostgreSQL:

	https://www.vivaolinux.com.br/dica/Criacao-de-1edeg;-super-usuario-no-PostgreSQL

	https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-phpmyadmin-on-ubuntu-14-04

	https://www.digitalocean.com/community/tutorials/como-instalar-a-pilha-linux-apache-mysql-php-lamp-no-ubuntu-14-04-pt

	https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mysql-php-lamp-stack-on-ubuntu-14-04

	http://ubuntuserverguide.com/2014/06/how-to-install-lamp-in-ubuntu-server-14-04-lts.html

	http://www.ubuntuiniciantes.com.br/2013/08/instalando-o-php-apache-e-postgres-no.html

	http://www.hardware.com.br/tutoriais/configurando-servidor-lamp/pagina4.html

	http://blog.wfsneto.com.br/2014/06/21/php-configurando-ambiente-de-densenvolvimento-ubuntu-14-04

	https://www.youtube.com/watch?v=Q2N5blJ4VIo

	https://www.youtube.com/watch?v=bDi9h8LJHuE

	https://www.youtube.com/watch?v=LYgQW4a_anA
