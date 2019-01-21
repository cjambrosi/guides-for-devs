Erro de Conexão do Git - Porta 22 Bloqueada
===============================================

--------------------

- Na maioria das vezes optamos por utilizar conexão SSH para clonar repositórios, ao invés de usar a clonagem por [HTTPS](https://help.github.com/articles/caching-your-github-password-in-git/). Mas alguns firewalls e a maioria dos servidores Proxy podem interferir na conexão, bloqueando a porta utilizada, por exemplo:

    ![](https://github.com/CristianAmbrosi/tutoriais/blob/master/images/error-port22-git.png)

- Para resolver o problema, alteramos a porta padrão que o Git utiliza, especificando para a porta 443 do servidor HTTPS.

--------------------

## Testando se a correção será possível

- Antes de tentar corrigir o problema, vamos testar se alterando a porta do servidor HTTPS (443) será possível fazer conexão. Para isso, use o comando a baixo:

    - GitHub:

        > ssh -T -p 443 git@ssh.github.com

    - Bitbucket

        > ssh -T -p 443 git@bitbucket.org

    - GitLab

        > ssh -T -p 443 git@gitlab.com

- Se a resposta for algo semelhante a isso, quer dizer que é possível fazer conexão SSH alterando a porta do servidor HTTPS.

    `Hi username! You've successfully authenticated, but GitHub does not provide shell access.`

--------------------

## Correção para o GitHub

1. Abra o arquivo de configuração do Git com o comando a baixo, utilizando um editor de texto (geralmente está nesse caminho):

    > code ~/.ssh/config

2. Adicione o código a baixo no arquivo:

    `Host github.com`</br>
    &nbsp;&nbsp;&nbsp;&nbsp;`Hostname ssh.github.com`</br>
    &nbsp;&nbsp;&nbsp;&nbsp;`Port 443`

--------------------

## Correção para o Bitbucket

1. Abra o arquivo de configuração do Git com o comando a baixo, utilizando um editor de texto (geralmente está nesse caminho):

    > code ~/.ssh/config

2. Adicione o código a baixo no arquivo:

    `Host bitbucket.org`</br>
    &nbsp;&nbsp;&nbsp;&nbsp;`Hostname  altssh.bitbucket.org`</br>
    &nbsp;&nbsp;&nbsp;&nbsp;`Port  443`

--------------------

## Correção para o GitLab

1. Abra o arquivo de configuração do Git com o comando a baixo, utilizando um editor de texto (geralmente está nesse caminho):

    > code ~/.ssh/config

2. Adicione o código a baixo no arquivo:

    `Host gitlab.com`</br>
    &nbsp;&nbsp;&nbsp;&nbsp;`Hostname altssh.gitlab.com`</br>
    &nbsp;&nbsp;&nbsp;&nbsp;`User git`</br>
    &nbsp;&nbsp;&nbsp;&nbsp;`Port 443`

--------------------

- Exemplo do arquivo modificado:

    ![](https://github.com/CristianAmbrosi/tutoriais/blob/master/images/correction-port-22-git.png)

--------------------

## Referências

https://help.github.com/articles/using-ssh-over-the-https-port/

https://stackoverflow.com/questions/7953806/github-ssh-via-public-wifi-port-22-blocked/

https://askubuntu.com/questions/610940/ssh-connect-to-host-github-com-port-22-connection-refused

https://help.github.com/articles/error-permission-denied-publickey/
