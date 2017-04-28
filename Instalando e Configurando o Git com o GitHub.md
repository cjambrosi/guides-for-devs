Instalando e Configurando o Git com o GitHub
===============================================

#### O que é uma ferramenta de Controle de Versão?
Resumidamente, é um sistema que registra as mudanças feitas em um arquivo ou um conjunto de arquivos ao longo do tempo de forma que você possa recuperar versões específicas. Pode ser usado com praticamente qualquer tipo de arquivo em um computador. 
Permite além reverter arquivos para um estado anterior, reverter um projeto inteiro para um estado anterior, comparar mudanças feitas ao decorrer do tempo, ver quem foi o último a modificar algo que pode estar causando problemas, quem introduziu um bug e muito mais. Usar um VCS normalmente significa que se você estragou algo ou perdeu arquivos, poderá facilmente reavê-los. Além disso, você pode controlar tudo sem maiores esforços.

#### Exemplos de ferramentas para Controle de Versão.
- SubVersion (SVN);
- Mercurial;
- Microsoft Visual Studio - Team Foundation Server;
- Git;
- CVS.

--------------------

## Instalando

1. Primeiramente, atualizar os repositórios e gatilhos do Ubuntu:

	> sudo apt-get update
	
	> sudo apt-get upgrade

2. Do repósitorio Ubuntu

	- Digitar o comando a baixo *(recomendado)*:

		> sudo apt-get install git 

		- ou

		> sudo apt-get install git-all

	- Instalar visualizador grágico do histórico de todos os commits feitos

		> sudo apt-get install gitk


3. Direto da Fonte
	
	- Para instalar a versão mais recente direto da fonte, é preciso instalar as seguintes bibliotecas que o Git depende (url, zlib, openssl, expat e libiconv):

		> sudo apt-get install libcurl4-gnutls-dev libexpat1-dev gettext \libz-dev libssl-dev

	- Instalada as dependências, ir no site do GitHub onde estão listadas todas as versões do Git, escolher a mais recente ou a que desejar, recomendo instalar a versão mais recente estável. A versão que você vê quando você chega na página do projeto é a ramificação que está sendo trabalhada ativamente. Se você quer a última versão estável, você deve alterar a ramificação para a última tag não **"rc"**.

		> https://github.com/git/git/releases

	- Baixado o pacote, devemos extrair e compilar. Exemplo:

		> tar -zxf git-2.10.1.tar.gz

		> cd git-2.10.1

		> make configure

		> ./configure --prefix=/usr

		> make all doc info

		> sudo make install install-doc install-html install-info

	- Após a conclusão, podemos obter o Git via o próprio Git para atualizações:

		> git clone git://git.kernel.org/pub/scm/git/git.git

--------------------

## Configurando o Git
	
1. Instalar o utilitário de linha de comando **"xclip"**.

	> sudo apt-get install xclip

2. Configurando nossa identidade:

	> git config --global user.name "Seu Nome"

	> git config --global user.email seu_email@example.com

3. Habilitar cor nas mensagens de saídas do Git para uma melhor análise.

	> git config --global color.ui true

4. Para corrigir formatação e erros de espaços em branco de um colaborador que utiliza Windows. Pois o Windows usa tanto o carácter "carriage-return" e um "carácter linefeed" para novas linhas em seus arquivos, enquanto os sistemas Mac e Linux usam apenas o carácter "linefeed".

	> git config --global core.autocrlf input

5. Opcionalemnte, podemos configurar um editor de texto padrão para ser usado quando o Git precisar que você escreva uma menssagem. Por padrão, o Git utiliza o editor do sistema, geralmente o VI ou VIM.

	> git config --global core.editor sublime-text

6. Verificar as configurações feitas até o momento:

	> git config --list

7. Gerando a Chave SSH (Protocolo - Secure Shell)

	1. Primeiro, você deve checar para ter certeza que você ainda não possui uma chave SSH. Por padrão, as chaves SSH de um usuário são armazenadas no diretório **~/.ssh**. Exemplo:

		> cd ~/.ssh
		
		> ls
		
		authorized_keys2 |  id_rsa 	   | known_hosts
		-----------------|-------------|-------------
		config           |  id_rsa.pub

	2. Agora devemos procurar por um par de arquivos chamados "algo" e "algo.pub", onde **algo** é normalmente "id_rsa" ou "id_rsa". O arquivo **.pub** é a sua chave pública, e o outro arquivo é a sua chave privada. 
	Se você não tem estes arquivos (ou não tem nem mesmo o diretório .ssh), você pode criá-los executando um comando chamado **"ssh-keygen"**, que é fornecido com o pacote SSH em sistemas Linux/Mac. Exemplo:

		> ssh-keygen

		- Opcionalmente, podemos adicionar um comentário na nossa chave SSH para lembrarmos o motivo dessa chave ou simplemente o seu e-Mail, ficando assim:

			> ssh-keygen -C "seu_email@example.com"

		- Gerando o par de chave SSH pública/privada.

			`Generating public/private rsa key pair.`

		- Será perguntado qual é o caminho completo e nome do arquivo que conterá a chave. Pressionar **ENTER** para manter o padrão.
			
			`Enter file in which to save the key (/Users/schacon/.ssh/id_rsa):`

		- Será perguntado para criarmos uma senha para a chave privada. **Essa senha é muito importante, pois se você perder não será possível recuperá-la, é preciso criar uma chave nova**. Inserir uma senha para a chave SSH e pressione **ENTER**.

			`Enter passphrase (empty for no passphrase):`

		- Será perguntado para repetirmos a senha escolhida. Digite a senha novamente para confirmar e pressione **ENTER**.

			`Enter same passphrase again:`

		- Criada a chave SSH, ficando semelhante a isso:

			`Your identification has been saved in /Users/schacon/.ssh/id_rsa.`</br>
			`Your public key has been saved in /Users/schacon/.ssh/id_rsa.pub.`</br>
			`The key fingerprint is:`</br>
			`43:c5:5b:5f:b1:f1:50:43:ad:20:a6:92:6a:1f:9a:3a seu_email@example.com`

		- Para verificar se realmente foram criados os dois arquivos digite o comando a baixo, deverá listar os dois arquivos contendo a chave pública e privada.

			>  ls ~/.ssh
			
			`id_rsa  id_rsa.pub`

