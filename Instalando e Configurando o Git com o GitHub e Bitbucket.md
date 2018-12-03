Instalando e Configurando o Git com o GitHub e Bitbucket
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

1. Antes de tudo, atualize os repositórios e gatilhos do Ubuntu:

	> sudo apt-get update

	> sudo apt-get upgrade

2. A partir do repósitorio do Ubuntu

	- Digite o comando a baixo *(recomendado)*:

		> sudo apt-get install git

		- ou

		> sudo apt-get install git-all

	- Instalar visualizador grágico do histórico de todos os commits feitos:

		> sudo apt-get install gitk

--------------------

## Configurando o Git

1. Se preferir, instale o utilitário de linha de comando **xclip**:

	> sudo apt-get install xclip

2. Configurando nossa identidade:

	> git config --global user.name "Seu Nome"

	> git config --global user.email seu_email@example.com

3. Habilitar cor nas mensagens de saídas do Git para uma melhor análise:

	> git config --global color.ui true

4. Para corrigir formatação e erros de espaços em branco de um colaborador que utiliza Windows. Pois o Windows usa tanto o carácter **carriage-return** e um carácter **linefeed** para novas linhas em seus arquivos, enquanto os sistemas Mac e Linux usam apenas o carácter **linefeed**:

	> git config --global core.autocrlf input

