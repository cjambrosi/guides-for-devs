Instalar Netbeans no Ubuntu
===============================================

--------------------

#### **OBS: Antes de efetuar a instalação, deve-se ter o JAVA e o JDK instalados na máquina.**

--------------------

## Baixando e Executando o instalador:

1. Acessar o site do Netbeans.org, ir na pagina de downloads e baixar a versão que desejar.

	> https://netbeans.org/

2. Abra o terminal. Vá até o diretório onde foi baixado e dê permissão de execução no arquivo **.sh**.
		Ex:
		
	> /Downloads$ chmod 777
	
	- ou 

	> /Downloads$ chmod +x netbeans-8.1-linux.sh

3. Execute o arquivo .sh.
	Ex:

	> /Downloads$	./netbeans-8.1-linux.sh

--------------------

## Instalação:

1. Na primeira janela de instalação você pode optar pelo quê você quer instalar ou não.

2. Siga os passos e aceite os termos do **contrato de licença**.

3. Na janela **"Escolha a pasta de instalação e o JDK(tm)"**:

	- **Instalar os NetBeans IDEs em:** pode deixar o diretório padrão (/home/user/netbeans-8.1) ou alterar se preferir;

	- **JDK(tm) dos NetBeans IDEs:** Se não for encontrado automaticamente e ficar como padrão o diretório **"/usr"** ou outro, deve-se procurar o JDK manualmente (lembrando que ele já deve estar instalado na máquina).
	Normalmente ele está instalado no diretórido **"/usr/lib/jvm/java-8-oracle"**.

4. Na próxima janela você pode optar por *receber / instalar* ou *não* as atualizações para o Netbeans.

5. Finalizar.

--------------------

# Fontes:

https://www.youtube.com/watch?v=74QEhBpzixs
