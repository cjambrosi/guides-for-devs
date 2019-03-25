Instalando e Configurando Ambiente de Desenvolvimento PHP
===============================================

## Pilha: Apache, MariaDB, PHP 7

--------------------

## Antes de tudo, atualize os repositórios e o sistema:

> sudo apt update

> sudo apt upgrade

--------------------

## Apache

1. Instalando:

	> sudo apt install apache2 apache2-doc apache2-utils


2. Configurando:

	- Quando uma pasta é requisitada, o Apache busca primeiramente um arquivo chamado **"index.html"**, mas queremos que ele dê preferência aos arquivos PHP, então faremos o Apache buscar um arquivo **"index.php"**, para isso basta configurar o arquivo **"dir.conf"** com privilégios de root:

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

		- Devere aparecer a página de configuração padrão do Apache.

	- A seguir devemos habilitar o módulo **mod_rewrite**, o Módulo de Redirecionamento de URL’s do Apache, também conhecido como "URL’s amigáveis":

		> sudo a2enmod rewrite

		- Saída:
			```
			Enabling module rewrite.
			To activate the new configuration, you need to run:
			   systemctl restart apache2
			```

	- Feito isso, reinicie seu Apache:

		> sudo service apache2 restart

	- O módulo **rewrite** foi ativado, mas o Apache não configurou nada além da linha que ativa o módulo no arquivo de configuração do mesmo, deixando assim por conta de você editar manualmente os arquivos dos sites padrões. Acesse:

		> sudo nano /etc/apache2/sites-available/000-default.conf

		- Insira as linhas de código a baixo e salve:
			```
			<Directory />
			   Options FollowSymLinks
			   AllowOverride All
			</Directory>
			<Directory /var/www>
			    Options Indexes FollowSymLinks MultiViews
			    AllowOverride All`</br>
			    Order Allow,Deny
			    Allow from all
			</Directory>
			```

		- Exemplo: </br>
			![](https://github.com/CristianAmbrosi/tutoriais/blob/master/images/exemplo-c%C3%B3digo-m%C3%B3dulo-rewrite.png)

	- Depois de salvar o aquivo, reinicie novamente o Apache com o comando:

		> sudo service apache2 restart

	- Agora iremos adicionar uma diretiva global chamada **ServerName** para supremir uma mensagem de aviso do Apache. Então, abra o arquivo de configuração principal do Apache:

		> sudo nano /etc/apache2/apache2.conf

	- Dentro do arquivo, na parte inferior, adicione a diretiva **ServerName**, apontando para o seu nome do domínio primário ou o IP público do seu servidor. [(Se não souber como descobrir o IP do seu servidor, vá para o final do tutorial)](#encontrando-endereço-do-ip-público-do-seu-servidor).

		```
		. . .
		ServerName nome_de_domínio_do_servidor_ou_IP
		```
		- ou
		```
		. . .
		ServerName localhost
		```

	- Salve e feche o arquivo. Depois, verifique erros de sintaxe com o comando:

		> sudo apache2ctl configtest

		- Saída deve ser:

			`[secondary-label Output]`</br>
			`Syntax OK`

	- Reinicie o Apache para implementar as alterações:

		> sudo systemctl restart apache2

	- Verifique a versão do Apache com o comando a baixo:

		> sudo apache2 -v

--------------------

## MariaDB

1. Instalando:

	> sudo apt update

	> sudo apt install mariadb-server

	- Na instalação, não é mais solicitado que seja definida uma senha ou quaisquer outras configurações. 
	
	- O seriviço do banco de dados deve ser iniciado automaticamente. Use o comando a baixo para verificar:

		> sudo systemctl status mariadb

2. Configurando:

	- Quando a instalação estiver concluída, é preciso executar alguns comandos adicionais para ter nosso ambiente com o MariaDB configurado de forma segura. Isso irá remover alguns padrões perigosos e bloquear um pouco o acesso ao nosso sistema de banco de dados. Inicie o script interativo executando:

		> sudo mysql_secure_installation

    - Siga os seguintes passos para a configuração:

        - In order to log into MariaDB to secure it, we'll need the current password for the root user.  If you've just installed MariaDB, and you haven't set the root password yet, the password will be blank, so you should just press enter here. </br>
        Enter current password for root (enter for none):

        - OK, successfully used password, moving on...</br>
        Setting the root password ensures that nobody can log into the MariaDB root user without the proper authorisation.</br>
        Set root password? [Y/n] 

        - By default, a MariaDB installation has an anonymous user, anyone to log into MariaDB without having to have a user account created for them. This is intended only for testing, and to make the installation go a bit smoother.  You should remove them before moving into a production environment.</br>
        Remove anonymous users? [Y/n]: **`y`**

        - Normally, root should only be allowed to connect from 'localhost'.  This ensures that someone cannot guess at the root password from network. </br>
         Disallow root login remotely? [Y/n]: **`y`**

        - By default, MariaDB comes with a database named 'test' that anyone can access.  This is also intended only for testing, and should be removed before moving into a production environment.</br>
        Remove test database and access to it? [Y/n]: **`y`**

        - Reloading the privilege tables will ensure that all changes made so far will take effect immediately.</br>
        Reload privilege tables now? [Y/n]: **`y`**

3. Correção do erro **#1698**. Erro ao logar com um cliente como o phpMyAdmin.

	- No sistema Debian, no usuário **root** do MariaDB é configurado o plugin **unix_socket** para autentificação por padrão. Isso permite uma maior segurança e usabilidade em muitos casos, mas também pode complicar quando é preciso permitir privilégios administrativos de um programa externo (por exemplo, phpMyAdmin). 

	- Como o servidor usa a conta **raiz** para tarefas como rotação de log e iniciar, para o servidor é melhor não alterar os detalhes de autenticação da conta **raiz** . Mudar as credenciais da conta **/etc/mysql/debian.cnf** pode funcionar inicialmente, mas as atualizações de pacotes podem substituir essas alterações. Em vez de modificar a conta **raiz** , os mantenedores do pacote recomendam a criação de uma conta **administrativa** separada com privilégidos de **root**, caso você precise configurar o acesso baseado em senha.

	- Para fazer isso, crie um novo usuário **USER** com os mesmos recursos da conta raiz (root), mas configurada para autenticação de **senha** que será usado no logar do usuario **root**. Para fazer isso, abra o prompt do MariaDB no seu terminal e altere o nome de usuário e a senha para corresponder às suas preferências:
	
		> sudo mysql

		> GRANT ALL ON \*.\* TO 'USER'@'localhost' IDENTIFIED BY 'PASSWORD' WITH GRANT OPTION;

		- Substitua **USER** pelo usuário que achar melhor.

		- Substitua **PASSWORD** pela senha que achar melhor.

	- Libere os privilégios para garantir que eles sejam salvos e estejam disponíveis na sessão atual:

		> FLUSH PRIVILEGES;

	- Criado novo usuário, pode sair do prompt do MariaDB:

		> exit

	- Para testar o novo usuário criado, é possível tentar se conectar ao banco de dados pela ferramenta **mysqladmin**, que é um cliente que permite executar comandos administrativos.

		> mysqladmin -u USER -p version

		- Saída de exemplo:
	
		```
		mysqladmin  Ver 9.1 Distrib 10.1.37-MariaDB, for debian-linux-gnu on x86_64
		Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

		Server version		10.1.37-MariaDB-0+deb9u1
		Protocol version	10
		Connection		Localhost via UNIX socket
		UNIX socket		/var/run/mysqld/mysqld.sock
		Uptime:			1 hour 4 min 27 sec

		Threads: 1  Questions: 10  Slow queries: 0  Opens: 17  Flush tables: 1  Open tables: 11  Queries per second avg: 0.002
		```

--------------------

## PHP 7

- Atualmente, o PHP 7.0 está diponível para o Debian 9 Stable. Para instalar uma versão mais recente do PHP, é preciso adicionar a DPA do desenvolvedor [**Ondrej**](https://deb.sury.org/), que é o responsável pelo empacotamento do PHP no Debian e no Ubuntu, tanto na versão Stable quanto nas versões Unstable e Testing do Debian.

1. Instalando:

	- Instalando apartir do repositório oficial do Debian:

		> sudo apt update

		> sudo apt install php7.0 php7.0-cli php7.0-intl php7.0-mcrypt php7.0-opcache php7.0-readline libapache2-mod-php7.0 php7.0-mbstring php7.0-json php7.0-curl php-imagick php7.0-mysql phpmyadmin

	- Instalando apartir do repositório do [**Ondrej - Packages Sury**](https://packages.sury.org/php/):

		> sudo apt update

		- Instale as dependências necessárias para adicionar um novo repositório via HTTPS:

			> sudo apt install apt-transport-https ca-certificates curl software-properties-common

		- Importe a chave GPG do repositório:

			> sudo wget -q https://packages.sury.org/php/apt.gpg -O- | sudo apt-key add -

		- Adicione o repositório do à lista de repositórios de softwares do seu sistema:

			> echo "deb https://packages.sury.org/php/ stretch main" | sudo tee /etc/apt/sources.list.d/php.list

		- Atualize novamente os repositórios do sistema e instale o PHP:

			> sudo apt update

			> sudo apt install php7.3 php7.3-cli php7.3-intl php7.3-opcache php7.3-readline libapache2-mod-php7.3 php7.3-mbstring php7.3-json php7.3-curl php-imagick php7.3-mysql phpmyadmin

	- Servidor web a configurar automaticamente: </br>
		`[*] Apache2` </br>
		`[ ] lighttpd`

	- Configurar banco de dados para phpmyadmin com dbconfig-common? </br>
		`<Sim>`

	- Senha MySQL da aplicação para o phpmyadmin: </br>
		`<Insira uma senha e ok>`

	- Confirmação de senha: </br>
		`<Confirme a senha escolhida e Ok>`

	- Reinicie o Apache com o comando:

		> sudo service apache2 restart

	- Verifique a versão do PHP instalado com o comando:

		> php --version

2. Configurando:

	1. Corrigindo o erro **"Not Found"** do phpmyadmin, quando acessada a URL **"localhost/phpmyadmin"** ou **"127.0.0.1/phpmyadmin"**.

		- Abra o arquivo **"apache2.conf"** no modo root com qualquer editor e texto:

			> sudo nano /etc/apache2/apache2.conf

		- No final do arquivo, inclua as linhas de código a baixo e salve:

			`Include /etc/phpmyadmin/apache.conf`

		- Reinicie o Apache com o comando:

			> sudo service apache2 restart

	2. Ativar as extensões *php7.3-mbstring* e *php7.0-mcrypt*:

		> sudo phpenmod mbstring
		
		- *Ative a extensão **php7.0-mcrypt** somente se você instalou o PHP 7.0 ou 7.1 pelo repositório padrão. Até o momento, não existe a versão 7.2 ou 7.3 para a extensão **mcrypt**, ao invés dela, está sendo usada a biblioteca **libsodium** para criptografia.*

		> sudo phpenmod mcrypt

	3. Habilitar as mensagens de erros do PHP 7.1.

		- Para habilitar as mensagens erros, precisamos editar o arquivo *php.ini*. Acesse o diretório referente a versão do PHP que você instalou e depois abra o arquivo com privilégios de super usuário:

			> sudo nano /etc/php/7.*/apache2/php.ini

		- Com o arquivo aberto, procure pelas variáveis **display_errors**, **display_startup_errors** e **log_errors**. Altere o valor de *Off* para *On* nas variáveis, como na imagem a baixo:

			![](https://github.com/CristianAmbrosi/tutoriais/blob/master/images/hab-mesg-erro.png)

		- Procure pela variável **error_log**, remova o **;** da frente e configure um caminho para armazenar o arquivo de logs de erros, assim como na imagem a baixo *(certifique-se de que o arquivo tenha permissão de leitura e escrita)*:

			![](https://github.com/CristianAmbrosi/tutoriais/blob/master/images/arq-log-erro.png)

		- Salve o arquivo e reinicie o apache:

			> sudo service apache2 restart


	4. Teste se a instalação do PHP está correta. Crie um arquivo **"info.php"** no diretório dos projetos **"/var/www/html"** e dentro do arquivo insira a função a baixo e salve:

		`<?php phpinfo(); ?>`

		- Vá no navegador e acesse o arquivo pela URL:

			> "localhost/info.php" ou "127.0.0.1/info.php"

		- Se abrir a página de informações do PHP, a instalação da linguagem está correta.

--------------------

## Gerenciar os serviços Apache e MariaDB no sistema

- Para verificar todos os serviços atualmente em execução, use o comando a baixo:

	> ps -A

- Desabilitar ou habilitar os serviços na inicialização do sistema.

    - Verificar status dos serviços:

    	> sudo systemctl status apache2

    	> sudo systemctl status mariadb

    	- Apache:

    		- Para desabilitar o serviço use:

    			> sudo systemctl stop apache2

    			> sudo systemctl disable apache2

    		- Para habilitar o serviço use:

    			> sudo systemctl enable apache2

    			> sudo systemctl start mariadb

    	- MariaDB:

    		- Para desabilitar o serviço use:

    			> sudo systemctl stop mariadb

    			> sudo systemctl disable mariadb

    		- Para habilitar o serviço use:

    			> sudo systemctl enable mariadb

    			> sudo systemctl start mariadb

    	- Para reiniciar um serviço use:

    		> sudo systemctl restart apache2

    		> sudo systemctl restart mariadb

--------------------

## Encontrando Endereço do IP Público do seu Servidor

Geralmente, esse é o endereço que você utiliza para se conectar ao seu servidor através do SSH.

1. Primeira Forma:

	- Utilizando a ferramenta **cURL** para entrar em contato com algum meio externo, para lhe dizer como ele vê o seu servidor. Você pode fazer isso perguntando a um servidor específico qual é o seu IP:

		> sudo apt install curl

		> curl http://icanhazip.com

	- *Independentemente do meio que você usa para obter seu endereço IP, você pode digitá-lo na barra de endereço do seu navegador web para chegar ao seu servidor.*

2. Segunda Forma:
	
	- Você pode utilizar as ferramentas do **iproute2** para obter seu endereço digitando isso:

		> ip addr show eth0 | grep inet | awk '{ print $2; }' | sed 's/\/.*$//'

		- Esse comando vai lhe retornar duas ou três linhas. Todos são endereços corretos, mas seu computador só poderá utilizar um deles, portanto, sinta-se livre para tentar cada um.

--------------------

## Referências

- Pilha LAMP

	https://elias.praciano.com/2017/07/como-instalar-um-servidor-web-lamp-no-debian-9/

	https://www.linuxbabe.com/debian/install-lamp-stack-debian-9-stretch

	https://www.vivaolinux.com.br/topico/Apache-Web-Server/Erro-ao-acessar-o-apache2

	https://askubuntu.com/questions/256013/apache-error-could-not-reliably-determine-the-servers-fully-qualified-domain-n

	https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mariadb-php-lamp-stack-debian9

	https://www.digitalocean.com/community/tutorials/como-instalar-a-pilha-linux-apache-mysql-php-lamp-no-ubuntu-16-04-pt

	https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-phpmyadmin-on-ubuntu-14-04

	https://ubuntuserverguide.com/2014/06/how-to-install-lamp-in-ubuntu-server-14-04-lts.html

	https://www.youtube.com/watch?v=Q2N5blJ4VIo

	https://www.youtube.com/watch?v=bDi9h8LJHuE

- PHP

	https://linuxize.com/post/how-to-install-php-on-debian-9/

    https://www.rosehosting.com/blog/how-to-install-php-7-2-on-debian-9/

    https://lukasmestan.com/install-libsodium-extension-in-php7/

    https://stackoverflow.com/questions/48363789/warning-module-mcrypt-ini-file-doesnt-exist-under-etc-php-7-2-mods-available

	https://www.digitalocean.com/community/tutorials/how-to-use-systemctl-to-manage-systemd-services-and-units

	https://www.vivaolinux.com.br/topico/Iniciantes-no-Linux/comando-service-e-invoke-rcd-nao-funciona-debian-8-help-me

	https://pt.wikihow.com/Reiniciar-Servi%C3%A7os-no-Linux

	https://matheuslima.com.br/instalando-o-nginx-php-7-mysql-lemp/

	https://www.vivaolinux.com.br/topico/PHP/The-mbstring-extension-is-missing-Please-check-your-PHP-configuration

	http://ubuntuforum-br.org/index.php?topic=74091.0

- MariaDB

	https://www.digitalocean.com/community/tutorials/how-to-install-mariadb-on-debian-9

	https://linuxize.com/post/how-to-install-mariadb-on-debian-9/

	http://eriberto.pro.br/blog/2018/09/04/instalando-e-configurando-mariadb-no-debian-9/

	https://stackoverflow.com/questions/50409788/mysql-8-create-new-user-with-password-not-working

- Módulos:

	https://www.debian.org/

	http://php.net/manual/pt_BR/intro.mcrypt.php

	http://php.net/manual/pt_BR/intro.mbstring.php

	http://php.net/manual/pt_BR/function.readline.php

- Habilitar mod_rewrite:

	http://gilbertoalbino.com/linux-habilitar-mod_rewrite-no-ubuntu/

	http://book.cakephp.org/3.0/pt/installation.html