5. Opcionalemnte, podemos configurar um editor de texto padrão para ser usado quando o Git precisar que você escreva uma menssagem. 

	- Opcinalmente utilizo o Visual Studio Code. Para configurá-lo corretamente, siga os comandos a baixo:

		> git config --global core.editor "code --wait"

		- Abra o arquivo de configuração global do Git e cole os comandos a baixo:
		
		> git config --global -e

		`[merge]`</br>
			&nbsp;&nbsp;&nbsp;&nbsp;`tool = vscode`</br>
		`[mergetool "vscode"]`</br>
			&nbsp;&nbsp;&nbsp;&nbsp;`cmd = code --wait $MERGED`</br>
		`[diff]`</br>
			&nbsp;&nbsp;&nbsp;&nbsp;`tool = vscode`</br>
		`[difftool "vscode"]`</br>
			&nbsp;&nbsp;&nbsp;&nbsp;`cmd = code --wait --diff $LOCAL $REMOTE`</br>

		- Exemplo:

			![](https://github.com/CristianAmbrosi/tutoriais/blob/master/images/git-vscode-config.png)

	- Por padrão, o Git utiliza o editor do sistema, geralmente o VI ou VIM:

		> git config --global core.editor vi

6. Verificar as configurações feitas até o momento:

	> git config --list

7. Gerando a Chave SSH (Protocolo - Secure Shell)

	- Primeiro, você deve checar para ter certeza que você ainda não possui uma chave SSH. Por padrão, as chaves SSH de um usuário são armazenadas no diretório **~/.ssh**. Exemplo:

		> cd ~/.ssh

		> ls

		authorized_keys2 |  id_rsa 	   | known_hosts
		-----------------|-------------|-------------
		config           |  id_rsa.pub

	- Agora devemos procurar por um par de arquivos chamados, geralmente, de **id_rsa** ou **id_dsa**. O arquivo **.pub** é a sua chave pública, e o outro arquivo é a sua chave privada. 
  
	- Se você não possui esses arquivos (ou não possui nem mesmo o diretório .ssh), você pode criá-los executando um comando chamado **ssh-keygen**, que é fornecido com o pacote SSH em sistemas Linux/Mac. Exemplo:

		> ssh-keygen -C "seu_email@example.com"

		- O texto que está em **" "** é opcional, pois assim podemos ter um comentário na chave SSH para lembrarmos o motivo dessa chave ou simplemente pode ser o seu e-Mail. Se preferir pode criar a chave sem cometário, usando somente o comando:

			> ssh-keygen

		- Gerando o par de chave SSH pública/privada.

			`Generating public/private rsa key pair.`

		- Será perguntado qual o caminho completo e o nome do arquivo que conterá a chave. Pressionar **ENTER** para manter o padrão ou passe o caminho que preferir.

			`Enter file in which to save the key (/home/user/.ssh/id_rsa):`

		- Será perguntado para criarmos uma senha para a chave privada. **Essa senha é muito importante, pois se você perder não será possível recuperá-la, é preciso criar uma chave nova**. 
		Insira uma senha para a chave SSH e pressione **ENTER**. Ou somente pressione **ENTER** para não utilizar uma senha.

			`Enter passphrase (empty for no passphrase):`

		- Será perguntado para repetirmos a senha escolhida. Digite a senha novamente para confirmar e pressione **ENTER**.

			`Enter same passphrase again:`

		- Criada a chave SSH, a saída final será algo semelhante a isso:

			`Your identification has been saved in /home/user/.ssh/id_rsa.`</br>
			`Your public key has been saved in /home/user/.ssh/id_rsa.pub.`</br>
			`The key fingerprint is:`</br>
			`43:c5:5b:5f:b1:f1:50:43:ad:20:a6:92:6a:1f:9a:3a seu_email@example.com`

		- Para verificar se realmente foram criados os dois arquivos digite o comando a baixo no caminho escolhido. Deverá listar os dois arquivos contendo a chave pública e privada.

			>  ls ~/.ssh

			`id_rsa  id_rsa.pub`

--------------------

## Configurando o GitHub

1. Inserir no GitHub a chave SSH criada do Git

	- Se você instalou o programa **xclip** digite o comando a baixo para copiar o conteúdo do arquivo que contem a chave pública. Se não, abra em um editor de texto e copie o conteúdo.

		> xclip -sel clip ~/.ssh/id_rsa.pub

	- Copiado o conteúdo do arquivo, acesse a sua conta no site do <i class="icon-provider-github"></i> **[GitHub](https://github.com/)** e vá nas configurações da sua conta.

	- Nos menus do lado esquerdo da tela, escolha a opção **SSH and GPG keys**.

	- Para adicionar a chave SSH criada, escolha a opção **New SSH key**.

	- Na opção **Title**, escolha um título para a chave, para que possamos identificá-la.

	- E na opção **Key**, cole o conteúdo da chave pública copiado anteriormente.

	- Para finalizar, clique em **Add SSH Key**, para adicionar a chave pública.

2. Testar a conexão da máquina com o GitHub

	- Após configurar a chave, devemos testar a conexão com o GitHub usando o comando a baixo:

		> ssh -T git@github.com

		- **Importante!** Se você estivar em algum lugar que utilize firewall, por exemplo na sua empresa, possivelmente você terá a porta padrão SSH que o Git utiliza bloqueada ou em uso. Para corrigir esse problema, siga o tutorial a baixo:

			- **[Erro de Conexão do Git - Porta 22 Bloqueada](https://github.com/CristianAmbrosi/tutoriais/blob/master/Erro%20de%20Conex%C3%A3o%20-%20Porta%2022%20Bloqueada.md)**

		- **Corrigido, siga esse tutorial normalmente.**

	- Será alertado que a autenticidade não pode ser estabelecida exibindo os dados e se queremos continuar conectados ou não. Exemplo:

	    `The authenticity of host 'github.com (192.30.253.113)' can't be established.`<br>
	    `RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.`<br>
		`Are you sure you want to continue connecting (yes/no)? yes`

	- Digite **"yes"** para continuar conectado.

		`Are you sure you want to continue connecting (yes/no)?` **`yes`**

	- Receberá um alerta dizendo que será adicionado permanentemente a lista de hosts conhecidos, pedindo a senha da chave SSH escolhida anteriormente. Exemplo:

		`Warning: Permanently added the RSA host key for IP address '104.192.143.1' to the list of known hosts.`

	- Será alertado que o usuário está autenticado, mas que o GitHub não permite acesso por um terminal Shell. Isso não é um problema, se chegar nessa mensagem, tudo ocorreu corretamente, a conexão está funcionando.

		`Hi USER You've successfully authenticated, but GitHub does not provide shell access.`

--------------------

## Configurando o Bitbucket

1. Inserir no Bitbucket a chave SSH criada do Git

	- Se você instalou o programa **xclip** digite o comando a baixo para copiar o conteúdo do arquivo que contem a chave pública. Se não, abra em editor de texto e copie o conteúdo.

		> xclip -sel clip ~/.ssh/id_rsa.pub

	- Copiado o conteúdo do arquivo, acesse as configurações da sua conta no site <i class="icon-provider-github"></i> **[Bitbucket](https://bitbucket.org/)**.

	- Na sessão de segurança, acesse o menu **SSH keys**. Clique no botão **Add key** para abrir a janela de inserção.

	- No campo **Label** de um nome para sua chave e no campo **Key** cole a chave copiada anteriormente. Feito isso clique no botão **Add key** para adicioná-la.

2. Testar a conexão da máquina com o Bitbucket

	- Após configurar a chave, devemos testar a conexão com o Bitbucket com o comando a baixo.

		> ssh -T git@bitbucket.org

	-

	- Receberá um alerta dizendo que será adicionado permanentemente a lista de hosts conhecidos, pedindo a senha da chave SSH escolhida anteriormente. Exemplo:

		`Warning: Permanently added the RSA host key for IP address '104.192.143.1' to the list of known hosts.`

	- Também será informado quais contas tem permissão para fazer login com essa chave, e um aviso de que você pode utilizar o Git ou o HG (Mercurial) para se conectar ao Bitbucket, mas que acesso via Shell está desabilitado.

		`logged in as USER.`

		`You can use git or hg to connect to Bitbucket. Shell access is disabled.`

	- Ao chegar nessas mensagens, quer dizer que as configurações ocorreram corretamente e que a conexão está funcionando.

--------------------

## O que foi instalado?!

**libcurl4-gnutls-dev =>** Pacote que fornece os arquivos de desenvolvimento (includes, static library, páginas manuais) que permitem construir softwares que usem libcurl;

**libexpat1-dev =>** Pacote que contém o arquivo de cabeçalho e bibliotecas de desenvolvimento de expat, a biblioteca C para analisar XML. Isso significa que você registrar manipuladores com o analisador antes de iniciar a análise. Esses manipuladores são chamados quando o analisador descobre as estruturas associadas no documento que está sendo analisado;

**gettext =>** Interessante para os autores e mantenedores de outros pacotes ou programas que eles querem ver internacionalizados;

**libz-dev =>** Não encontrado;

**libssl-dev =>** Este pacote é parte da implementação do projeto OpenSSL do SSL e TLS, protocolos de criptografia para comunicação segura através da Internet. Ele contém bibliotecas de desenvolvimento, arquivos de cabeçalhos e manpages para libssl e libcrypto;

**Git =>** Ferramenta de Controle de Versão, criado por Linus Torvalds em 2005;

**gitk =>** Basicamente uma ferramenta visual para o git log, ele aceita aproximadamente todas as opções de filtros que o git log aceita;

**xclip =>** Utilitário de linha de comando. Pode ler dados de padrão ou um arquivo e colocá-lo em uma seleção X (área de transferência) para colar em outras aplicações X. xclip também pode imprimir uma seleção X para a saída padrão, que pode então ser redirecionada para um arquivo ou outro programa.

--------------------

## Referências

https://git-scm.com/book/pt-br/v1

https://try.github.io/

https://confluence.atlassian.com/bitbucket/set-up-an-ssh-key-728138079.html

https://www.youtube.com/watch?v=WVLhm1AMeYE&list=PLInBAd9OZCzzHBJjLFZzRl6DgUmOeG3H0

https://help.github.com/articles/generating-an-ssh-key/

https://www.youtube.com/watch?v=UMhskLXJuq4

https://www.youtube.com/watch?v=iVUnXw64Ez8

https://packages.debian.org/wheezy/libcurl4-gnutls-dev

https://packages.debian.org/jessie/xclip

https://packages.debian.org/wheezy/libexpat1-dev

https://packages.debian.org/jessie/libssl-dev

https://askubuntu.com/questions/765565/how-to-fix-processing-with-runit-and-git-daemon-run
