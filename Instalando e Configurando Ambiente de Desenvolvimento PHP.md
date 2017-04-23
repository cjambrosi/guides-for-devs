Instalando e Configurando Ambiente de Desenvolvimento PHP para o CakePHP | Pilha: Apache, MySQL/Postegres, PHP5 | Ubuntu >= 16.04
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

	- A seguir, iremos adicionar uma diretiva global chamada **ServerName** para supremir uma mesnagem de aviso do Apache. Então abra o arquivo de configuração principal do Apache.

		> sudo nano /etc/apache2/apache2.conf

	- Dentro do arquivo, na parte inferior, adicione a diretiva **ServerName**, apontando para o seu nome do domínio primário ou o IP público do seu servidor. [(Se não souber como descobrir o IP do seu servidor, vá para o final do tutorial)](#encontrando-endereço-do-ip-público-do-seu-servidor).

		`. . .`</br>
		`ServerName nome_de_domínio_do_servidor_ou_IP`

	- Salve e feche o arquivo. Depois verifique erros de sintaxe com o comando:

		> sudo apache2ctl configtest

		- Saída deverá ser:

			`[secondary-label Output]`</br>
			`Syntax OK`

	- Reinicie o Apache para implementar as alterações.

		> sudo systemctl restart apache2

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

		- Exemplo: </br>
			![](https://github.com/CristianAmbrosi/tutoriais/blob/master/images/exemplo-c%C3%B3digo-m%C3%B3dulo-rewrite.png)
	- Depois de ter salvo o arquivo, reinicie novamente o Apache com o comando:

		> sudo service apache2 restart

--------------------

## MySQL

1. Instalando:
	
	> sudo apt-get update

	> sudo apt-get install mysql-server

	- Nova palavra-passe para o utilizador **"root"** de MySQL: </br>
		`<Inserir senha escolhida>`

	- Repita a palavra-passe para o utilizador **"root"** de MySQL: </br>
		`<Repetir senha escolhida>`
		
2. Configurando:

	- Acesse via terminal com seu usuário e senha para saber se está conectando ao banco MySQL com o seguinte comando:

		> mysql -uroot -p

	- O comando **"-u"** serve para passar o usuário, no caso **"root"** (sem espaço entre os dois) e o comando **"-p"** vai pedir a senha do usuário. Para sair do banco na linha de comando pressione:

		> mysql> Ctrl + d

	- *(OPCIONAL)* Quando a instalação estiver concluída, precisaremos executar alguns comandos adicionais para ter nosso ambiente MySQL configurado de forma segura. 
	Iremos executar um script simples de segurança que vai remover alguns padrões perigosos e bloquear um pouco o acesso ao nosso sistema de banco de dados. Inicie o script interativo executando:

		- *(IMPORTANTE)* A habilitação dessa funcionalidade é algo que deve ser avaliado. Se habilitado, senhas que não seguem o critério especificado (senha root por exmplo) serão rejeitadas pelo MySQL com um erro. Isso irá causar problemas se você utilizar uma senha fraca juntamente com software que configura automaticamente as credenciais de usuário do MySQL, tais como os pacotes do Ubuntu para o phpMyAdmin. É seguro deixar a validação desativada, mas você deve sempre utilizar senhas fortes e exclusivas para as credenciais do banco de dados.
		</br></br>
		
		> sudo mysql_secure_installation
		
	- Siga os seguintes passos para a configuração:

		- Enter password for user root: `<sua senha escolhida para o BD MySQL>`</br>

		- VALIDATE PASSWORD PLUGIN can be used to test passwords
		and improve security. It checks the strength of password
		and allows the users to set only those passwords which are
		secure enough. Would you like to setup VALIDATE PASSWORD plugin?
		</br></br>
		Press y|Y for Yes, any other key for No:  **`y`**
		
		- There are three levels of password validation policy:
		LOW    Length >= 8
		MEDIUM Length >= 8, numeric, mixed case, and special characters
		STRONG Length >= 8, numeric, mixed case, special characters and dictionary file
		Please enter 0 = LOW, 1 = MEDIUM and 2 = STRONG:  **`0`**, **`1`** ou **`2`**

		- Estimated strength of the password: 25 
		Change the password for root ? (Press y|Y for Yes, any other key for No): `Se estiver satisfeito com a sua senha atual, digite` **`n`**, `se não digite` **`y`** `para altera-la.`

			- Estimated strength of the password: 100 
			Do you wish to continue with the password provided?(Press y|Y for Yes, any other key for No) : **`n`**

		- Remove anonymous users? (Press y|Y for Yes, any other key for No): **`y`**

		- Disallow root login remotely? (Press y|Y for Yes, any other key for No): **`y`**

		- Remove test database and access to it? (Press y|Y for Yes, any other key for No): **`y`** 

		- Reload privilege tables now? (Press y|Y for Yes, any other key for No): **`y`**

--------------------

## PostgreSQL

1. Instalando:
	
	> sudo apt-get update

	> sudo apt-get install postgresql postgresql-contrib

	> sudo apt-get install pgadmin3

	- Consultar versão instalada. 

		> psql --version

		`psql (PostgreSQL) 9.5.6`
		

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
	- *(IMPORTANTE)* Se for instalar os dois Bancos de Dados (MySQL e PostgresSQL),  

	- **MySQL:**

		> sudo apt-get update
	
		> sudo apt-get install php7.0 php7.0-cli php7.0-intl php7.0-mysql php7.0-mcrypt php7.0-readline php-geoip php-imagick phpmyadmin libapache2-mod-php7.0 php7.0-mbstring

		- Servidor web a configurar automaticamente: </br>
			`[*] Apache2` </br>
			`[ ] lighttpd`

		- Configurar banco de dados para phpmyadmin com dbconfig-common? </br>
			`<Sim>`

		- Senha MySQL da aplicação para o phpmyadmin: </br>
			`<Inserir senha escolhida e ok>`

		- Confirmação de senha: </br>
			`<Confirmar senha escolhida e Ok>`

		- Agora iremos corrigir o erro **"Not Found"** do phpmyadmin, quando acessada a URL **"localhost/phpmyadmin"** ou **"127.0.0.1/phpmyadmin"**.

		- Abra o arquivo **"apache2.conf"** no modo root com qualquer editor e texto:

			> sudo nano /etc/apache2/apache2.conf

		- No final do arquivo inserir as linhas de código a baixo e salvar.

			` Include /etc/phpmyadmin/apache.conf`

		- Salvado o arquivo, reiniciar o Apache com o comando:

			> sudo service apache2 restart

	- **PostgreSQL:**

		> sudo apt-get update

		> sudo apt-get install php7.0 php7.0-intl php7.0-mcrypt php7.0-readline php-geoip php-imagick php7.0-pgsql

2. Configurando:

	- Ativar a extensão do php7.0-mcrypt:

		> sudo phpenmod mcrypt

	- Depois de ativada a extensão do php5-mcrypt, reiniciar o Apache:

		> sudo service apache2 restart

	- Teste se a instalação do PHP está correta. Crie um arquivo **"info.php"** no diretório dos projetos **"/var/www/html"** e dentro do arquivo inserira a função a baixo e salve.

		`<?php phpinfo(); ?>`

	- Ir no navegador e acessar o arquivo pela URL: 
			
		> "localhost/info.php" ou "127.0.0.1/info.php" 

	- Se abrir a página de informações do PHP, a instalação da linguagem está correta.

--------------------

## Encontrando Endereço do IP Público do seu Servidor

Geralmente, esse é o endereço que você utiliza para se conectar ao seu servidor através do SSH.

1. Primeira Forma:

- A partir da linha de comando, você pode encontrar isso de algumas maneiras. Primeiro, você pode utilizar as ferramentas **iproute2** para obter seu endereço digitando isso:

	> ip addr show eth0 | grep inet | awk '{ print $2; }' | sed 's/\/.*$//'

	- Esse comando vai lhe retornar duas ou três linhas. Todos são endereços corretos, mas seu computador só poderá utilizar um deles, portanto, sinta-se livre para tentar cada um.

2. Segunda Forma: 

- Um método alternativo é usar o utilitário **curl** para entrar em contato com algum meio externo para lhe dizer como ele vê o seu servidor. Você pode fazer isso perguntando a um servidor específico qual é o seu IP:

	> sudo apt-get install curl

	> curl http://icanhazip.com

- *Independentemente do meio que você usa para obter seu endereço IP, você pode digitá-lo na barra de endereço do seu navegador web para chegar ao seu servidor.*

--------------------

## O que foi instalado?!

**apache2 =>** Servidor web livre mais utilizado no mundo, onde rodam suas aplicações;

**pgadmin3 =>** Software gráfico para administração do SGBD PostgreSQL;
	
**php7.0 =>** Linguagem de programação na qual serão feitos os projetos;

**apache2-doc =>** Documentação completa do Apache;

**apache2-utils =>** Contém diversos utilitários de gerenciamento do Apache que possívelmente serão utilizados;

**mysql-server =>** Banco de Dados MySQL;
	
**postgresql =>** Banco de Dados PostgreSQL, instalar a versão estável mais atualizada;
	
**phpmyadmin =>** Aplicação web para o gerenciamneto do SGBD MySQL;
	
**php-geoip =>** Módulo do PHP que permite que você encontre a localização de um endereço IP - Cidade, Estado, País, Longitude, Latitude e outras informações, como o ISP e o tipo de conexão;
	
**php-imagick =>** É uma extensão nativa do PHP para criar e modificar imagens usando a API do ImageMagick;
	
**php7.0-intl =>** Contém um módulo para facilitar a internacionalização de scripts PHP;

**php7.0-pgsql =>** Drive que irá fazer conexão com o Banco de Dados PostgreSQL diretamente de scripts PHP;

**php7.0-mysql =>** Este pacote fornece módulos para conexões de banco de dados MySQL diretamente de scripts PHP. Inclui o módulo genérico "mysql", que pode ser usado para conectar-se a todas as versões do MySQL;

**php7.0-mcrypt =>** Pacote que contém um módulo para funções mcrypt em scripts PHP. Maioria dos Frameworks exige que este módulo esteja ativado;

**php7.0-readline =>** Pacote que contém um módulo para funções readline (baseado em libedit) em scripts PHP;

**postgresql-contrib =>** Contém diversos utilitários do Banco de Dados PostgreSQL;

**libapache2-mod-auth-mysql =>** Módulo para o servidor web Apache 2, que permite a autenticação HTTP contra as informações armazenadas em um banco de dados MySQL.

--------------------

# Fontes:

https://www.digitalocean.com/community/tutorials/como-instalar-a-pilha-linux-apache-mysql-php-lamp-no-ubuntu-16-04-pt

https://matheuslima.com.br/instalando-o-nginx-php-7-mysql-lemp/

https://www.vivaolinux.com.br/topico/PHP/The-mbstring-extension-is-missing-Please-check-your-PHP-configuration

- All Packages:

	https://www.debian.org/

- Habilitar mod_rewrite:

	http://gilbertoalbino.com/linux-habilitar-mod_rewrite-no-ubuntu/

	http://book.cakephp.org/3.0/pt/installation.html

- php5-readline:

	http://php.net/manual/pt_BR/function.readline.php

- Criando Usuário PostgreSQL:

	https://www.digitalocean.com/community/tutorials/como-instalar-e-utilizar-o-postgresql-no-ubuntu-16-04-pt

	https://www.rosehosting.com/blog/install-postgresql-with-phppgadmin-on-ubuntu/

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
