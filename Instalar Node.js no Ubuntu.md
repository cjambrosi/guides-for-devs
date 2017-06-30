Instalar o Node.js no Ubuntu
===============================================

--------------------

O que é Node.js?
Node.js é uma plataforma para desenvolvimento de aplicações server-side (trabalho no lado do servidor) baseadas em rede utilizando JavaScript e o V8 JavaScript Engine, ou seja, com Node.js podemos criar uma variedade de aplicações Web utilizando apenas código em JavaScript (client-side, trabalha no lado do cliente).

--------------------

Nas distribuições baseadas no Debian (Ubuntu obviamente), é muito comum utilizarmos *apt-get install nome-do-pacote*. Com o Node isso pode ocasionar em problemas de conflito entre os nomes *node* e *node.js* (ao menos até o momento que escrevo esse passo-a-passo), pois o NPM que é o gerenciador de dependêcias ficará perdido e algumas funções não funcionaram.
O recomendado é instalar o **arquivo binário** do Node ou instalar o **NVM primeiro e depois o Node**, que é o que será feito aqui. Assim, se quisermos podemos instalar várias versões do Node e ficar alternando entre elas.

## Instalação

Antes de instalar o NVM, precisamos instalar algumas depêndencias. Abra o terminal e digite o comando a baixo:

	> sudo apt-get update sudo apt-get install build-essential libssl-dev

Agora vamos baixar o script de instalação do repositório oficial e executá-lo.

	> curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.2/install.sh | bash

source ~/.bashrc

Rode o comando a baixo para exibir as várias versõs do Node, pois assim saberemos que está funcionando corretamente.

	> nvm ls-remote

Para instalar o Node, escolha a versão mais recente ou aquela que você preferir:

	> nvm install v8.1.2

Verifique a versão do Node instalado com o comando a baixo:

	> node -v

--------------------

## Testar funcionamento















## Referências

https://nodejs.org/en/

https://tableless.com.br/como-instalar-node-js-no-linux-corretamente-ubuntu-debian-elementary-os/

https://github.com/creationix/nvm

https://tableless.com.br/o-que-nodejs-primeiros-passos-com-node-js/