# Ambiente de desenvolvimento com Docker e Docker Compose

O proposito deste repositório é demonstrar como utilizo o [Docker](https://docs.docker.com/get-started/overview/) e [Docker Compose](https://docs.docker.com/compose/) para montar meu ambiente de desenvolvimento.

O ambiente possui 3 versões do banco de dados MySql (8, 5.7 e 5.6), Apache e possibilidade de troca entre 2 versões do PHP (7.3 e 7.4).

## Instalação

Se você ainda não tem Docker e Docker Compose instalado, aqui estão alguns links para ajuda-lo:

* [Docker](https://docs.docker.com/get-docker/)

* [Docker Compose](https://docs.docker.com/compose/install/)

## Estrutura do ambiente

Precisamos utilizar basicamente dois diretórios **/etc/** e **/var/www/html**.

Temos a seguinte estrutura no diretório /var/www/html

```bash
├── apache
│   ├── mysite.dev.conf
├── docker
│   ├── .dockerignore
│   ├── database
│   │   ├── mysql8
│   │   ├── mysql56
│   │   ├── mysql57
│   ├── docker-compose.yml
│   ├── PHP73
│   ├── PHP74
├── mysite
```

_E o que cada um deles significa?_
  
* **mysite.dev.conf** é a configuração do virtual host do apache.
* **.dockerignore** é como se fosse o .gitignore, é responsável por indicar ao docker o que ele deve ignorar durante o build da imagem.
* **databases** armazena os arquivos de cada versão do banco de dados mysql, perceba que temos 3 versões disponíveis.
* **docker-compose.yml** define os serviços e seus parâmetros para que todos os containers sejam capazes de conversar entre si. 
* **PHP73** e **PHP74** são os dois Dockerfile disponíveis, assim é possível alternar entre versões de PHP.

Também utilizamos o arquivo hosts do sistema, dentro de  **/etc/hosts** este arquivo é responsável por apontar um determinado domínio para um ip especifico. Assim conseguimos criar domínios em nossa própria maquina.

Para adicionar um novo site basta copiar o **mysite.dev.conf**, renomear de acordo com domínio pretendido e configurar o vhost.

Para iniciar os serviços basta entrar na pasta do docker **/var/www/html/docker** e executar o seguinte comando:
```
docker-compose up --build -d
```

Para acessar o banco de dentro do container do php utilize o host moodle-db57, usuário e senha root.

Para acessar o banco de fora do container do php utilize o host 127.0.0.1, a porta 3357, usuário e senha root.

Por padrão esta utilizando o Dockefile da versão 7.4 do PHP, para alterar para o 7.3 basta alterar o seguinte trecho do *docker-compose.yml* de "dockerfile: PHP74" para "dockerfile: PHP73", e executar o comando acima novamente.

