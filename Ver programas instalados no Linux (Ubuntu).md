
Ver programas instalados no Linux (Ubuntu)
===============================================

--------------------

## Listar todos os programas instalados:										
	
> sudo dpkg --get-selections


## Buscar programas instalados por uma palavra chave:

> sudo dpkg --get-selections | grep php

--------------------

## Breve explicação dos comandos:

- **sudo =>** Obter privilégios de super usuário;

- **dpkg =>** Comando similar ao "apt-get", ele foi criado para instalar pacotes (.deb), uma espécie de complemento do "apt-get". Ele faz o trabalho braçal, mas não é bom em resolver problemas. É o apt-get que cuida das situações mais delicadas.

- **--get-selections =>**

- **| =>** De uma maneira simplória podemos dizer que o pipe nada mais é do que o encadeamento de processos.

- **grep =>** Usa expressões regulares (regex) para realizar as buscas de forma que o nome ou a palavra desejada case com a expressão.

- **php =>** Palavra chave à ser procurada.

--------------------

## Fonte:

https://www.vivaolinux.com.br/dica/O-gerenciador-de-pacotes-dpkg

http://www.hardware.com.br/livros/entendendo-linux/usando-dpkg.html

https://www.vivaolinux.com.br/dica/Usando-o-pipe

https://www.vivaolinux.com.br/artigo/Usando-grep-e-egrep