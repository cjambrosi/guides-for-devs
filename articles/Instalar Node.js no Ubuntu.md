Instalar o Node.js no Ubuntu
===============================================

--------------------

#### O que é o Node.js?<br/>
Node.js é uma plataforma para desenvolvimento de aplicações server-side (que trabalha no lado do servidor) baseadas em rede utilizando JavaScript e o V8 JavaScript Engine, ou seja, com Node.js podemos criar uma variedade de aplicações Web utilizando apenas código em JavaScript (client-side, que trabalha no lado do cliente).

- Nas distribuições baseadas no Debian (Ubuntu obviamente), é muito comum utilizarmos *apt-get install nome-do-pacote*. Com o Node isso pode ocasionar em problemas de conflito entre os nomes *node* e *node.js* (ao menos até o momento que escrevo esse passo-a-passo), pois o NPM que é o gerenciador de dependêcias ficará perdido e algumas funções não funcionaram.
- O recomendado é instalar o **arquivo binário** do Node ou instalar o **NVM primeiro e depois o Node**, que é o que será feito aqui. Assim, se quisermos podemos instalar várias versões do Node e ficar alternando entre elas.

--------------------

## Instalação

1. Antes de tudo, atualize os repositórios e o sistema:

	> sudo apt-get update

	> sudo apt-get upgrade

2. Antes de instalar o NVM, precisamos instalar algumas depêndencias. Abra o terminal e digite o comando a baixo:

	> sudo apt-get install build-essential libssl-dev

3. Agora vamos baixar o script de instalação/atualização do NVM, a partir do repositório oficial e executá-lo com o comando a baixo.

	> curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.34.0/install.sh | bash

	- O número da versão **(v0.33.2)** pode mudar com o tempo, então acesse o [**repositório oficial**](https://github.com/creationix/nvm) para procurar a versão mais recente.

4. Para o terminal reconhecer as configurações feitas, execute o comando a baixo ou feche e abra-o novamente.

	> source ~/.bashrc

5. Rode o comando a baixo para exibir as várias versões do Node, pois assim saberemos que o NVM está funcionando corretamente e veremos qual/quais versões iremos instalar.

	> nvm ls-remote

6. Para instalar o Node, escolha a versão mais recente ou aquela que você preferir:

	> nvm install v8.1.2

7. Verifique a versão do Node instalado com o comando a baixo:

	> node -v

--------------------

## Testar funcionamento

--------------------

## Referências

https://nodejs.org/en/

https://tableless.com.br/como-instalar-node-js-no-linux-corretamente-ubuntu-debian-elementary-os/

https://github.com/creationix/nvm

https://tableless.com.br/o-que-nodejs-primeiros-passos-com-node-js/
