<h1 align="center">Instalando e Configurando o Composer no Linux (Ubuntu)</h1>

## Instalar

1. Antes de tudo, atualize os repositórios e o sistema:

	> sudo apt update

	> sudo apt upgrade

2. Precisaremos da biblioteca **"curl"** instalada, para baixarmos o pacote Composer. Digite o comando a baixo para instalar:

	> sudo apt install curl

3. Com o comando a baixo, o Composer é baixado direto da fonte e instalado. Será baixado no **/home**:

	> curl -sS https://getcomposer.org/installer | php

4. Torne-o executável com o comando a baixo:

	> sudo chmod +x composer.phar

5. Vamos mover o arquivo Composer para pasta de executáveis local:

	> sudo mv composer.phar /usr/local/bin/composer


6. Assim será possível executar o Composer de qualquer lugar do computador, sem a necessidade da extensão **".phar"**.

	- Verifica a versão instalada com o comando a baixo:

		> composer --version

## O que foi instalado?!

 - **[Composer](https://getcomposer.org/) =>** É uma ferramenta para gerenciamento de dependências para o PHP que vem ganhando espaço e se tornando cada vez mais indispensável. Com algumas poucas linhas de configurações você define todas as bibliotecas de terceiros ou mesmo suas que deseja/precisa utilizar em seu projeto, o composer encarrega-se de baixá-las e criar um autoloader deixando-as prontas para uso;

 - **chmod +x =>** Comando que dá permissão de execução apenas;

 - **curl =>** Uma biblioteca suportada pelo PHP, que permite que você conecte-se e comunique-se com diferentes tipos de servidores usando diferentes tipos de protocolos. *libcurl* atualmente suporta os protocolos http, https, ftp, gopher, telnet, dict, file, e ldap. libcurl também suporta certificados HTTPS, HTTP POST, HTTP PUT, upload via FTP (podendo também ser feito com a extensão ftp do PHP), upload HTTP por formulário, proxies, cookies, e autenticação com usuário e senha.

### Referências

<http://gilbertoalbino.com/instalacao-do-composer-no-ubuntu>

<http://tableless.com.br/composer-para-iniciantes>

<http://php.net/manual/pt_BR/book.curl.php>
