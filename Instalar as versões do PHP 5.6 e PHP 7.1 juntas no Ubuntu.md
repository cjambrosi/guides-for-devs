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
		`Copyright (c) 1997-2016 The PHP Group`</br>
		`Zend Engine v2.6.0, Copyright (c) 1998-2016 Zend Technologies`</br>
		    `with Zend OPcache v7.0.6-dev, Copyright (c) 1999-2016, by Zend Technologies`</br>

- Instalando o PHP 7.1

	> sudo apt-get install php7.1 php7.1-cli php7.1-intl php7.1-mcrypt php7.1-opcache php7.1-readline libapache2-mod-php7.1 php7.1-mbstring php7.1-json php7.1-curl php-imagick php7.1-mysql phpmyadmin
	
	- Verificar a versão instalada:
		
		> php -v
		
	- Ou:
	
		> php --version

	- Exemplo de saída:

		`PHP 7.1.5-1+deb.sury.org~xenial+1 (cli) (built: Apr 11 2017 22:12:32) ( NTS )`</br>
		`Copyright (c) 1997-2017 The PHP Group`</br>
		`Zend Engine v3.1.0, Copyright (c) 1998-2017 Zend Technologies`</br>
		    `with Zend OPcache v7.1.5-1+deb.sury.org~xenial+1, Copyright (c) 1999-2017, by Zend Technologies`</br>

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

		`PHP 5.6.30-10+deb.sury.org~xenial+2 (cli)`</br>
		`Copyright (c) 1997-2016 The PHP Group`</br>
		`Zend Engine v2.6.0, Copyright (c) 1998-2016 Zend Technologies`</br>
		    `with Zend OPcache v7.0.6-dev, Copyright (c) 1999-2016, by Zend Technologies`</br>

- Instalando o PHP 7.1

	> sudo apt-get install php7.1 php7.1-cli php7.1-intl php7.1-mcrypt php7.1-opcache php7.1-readline libapache2-mod-php7.1 php7.1-mbstring php7.1-json php7.1-curl php-imagick php7.1-pgsql

	- Verificar a versão instalada:
		
		> php -v
		
	- Ou:
	
		> php --version

	- Exemplo de saída:

		`PHP 7.1.5-1+deb.sury.org~xenial+1 (cli) (built: Apr 11 2017 22:12:32) ( NTS )`</br>
		`Copyright (c) 1997-2017 The PHP Group`</br>
		`Zend Engine v3.1.0, Copyright (c) 1998-2017 Zend Technologies`</br>
		    `with Zend OPcache v7.1.5-1+deb.sury.org~xenial+1, Copyright (c) 1999-2017, by Zend Technologies`</br>

--------------------

## Alternando entre as duas versões instaladas

- Se estiver na versão do **PHP 5.6** e quiser usar a versão do **PHP 7.1**, digite o comando a baixo:

	> sudo a2dismod php5.6; sudo a2enmod php7.1; sudo service apache2 restart | sudo update-alternatives --set php /usr/bin/php7.1

	- Ou:

	> sudo a2dismod php5.6; sudo a2enmod php7.1; sudo service apache2 restart; echo 2 | sudo update-alternatives --config php

- Se estiver na versão do **PHP 7.1** e quiser usar a versão do **PHP 5.6**, digite os comandos na seguinte ordem:

	> sudo a2dismod php7.1; sudo a2enmod php5.6; sudo service apache2 restart | sudo update-alternatives --set php /usr/bin/php5.6

	- Ou:

	> sudo a2dismod php7.1; sudo a2enmod php5.6; sudo service apache2 restart; echo 1 | sudo update-alternatives --config php

--------------------

## Testar as duas versões instaladas
Para testar se a versão do PHP 7.1 está funcionando junto a do PHP 5.6, podemos utilizar um código simples usando o operador de comparação *Spaceship (nave espacial, <=>)*, que está disponível a partir do PHP 7.0.

- Crie um arquivo em algum diretório do sistema com um nome qualquer (teste.php, por exemplo), e cole o código a baixo:
	</br>`<?php`</br>
		`$var1 = var_dump(10 <=> 10);`</br>
		`echo $var1; //  0`</br>
		`$var2 = var_dump(10 <=> 5);`</br>
		`echo $var2; //  1`</br>
		`$var3 = var_dump(5 <=> 10);`</br>
		`echo $var3; // -1`</br>
	`?>`</br>
	
- Execute o arquivo com as duas versões do PHP no terminal.
	> php5.6 teste.php
	
- Ou:
	
	> php7.1 teste.php
	
- Versão PHP 5.6 -> Deverá ocorrer o erro a baixo, pois não há suporte para este operador.
 
	`PHP Parse error:  syntax error, unexpected '>' in /home/sim/Área de Trabalho/teste.php on line 2`

- Versão PHP 7.1 -> Deverá gerar a seguinte saída:
	</br>`int(0)`</br>
	`int(1)`</br>
	`int(-1)`</br>

--------------------

### (*Opcional*) Podemos criar um par de *Alias* para não termos que digitar todo aquele comando enorme

- Para criá-los, é preciso modidificar o arquivo **.bashrc** que se encontra em **/home/USER/.bashrc** (se não existir o arquivo, crie-o). Abra o arquivo com privilégios de super usuário no editor de texto que preferir.

	> sudo nano ~/.bashrc

- Inclua os aliases no arquivo, de preferência junto aos outros aliases existentes.

	> alias phpV5='sudo a2dismod php7.1; sudo a2enmod php5.6; sudo service apache2 restart | sudo update-alternatives --set php /usr/bin/php5.6'

	> alias phpV7='sudo a2dismod php5.6; sudo a2enmod php7.1; sudo service apache2 restart | sudo update-alternatives --set php /usr/bin/php7.1'

- Ou:

	> alias phpV5='sudo a2dismod php7.1; sudo a2enmod php5.6; sudo service apache2 restart; echo 1 | sudo update-alternatives --config php'

	> alias phpV7='sudo a2dismod php5.6; sudo a2enmod php7.1; sudo service apache2 restart; echo 2 | sudo update-alternatives --config php'

	- Exemplo:

		![](https://github.com/CristianAmbrosi/tutoriais/blob/master/images/alias-php-bashrc.png)

- Por fim, para gravar definitivamente os aliases e ser possível executá-los, digite o comando o baixo:

	> source ~/.bashrc

--------------------

## Fontes:

https://tecadmin.net/install-php5-on-ubuntu/

https://phpraxis.wordpress.com/2016/05/16/install-php-5-6-or-5-5-in-ubuntu-16-04-lts-xenial-xerus/

http://php.net/manual/pt_BR/language.operators.comparison.php

https://www.linuxdescomplicado.com.br/2015/06/criar-comandos-usando-alias.html

http://sejalivre.org/como-usar-aliases-para-personalizar-comandos-no-ubuntu/