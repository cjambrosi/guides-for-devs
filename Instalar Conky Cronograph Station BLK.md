Instalar Conky Cronograph Station BLK 8.0 Modificado no Ubuntu
===============================================

--------------------

- **Este Conky foi modificado a meu gosto, se desejar pode instalar seguindo os mesmos passos a versão mais recente do repositório [*oficial*](https://github.com/drxspace/cronoconky).** 

--------------------

- Primeiramente, atualizar os repositórios e gatilhos do Ubuntu

	> sudo apt-get update

	> sudo apt-get upgrade

- Baixe o arquivo compactado neste link e descompacte-o:
	
	- [**Conky Cronograph Station BLK 8.0 Modificado**](/files/cronoconky-blk-8.0-modificado.tar.gz?raw=true)

- Descompactado o arquivo, entre na pasta pelo terminal e execute o arquivo *debians_install.sh*.

	> ./debians_install.sh

- Siga os passos a baixo:

	- `Do you want to continue? [Y/n]:` **`Y`**
	</br>`digite sua senha de super usuário`

	- `Do you want to continue? [Y/n]:` **`Y`**

	- `Do you want to install the hddtemp service as daemon? [Y/n]:` **`n`**

	- `Celsius or Fahrenheit? [C/f]:` **`(Opcional)`**

	- `Do you want to add this conky to the Startup Applications list? [Y/n]:` **`Y`**

- Acesse o site  [Yahoo Weather](https://www.yahoo.com/news/weather). Onde mostra a temperatura, altere para a que você escolheu na instalação *C (Celsius)* ou *F (Fahrenheit)* e procure pela cidade desejada utiliando o CEP. Ao selecionar a cidade, no final da URL copie o código da cidade.

	- Exemplo: `https://www.yahoo.com/news/weather/brazil/erechim/erechim-`**`12827913`**

- Copiado o código, vá no diretório onde foi instalado o Conky, por padrão está em `/opt/cronograph_blk/`. Dentro do diretório vá em `yahooweather` e abra o arquivo chamado `forecasts.sh`. Na linha 50, altere a variável `WOEID='12827913'` pelo código obtido da sua cidade e salve.

	> cd /opt/cronograph_blk/yahooweather/

	> sudo nano forecasts.sh

	![](https://github.com/CristianAmbrosi/tutoriais/blob/master/images/conky-forecasts.png)

- Volte uma pasta e execute o arquivo *start_crono.sh* para reiniciar o Conky com a modificação feita.

	> ./start_crono.sh

--------------------

- Desinstalar o Conky Cronograph BLK

	- Abra o terminal e digite o seguinte comando:

		> sudo apt-get --purge remove conky*

	- Feito isso, vá até a pasta onde foi instalado o Conky e siga os passos a baixo:

		> cd /opt/

		> ls -l

		> sudo rm -rf cronograph_blk/ 

--------------------

- **O que é o serviço hddtemp?**</br>
O aplicativo *hddtemp* serve para monitorar a temperatura do seu HD, através da leitura dos dados do S.M.A.R.T. O propósito do S.M.A.R.T é antecipar falhas no dispositivo de armazenamento, o que permite ao usuário se prevenir de perda de dados.
O *hddtemp* busca informações sobre a temperatura do disco rígido nos dados fornecidos pelo S.M.A.R.T — desde que o dispositivo tenha suporte ao recurso.
O aplicativo pode ser executado como um comando simples ou como daemon (controla um serviço provido pelo seu sistema), para obter informações de todos os servidores.

--------------------

- Fontes:

	http://www.upubuntu.com/2012/06/conky-cronograph-station-elegant.html

	https://www.youtube.com/watch?v=D3qDJRNXfJU

	https://elias.praciano.com/2014/03/monitore-a-temperatura-do-seu-hd-com-hddtemp/

	https://www.cyberciti.biz/tips/howto-monitor-hard-drive-temperature.html

	http://manpages.ubuntu.com/manpages/zesty/man8/hddtemp.8.html

	https://packages.debian.org/search?keywords=hddtemp

	https://www.vivaolinux.com.br/artigo/Entendendo-um-pouco-sobre-os-daemons

	https://askubuntu.com/questions/26542/what-is-a-daemon
