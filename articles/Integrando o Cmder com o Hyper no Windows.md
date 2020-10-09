
<div align="center">
  <img width="250px" src="https://user-images.githubusercontent.com/9125404/90842591-13507300-e336-11ea-8a08-c5453c3becbf.png" alt="Hyper Cmder Fusion" title="Hyper Cmder Fusion" />
</div>

<h1 align="center">Hyper Cmder:<br />Integrando o Cmder com o Hyper no Windows</h1>

O [Hyper](https://hyper.is) é uma interface de linha de comando amigável e altamente customizável para terminais, baseado em Electron. Com ele, é possível integrar terminais, customizar a interface e instalar plugins para auxiliar e melhorar a experiência de usabilidade.

O [Cmder](https://cmder.net) (Commander), por sí só é uma das melhores opções de interface de linha de comando no momento. Desenvolvido com a finalidade de melhorar a experiência de uso de terminais no Windows, traz com sigo vários recursos e utilitários. Como os comandos do Linux, integração com o Git, customizações do layout e atalhos, entre outros.

Combinar essas duas ferramentas poderosas, pode-se obter uma ótima produtividade e experiência com relação a interfaces de linha de comando. Essa combinação é chama de *Hyper Cmder*, como é possível conferir em [*Seamless Hyper integration*](https://github.com/cmderdev/cmder/wiki/Seamless-Hyper-integration).

## Instalação

Como dependência, é necessário ter o Node.js instalado na máquina para a instalação de plugins no Hyper. Caso não possua, acesse o [site](https://nodejs.org/en) e baixe a versão mais estável.

### Cmder

Acesse o site do [Cmder](https://cmder.net) e escolha entre as duas opções de download.

A opção *Mini* possui somente o terminal Cmder e nada mais. Já a versão, *Full* possui o Git para Windows e mais alguns complementos, caso já tenha o Git instalado, não há problema de baixá-la também.

O Cmder **não possui um instalador**, então só é preciso descompactar o arquivo baixado e executar o **Cmder.exe**. Porém, deixá-lo em diretórios como "Downloads" ou "Documentos", não é o mais apropriado. Também como não se trata de uma instalação convencional, não é recomendado mover para "Arquivos de Programas" (*Program Files*).

O mais apropriado é movê-lo para o **C:\\**, e renomear a pasta para **cmder**. Ficando o caminho desta forma: `C:\cmder\`.

- Como questão de organização, pode-se criar outro diretório em **C:\\**. Por exemplo **Tools**, onde seriam colocados todos os programas que não possuem a forma convencional de instalação.

Movido para o diretório correto, acesse as "Variáveis de Ambiente" do Windows e em "Variáveis do sistema", crie uma variável chamada **CMDER_ROOT** e insira o caminho do diretório do Cmder. Por exemplo: `C:\cmder`.

Ainda em "Variáveis de Ambiente" e "Variáveis do sistema", acesse a variável "Path" e insira também o caminho do diretório onde está o Cmder.

Por fim, crie um atalho do executável **Cmder.exe** para a sua "Àrea de trabalho".

Para tornar o Cmder como terminal padrão do VSCode, clique [aqui](#cmder-como-terminal-padrão-do-vscode).

Se tiver interesse em incluir o Cmder no menu de contexto (*"Open Cmder Here"*), clique [aqui](#cmder-no-menu-de-contexto).

### Hyper

Acesse o site do [Hyper](https://hyper.is/#installation) na página com as opções de downloads. Baixe o instalador na sua versão estável.



## Configuração

## Desinstalação

## Cmder como terminal padrão do VSCode

Para torná-lo o terminal padrão do VSCode, é preciso ter o diretório do Cmder incluído nas variáveis de ambeinte.

## Cmder no Menu de Contexto

*"Open Cmder Here"*.

Para incluir o Cmder no menu de contexto do Windows, é preciso ter o diretório do Cmder incluído nas variáveis de ambiente.
