Permissões de um Arquivo ou Diretório no Linux
===============================================

--------------------

1. Abra o terminal do linux, escolha um diretório qualquer e dê o seguinte comando:
	
	>  ls -l
	
- ou

	> ll

	Permissões | Links  | Proprietário | Grupo | Tamanho | Data e Hora   | Nome
	--------------|--------|----------------|--------|------------|------------------|-----------
	drwxr-xr-x  | 2 	   | root 		     | root     | 4096       | Out 19 09:10  | composer/


- **Permissões =>** Tipo do ítem e nível permitido de permissão para Leitura, Escrita e Execução do ítem ou diretório;
- **Links =>** Número de ligações que o ítem possui, no caso do diretório, número de subdiretórios que possui;
- **Proprietário =>** Quem é o dono, quem criou. É o diretório padrão do usuário, o *home*;
- **Grupo =>** Grupo ao qual pertence o ítem ou diretório. Utilizado para dar permissões à outros usuários;
- **Tamanho =>**	Em Bytes;
- **Data e Hora =>** Momento em que foi criado;
- **Nome =>** Nome do ítem ou diretório;
- **Outros =>** Se não é Proprietário do ítem e não está no Grupo do ítem, ele pertence ao conjunto de usuários Outros.

2. O primeiro caractere das Permissões é o **TIPO** do que está sendo mostrando, que pode ser:

	- **d =>** Diretório;
	- **- =>** Arquivo comum de usuário (música, videos, imagens...);
	- **c =>** Arquivo de caractere;
	- **b =>** Arquivo de bloco;
	- **l =>** link (Espécie de atalho no Linux);

3. As permissões são aplicadas em **três** conjuntos da seguinte ordem:

	Proprietário | Grupo | Outros
	-------------- |---------|------------
	rwx			    | r-x	     | r-x

	- **r =>** Read (Permissão de Leitura do arquivo. Ver o conteúdo do diretório);
	- **w =>** Write (Permissão de Escrita do ítem. Alterar o contúdo de um arquivo ou diretório);
	- **x =>** Execution (Permissçao de Execução. Executar um arquivo ou Entrar num diretório);
	- **- =>** Sem permissão.

4. Entendendo as permissões.

	Leitura(**r**) =  4 </br>
	Escrita(**w**) =  2 </br>
	Execução(**x**) = 1

	- Pensaremos nas permissões como sendo bits de **ligados = 1 / desligados = 0**. Convertemos de binário para decimal.

		`rwx = 111 ( 7 | Acesso Total )` </br>
		`r-- = 100 ( 4 | Somente Leitura )` </br>
		`-w- = 010 ( 2 | Somente Escrita )` </br>
		`--x = 001 ( 1 | Somente Execução )` </br>
		`rw- = 110 ( 6 | Somente Leitura e Escrita )` </br>
		`r-x = 101 ( 5 | Somente Leitura e Execução )` </br>
		`-wx = 011 ( 3 | Somente Escrita e Execução )` </br>
		`--- = 000 ( 0 | Todos Acessos Negados )`

		rwx | rw- |  rw-
		-----|------|------
		111 | 110 | 110
		 7    |  6    |   6	
		 - *chmod 766 [arquivo ou diretório]*

- Como existem **3 tipos** de permissões, são **3 bits** disponíveis, então **2³ = 8** combinações possíveis de valores de permissões.

5. Comandos para dar permissão.

	- **chmod =>** Altera as permissões de acessos a arquivos e diretórios no Linux. Há dois modos principais de trabalhar com esse comando, o modo Literal (caracteres) e o modo Octal (mais eficiente e simples).

		- Sintaxe:
	
			> chmod [permissões] [arquivo ou diretório]
	
			- Arquivo: 
		
				> sudo chmod 755 /Downloads/atom-amd64.deb
	
			- Diretório: 
		
				> sudo chmod 755 /var/www/html/
	
			- ![](https://github.com/CristianAmbrosi/tutoriais/blob/master/images/asterisco.png) => Pegar todas as pastas dentro diretório. 
				
				Ex:
				
				> sudo chmod 755 /var/www/html/*
	
			- **.** => Pegar todos os arquivos dentro do diretóio. 
				
				Ex:
				
				> sudo chmod 755 /var/www/html/.
	
			- **.*** => Tudo no mesmo comando. 
				
				Ex:
				
				> sudo chmod 755 /var/www/html/.*
	
			- **-R** => Recursivo. 
				
				Ex:
				
				> sudo chmod 755 /var/www/html/ -R


6. Alterar Proprietário e Grupos de Arquivos e Diretórios no Linux

- **Alterar Proprietário:** chown (change owner)
	
	- Sintaxe:

		> chown [novo_proprietário] [arquivo ou diretório]

		- Arquivo: 
		
			> sudo chown goku teste.php

		- Diretório: 
		
			> sudo chown goku teste

	- **Obs:** O Proprietário já deve existir.

- **Alterar o Grupo: chgrp (change group)**
	
	- Sintaxe:
	
		> chgrp [novo_grupo] [arquivo ou diretório]

		- Arquivo: 
		
			> sudo chgrp goku teste.php

		- Diretório: 
		
			> sudo chgrp goku teste

	- **Obs:** O Grupo já deve existir. 
	  - Como criar um Grupo?

		  > sudo addgroup [nome_grupo]

--------------------

## Fonte

https://www.youtube.com/watch?v=C-X_HmtGqPk

https://www.youtube.com/watch?v=nogVVjeeXLg

https://www.youtube.com/watch?v=_jR8tOl0yqU

https://www.vivaolinux.com.br/dica/Chmod-+-dicas
