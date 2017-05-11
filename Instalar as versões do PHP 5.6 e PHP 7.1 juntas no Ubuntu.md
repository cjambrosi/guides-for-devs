Instalar as versões do PHP 5.6 e PHP 7.1 juntas no Ubuntu >= 14.04
===============================================

--------------------

## Importante

- Se você tiver uma versão do PHP mais recente instalada em seu sistema e precisa instalar uma versão mais antiga,  você precisará desinstalar a versão mais recente, instalar a mais antiga e depois reinstalar a versão mais recente.

- Se você instalar o PHP para os dois Banco de Dados (MySQL e PostgreSQL), deve manter atenção para instalar somente os módulos necessários para cada um.

- Esse repositório (*ppa:ondrej/php*) é mantido pelo [Ondřej Surý](https://launchpad.net/~ondrej).

--------------------

## Primeiramente, atualizar os repositórios e gatilhos do Ubuntu

> sudo apt-get update

> sudo apt-get upgrade

--------------------

## Para o Banco de Dados MySQL

- Adicionar o repositório:
	
	> sudo add-apt-repository ppa:ondrej/php

	> sudo apt-get update

- Instalando o PHP 5.6
	
	> sudo apt-get install php5.6 php5.6-cli php5.6-intl php5.6-mcrypt php5.6-opcache php5.6-readline libapache2-mod-php5.6 php5.6-mbstring php5.6-json php5.6-curl php-imagick php5.6-mysql phpmyadmin
	
	- Verificar a versão instalada:
		
		> php -v
		
	- Ou:
	
		> php --version

	- Exemplo de saída:

		`PHP 5.6.30-10+deb.sury.org~xenial+2 (cli)`</br>
		Copyright (c) 1997-2016 The PHP Group`</br>
		Zend Engine v2.6.0, Copyright (c) 1998-2016 Zend Technologies`</br>
		    with Zend OPcache v7.0.6-dev, Copyright (c) 1999-2016, by Zend Technologies`</br>

- Instalando o PHP 7.1

	> sudo apt-get install php7.1 php7.1-cli php7.1-intl php7.1-mcrypt php7.1-opcache php7.1-readline libapache2-mod-php7.1 php7.1-mbstring php7.1-json php7.1-curl php-imagick php7.1-mysql phpmyadmin
	
	- Verificar a versão instalada:
		
		> php -v
		
	- Ou:
	
		> php --version

	- Exemplo de saída:

		`PHP 7.1.4-1+deb.sury.org~xenial+1 (cli) (built: Apr 11 2017 22:12:32) ( NTS )
		Copyright (c) 1997-2017 The PHP Group
		Zend Engine v3.1.0, Copyright (c) 1998-2017 Zend Technologies
		    with Zend OPcache v7.1.4-1+deb.sury.org~xenial+1, Copyright (c) 1999-2017, by Zend Technologies`

--------------------

## Para o Banco de Dados PostgreSQL

- Adicionar o repositório:

	> sudo add-apt-repository ppa:ondrej/php
	
	> sudo apt-get update
	
- Instalando o PHP 5.6

	> sudo apt-get install php5.6 php5.6-cli php5.6-intl php5.6-mcrypt php5.6-opcache php5.6-readline libapache2-mod-php5.6 php5.6-mbstring php5.6-json php5.6-curl php-imagick php5.6-pgsql

	- Verificar a versão instalada:
			
		> php -v
			
	- Ou:
	
		> php --version

	- Exemplo de saída:

		`PHP 5.6.30-10+deb.sury.org~xenial+2 (cli)
		Copyright (c) 1997-2016 The PHP Group
		Zend Engine v2.6.0, Copyright (c) 1998-2016 Zend Technologies
		    with Zend OPcache v7.0.6-dev, Copyright (c) 1999-2016, by Zend Technologies`

- Instalando o PHP 7.1

	> sudo apt-get install php7.1 php7.1-cli php7.1-intl php7.1-mcrypt php7.1-opcache php7.1-readline libapache2-mod-php7.1 php7.1-mbstring php7.1-json php7.1-curl php-imagick php7.1-pgsql

	- Verificar a versão instalada:
		
		> php -v
		
	- Ou:
	
		> php --version

	- Exemplo de saída:

		`PHP 7.1.4-1+deb.sury.org~xenial+1 (cli) (built: Apr 11 2017 22:12:32) ( NTS )
		Copyright (c) 1997-2017 The PHP Group
		Zend Engine v3.1.0, Copyright (c) 1998-2017 Zend Technologies
		    with Zend OPcache v7.1.4-1+deb.sury.org~xenial+1, Copyright (c) 1999-2017, by Zend Technologies`

--------------------

## Alternando entre as duas versões instaladas

- Se estiver na versão do PHP 5.6 e quiser usar a versão do PHP 7.1, digite os comandos na seguinte ordem:
	
	> sudo a2dismod php5.6
	
	- Saída:
		`odule php5.6 disabled.`
		
	> sudo a2enmod php7.1
	
	- Saída:
		`Enabling module php7.1.`

	> sudo service apache2 restart

	> sudo update-alternatives --set php /usr/bin/php7.1

- Se estiver na versão do PHP 7.1 e quiser usar a versão do PHP 5.6, digite os comandos na seguinte ordem:
	
	> sudo a2dismod php7.1
	
	- Saída:
		`Module php7.1 disabled.`

	> sudo a2enmod php5.6
	
	- Saída:
		`Enabling module php5.6.`

	> sudo service apache2 restart

	> sudo update-alternatives --set php /usr/bin/php5.6

--------------------

## Testar as duas versões instaladas
Para testar se a versão do PHP 7.1 está funcionando junto a do PHP 5.6, podemos utilizar um código simples usando o operador de comparação *Spaceship (nave espacial, <=>)*, que está disponível a partir do PHP 7.0.

- Crie um arquivo em algum diretório do sistema com um nome qualquer (teste.php, por exemplo), e cole o código a baixo:
	`<?php`
		`$var1 = var_dump(10 <=> 10);`
		`echo $var1; //  0`
		`$var2 = var_dump(10 <=> 5);`
		`echo $var2; //  1`
		`$var3 = var_dump(5 <=> 10);`
		`echo $var3; // -1`
	`?>`
	
- Execute o arquivo com as duas versões do PHP no terminal.
	> php5.6 teste.php
	
	- Ou
	
	> php7.1 teste.php
	
- Versão PHP 5.6. Deverá ocorrer o erro a baixo, pois não há suporte para este operador.
 
	`PHP Parse error:  syntax error, unexpected '>' in /home/sim/Área de Trabalho/teste.php on line 2`

- Versão PHP 7.1. Deverá gerar a seguinte saída:
	`int(0)`
	`int(1)`
	`int(-1)`



--------------------

## Fontes:

https://tecadmin.net/install-php5-on-ubuntu/

https://phpraxis.wordpress.com/2016/05/16/install-php-5-6-or-5-5-in-ubuntu-16-04-lts-xenial-xerus/

http://php.net/manual/pt_BR/language.operators.comparison.php