
Tutorial Firebird SQL - Backup e Restore | (Linha de Comando)
===============================================

--------------------

## Backup

1. No terminal do linux digite:

	> sudo su firebird

2. Digite sua senha do usuário linux. Você vai estar como administrador do Banco de Dados. 
Ex: 

	> firebird@usuario:/home/usuario$

3. Em seguida digite no terminal os seguintes comandos:

	> gbak -g -l -b -v -z /CAMINHO-DO-ARQUIVO/banco.fbd /CAMINHO-DO-BACKUP/banco.fbk -user USUARI_DO_BANCO -pas SENHA_DO_BANCO

--------------------

## Restore

1. No terminal do linux digite:

	> sudo su firebird

2. Digite sua senha do usuário linux. Você vai estar como administrador do Banco de Dados. 
Ex:

	> firebird@usuario:/home/usuario$

3. Em seguida digite no terminal os seguintes comandos:

	> gbak -c -v -z /CAMINHO-DO-BACKUP/banco.fbk /CAMINHO-DO-BACKUP/banco.fbd -user USUARI_DO_BANCO -pas SENHA_DO_BANCO

	- **Obs: Se tiver dúvidas, pode criar um .NEW e depois renomear normalmente para .fbd.**

--------------------

## Lista de comandos utilizados

- **USUARI_DO_BANCO =>** sysdba (Por padrão)

- **SENHA_DO_BANCO =>** masterkey (Por padrão)
	
- **.fbk =>** Extensão do arquivo para backup

- **-g =>** Não realiza o processo de garbage collection durante o processo de backup, porém, é recomendado que você sempre realize o garbage collect, pois o mesmo é responsável por excluir as versões de registro que não são mais necessárias. (NÃO É OBRIGATÓRIO E É RESTRITO AO BACKUP)

- **-l =>** Desativa os índices durante o processo de restauração do banco de dados. (NÃO É OBRIGATÓRIO E É RESTRITO AO BACKUP)

- **-b =>** Gera um backup. (OBRIGATÓRIO PARA O BACKUP)

- **-v =>** Mostra na tela todo o processo que está sendo executado no backup/restore. (NÃO É OBRIGATÓRIO)

- **-z =>** Mostra a versão do gBak. (NÃO É OBRIGATÓRIO)

- **-c =>** Cria um banco de dados a partir de um arquivo de backup já pronto. (OBRIGATÓRIO PARA O RESTORE)

- **Obs:** No Windows é um pouco diferente, ao invés de usar o **'sudo su'** que é do linux, deve-se acessar a pasta de instalação do Firebird pelo CMD, até a pasta **'bin'** e seguir normalmente os passos. 	
Ex: 
	> cd C:\Arquivos de programas\Firebird\Firebird_2_1\bin>

--------------------

## Fonte 
	
https://www.youtube.com/watch?v=NNV5M0nsaF8

http://www.devmedia.com.br/utilizando-o-gbak-do-firebird-para-efetuar-backup-restore/4877