--------------------

## Configurando o GitHub
			
1. Inserir no GitHub a chave SSH criada no Git

	- Usaremos o programa *"xclip"* instalado anteriormente para copiar o conteúdo do arquivo que contem a chave pública.
	
		> xclip -sel clip ~/.ssh/id_rsa.pub

	- Copiado o conteúdo do arquivo, acessar a sua conta no site do <i class="icon-provider-github"></i> **[GitHub](https://github.com/)**, ir no menu do seu usuário no canto superio direito da tela e clicar na opção **"Settings"**. 

	- Nos menus do lado esquerdo da tela, escolher a opção **"SSH and GPG keys"**.

	- Pada adicionar a chave SSH criada, escolha a opção **"New SSH key"**. 

	- Na opção **"Title"**, escolher um título para a chave, para que possamos identificá-la.

	- E na opção **"Key"**, colar o conteúdo da chave pública copiado anteriormente.

	- Para finalizar, clicar em **"Add SSH Key"**, para adicionar a chave pública.

2. Testar a conexão da máquina com o GitHub

	> ssh -T git@github.com

	- Será alertado que a autenticidade não pode ser estabelecida mostrando os dados e vai pedir se queremos continuar conectados ou não. Exemplo:

	    `The authenticity of host 'github.com (192.30.253.113)' can't be established.`<br>
	    `RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.`<br>
		`Are you sure you want to continue connecting (yes/no)? yes`

	- Digite **"yes"** para continuar conectado.
		
		`Are you sure you want to continue connecting (yes/no)?` **`yes`**
		
	- Receberá um alerta dizendo que será adicionado permanentemente a lista de hosts conhecidos, pedindo a senha da chave SSH Privada escolhida anteriormente. Exemplo:

		`Warning: Permanently added the RSA host key for IP address '192.30.253.112' to the list of known hosts.`

	- Aqui será avisado que o usuário está autenticado, mas que o GitHub não permite acesso por um terminal SSH. Isso não é um problema, se chegar nessa mensagem, tudo ocorreu corretamente, a conexão está funcionando.

		`Hi USER You've successfully authenticated, but GitHub does not provide shell access.`

--------------------

## O que foi instalado?!

**libcurl4-gnutls-dev =>** Pacote que fornece os arquivos de desenvolvimento (includes, static library, páginas manuais) que permitem construir softwares que usem libcurl;

**libexpat1-dev =>** Pacote que contém o arquivo de cabeçalho e bibliotecas de desenvolvimento de expat, a biblioteca C para analisar XML. Isso significa que você registrar manipuladores com o analisador antes de iniciar a análise. Esses manipuladores são chamados quando o analisador descobre as estruturas associadas no documento que está sendo analisado;

**gettext =>** Interessante para os autores e mantenedores de outros pacotes ou programas que eles querem ver internacionalizados;

**libz-dev =>** Não encontrado;

**libssl-dev =>** Este pacote é parte da implementação do projeto OpenSSL do SSL e TLS, protocolos de criptografia para comunicação segura através da Internet. Ele contém bibliotecas de desenvolvimento, arquivos de cabeçalhos e manpages para libssl e libcrypto;

**Git =>** Ferramenta de Controle de Versão, criado por Linus Torvalds em 2005;

**gitk =>** Basicamente uma ferramenta visual para o git log e ele aceita aproximadamente todas as opções de filtros que o git log aceita;

**xclip =>** Utilitário de linha de comando. Pode ler dados de padrão ou um arquivo e colocá-lo em uma seleção X (área de transferência) para colar em outras aplicações X. xclip também pode imprimir uma seleção X para a saída padrão, que pode então ser redirecionada para um arquivo ou outro programa.

--------------------

## Fontes

https://git-scm.com/book/pt-br/v1

https://try.github.io/

https://www.youtube.com/watch?v=WVLhm1AMeYE&list=PLInBAd9OZCzzHBJjLFZzRl6DgUmOeG3H0

https://help.github.com/articles/generating-an-ssh-key/

https://www.youtube.com/watch?v=UMhskLXJuq4

https://www.youtube.com/watch?v=iVUnXw64Ez8

https://packages.debian.org/wheezy/libcurl4-gnutls-dev

https://packages.debian.org/jessie/xclip

https://packages.debian.org/wheezy/libexpat1-dev

https://packages.debian.org/jessie/libssl-dev

https://askubuntu.com/questions/765565/how-to-fix-processing-with-runit-and-git-daemon-run
