Instalar o compilador G++ e Code::Blocks no Ubuntu, para compilar C++
===============================================

--------------------

## Antes de tudo, atualizar os repositórios e gatilhos do Ubuntu:

> sudo apt-get update

> sudo apt-get upgrade

--------------------

## Instalando o G++:

- No momento a distribuição padrão do Ubuntu Linux inclui os compiladores GCC e G++. Para Ter certeza de que você já possui o compilador, digite o seguinte comando:

> g++ --version

`g++ (Ubuntu 5.4.0-6ubuntu1~16.04.4) 5.4.0 20160609
Copyright (C) 2015 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.`
	
- Se não possuir o compilador, abra o terminal e digite os seguintes comandos:
	
	> sudo apt-get install g++	

	`Instalar a última versão estável do compilador do C++`

--------------------

## Instalando e Configurando o Code::Blocks:

1. Para instalar do repositório padrão do Ubuntu, digite no terminal:

	> sudo apt-get install codeblocks

2. Para instalar do repositório ofcial do Code::Blocks, digite no terminal:

	> sudo apt-get install codeblocks
	
3. Abra o Code::Blocks, vá em "Settings> Compiler". Marque as opções:

	- **Enable all common compiler warnings (overrides many other settings)**

	- **Have g++ follow the coming C++0x ISO C++ language standard**

	- **Have g++ follow the C++11 ISO C++ language standard**

4. Selecione a aba **"Toolchain Executables"** e clique no botão **"..."** Navegue até a pasta **"/usr/bin"**, à menos que você tenha instalado em outro diretório que não seja **"/user/bin"**.

5. Nas seguintes opções deixe como especificado a baixo:

	- C Compiler => deve ser **gcc**

	- C++ Compiler => deve ser **g++**
		
	- Linker for dynamic libs => deve ser **g++**

6. Efetuadas as alterações selecione **OK** para salvar e finalizar as configurações.

--------------------

## Desinstalar completamente o Code::Blocks do Ubuntu

>sudo apt-get --purge remove codeblocks*

> sudo apt-get autoremove

> sudo apt-get autoclean

--------------------

## Fontes

http://www.dummies.com/how-to/content/how-to-install-c-codeblocks-in-ubuntu-linux.html

http://www.edivaldobrito.com.br/instalar-ide-codeblocks-no-ubuntu/

http://ubuntuhandbook.org/index.php/2016/05/install-codeblocks-ide-ubuntu-16-04/

https://www.vivaolinux.com.br/topico/C-C++/Diferenca-entre-gcc-e-g++


