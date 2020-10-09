<h1 align="center">Instalando e Configurando o Sublime Text 3 no Ubuntu</h1>

## Antes de tudo, atualize os repositórios e o sistema:

> sudo apt-get update && apt-get upgrade


## Instalando

1. Primeira forma de instalação. Através do repositório oficial do Sublime Text.

	- Instale a chave GPG:

		> wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -

	- Adicione a fonte de onde será baixado e instalado a versão estável mais atual do Sublime Text:

		> echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list

	- Atualize as fontes e instale:

		> sudo apt-get update

		> sudo apt-get install sublime-text

	- **Obs:** Algumas vezes instalando desta forma, não é possível escolher o Sublime Text como editor de texto padrão do sistema. [Clique aqui para corrigir esse problema](#sublime-text-como-editor-de-texto-padrão-do-sistema).

2. Segunda forma de instalação. Através do PPA criado pela esquipe **[WebUp8](http://www.webupd8.org/)**. Apesar de não ser um repositório oficial, é muito confiável. Único porém, é que terá um pequeno atraso para a versão mais recente lançada do Sublime Text.

	- Adicione o repositório a baixo e atualize-o:

		> sudo add-apt-repository ppa:webupd8team/sublime-text-3

		> sudo apt-get update

	- Para instalar, use o comando a baixo:

		> sudo apt-get install sublime-text-installer

## Instalar Plugins/Pacotes no Sublime Text

1. Para instalar plugins no Sublime Text, é preciso ter instalado o plugin **Package Control**. Esse plugin é responsável por gerenciar todos os outros plugins, ou seja, é com ele que você vai instalar, desinstalar e configurar plugins.

	- Para instalar o plugin, acesse o link a baixo e copie o código referente ao **Sublime Text 3**:

		> https://packagecontrol.io/installation#st3

	- No Sublime Text, abra o console indo na opção de menu **View** > **Show Console**. Cole o código copiado no console e pressione Enter. Após terminada a instalação, reinicie o Sublime Text.

2. Instalado o Package Constrol, vamos utilizá-lo para instalar outros plugins. O Sublime Text possui uma infinidade de plugins.

	- Acesse o Package Control pelo atalho **Ctrl**+**Shift**+**P**. Para instalar um plugin, digite o comando a baixo seguido do nome do plugin:

		> install package Color Highlighter

		- Você também pode apenas digitar *install* e pressionar Enter, que irá aparecer uma lista de plugins para você instalar.

	- Se quiser remover um plugin, digite o comando a baixo seguido do nome do plugin:

		> remove package Color Highlighter

	- Logo a baixo, há uma [lista com alguns bons plugins](#lista-de-alguns-plugins-para-usar-no-sublime-text) para serem instalados.

## Configurações do Usuário

- Vá em **Preferences** e clique em **Settings**. Será aberto dois arquivos JSON, o da esquerda é o arquivo **Default**, onde há todas as opções com suas configurações padrões. O da direita é o arquivo **User**, onde é possível modificar as opções padrões para o gosto do usuário.

- No arquivo **User** (a direita), dentro das chaves **{}**, adicione as variáveis que deseja alterar os valores padrões e salve. Abaixo, algumas variáveis alteradas de exemplo:

	`{` <br />
	&nbsp;&nbsp;&nbsp;&nbsp;`// Usa a fonte Menlo como padrão.`<br />
	&nbsp;&nbsp;&nbsp;&nbsp;`"font_face": "Menlo",`<br />
	&nbsp;&nbsp;&nbsp;&nbsp;`// Tamanho de fonte 10 como padrão.`<br />
	&nbsp;&nbsp;&nbsp;&nbsp;`"font_size": 10,`<br />
	&nbsp;&nbsp;&nbsp;&nbsp;` // Define a indentação com tamanho 2.`<br />
	&nbsp;&nbsp;&nbsp;&nbsp;`"tab_size": 2,`<br />
	&nbsp;&nbsp;&nbsp;&nbsp;`// Altera a tecla que faz o autocomplete para tab.`<br />
	&nbsp;&nbsp;&nbsp;&nbsp;`"auto_complete_commit_on_tab": true,`<br />
	&nbsp;&nbsp;&nbsp;&nbsp;`// Adiciona linha em branco ao final do arquivo.`<br />
	&nbsp;&nbsp;&nbsp;&nbsp;`"ensure_newline_at_eof_on_save": true,`<br />
	&nbsp;&nbsp;&nbsp;&nbsp;`// Destaca a linha com o cursor.`<br />
	&nbsp;&nbsp;&nbsp;&nbsp;`"highlight_line": true,`<br />
	&nbsp;&nbsp;&nbsp;&nbsp;`// Marca as abas modificadas de modo diferente.`<br />
	&nbsp;&nbsp;&nbsp;&nbsp;`"highlight_modified_tabs": true,`<br />
	&nbsp;&nbsp;&nbsp;&nbsp;`// Exibe o caminho completo do arquivo que está sendo editado no rodapé.`<br />
	&nbsp;&nbsp;&nbsp;&nbsp;`"show_full_path": true,`<br />
	&nbsp;&nbsp;&nbsp;&nbsp;`// Remove whitespaces quando o arquivo é salvo.`<br />
	&nbsp;&nbsp;&nbsp;&nbsp;`"trim_trailing_white_space_on_save": true,`<br />
	&nbsp;&nbsp;&nbsp;&nbsp;`// Salva o arquivo automaticamente ao mudar para outro arquivo.`<br />
	&nbsp;&nbsp;&nbsp;&nbsp;`"save_on_focus_lost": true,`<br />
	&nbsp;&nbsp;&nbsp;&nbsp;`// Deixa os diretórios em negrito na sidebar.`<br />
	&nbsp;&nbsp;&nbsp;&nbsp;`"bold_folder_labels": true`<br />
	`}`<br />

## Sublime Text como editor de texto padrão do sistema

- Acesse o seguinte diretório:

	> cd ~/.local/share/applications/

- Deve existir um arquivo chamado **sublime_text.desktop** ou semelhante (se não existir, crie-o). Abra o arquivo com permissão de super usuário:

	> sudo nano sublime_text.desktop

- Na linha **Exec=/opt/sublime_text/sublime_text** adicione o atributo **%F**, assim como na imagem a baixo:

	![](https://github.com/CristianAmbrosi/tutoriais/blob/master/images/st-editor-padrao.png)

- Salve o arquivo e verifique nas opções se já é possível escolher o Sublime Text como editor de texto padrão para seus arquivos.

## Lista de alguns plugins para usar no Sublime Text

- [EMMET](https://packagecontrol.io/packages/Emmet)

- [Color Highlighter](https://github.com/Monnoroch/ColorHighlighter)

- [CSS3](https://github.com/y0ssar1an/CSS3)

- [DocBlockr](https://packagecontrol.io/packages/DocBlockr)

- [PHPCS](https://packagecontrol.io/packages/Phpcs)

- [PHP Companion](https://packagecontrol.io/packages/PHP%20Companion)

- [Laravel 5 Artisan](https://packagecontrol.io/packages/Laravel%205%20Artisan)

- [jQuery](https://packagecontrol.io/packages/jQuery)

- [AngularJS](https://packagecontrol.io/packages/AngularJS)

- [Sub­lime­CodeIn­tel](https://github.com/SublimeCodeIntel/SublimeCodeIntel)

- [Side­BarEn­hance­ments](https://packagecontrol.io/packages/SideBarEnhancements)

- [AutoFileName](https://packagecontrol.io/packages/AutoFileName)

## Referências

- Instalação e configuração:

	<https://www.sublimetext.com/docs/3/linux_repositories.html>

	<http://www.diolinux.com.br/2013/07/omo-instalar-o-sublime-text-3-no-via-ppa.html>

	<https://askubuntu.com/questions/396938/how-do-i-make-sublime-text-3-the-default-text-editor>

	<https://askubuntu.com/questions/172698/how-do-i-install-sublime-text-2-3>

	<https://ubuntuforums.org/showthread.php?t=794255>

	<http://sublimetextdicas.com.br>

- Plugins/Pacotes:

	<https://packagecontrol.io/installation>

	<http://sublimetextdicas.com.br/11-plugins-para-php-no-sublime-text>

	<https://tableless.com.br/7-plugins-sublime-text-que-voce-deveria-conhecer>

	<https://medium.com/@juniorb2s/melhores-plugins-sublime-para-php-4b011aa02cdf>

	<https://willianjusten.com.br/meus-plugins-favoritos-do-sublime-text>

	<https://medium.com/@MariaSpr/sublime-text-3-essential-packages-2596133aead9>

	<https://umdevweb.wordpress.com/2015/10/04/instalando-o-sublime-text-3-e-configurando-plugins-part-2>

	<http://aslanbakan.com/en/blog/33-essential-sublime-text-plugins-for-all-developers>

	<http://www.devmedia.com.br/sublime-text-ide-introducao-a-melhor-ide-para-desenvolvimento/34117>

	<https://tableless.com.br/sublime-text-2-meu-novo-editor>

	<https://nandovieira.com.br/configurando-o-sublime-text-2>

	<https://webdesign.tutsplus.com/pt/articles/simple-visual-enhancements-for-better-coding-in-sublime-text--webdesign-18052>
