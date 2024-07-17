## Estrutuda do docker-compose.yml

Não tem erro, o docker-compose.yml é todo escrito no formato yaml, que é uma estrutura onde o ser humano comprende e pode trablhar facilmente.

Atualmente, muitos serviços utilizam este formato para configurar muitas coisas.

O arquivo é formado por CHAVE:VALOR ou TAG:VALOR podendo ou não conter subníveis.


````yml
# services: definição de 1 ou mais serviços
services:
# nome do primeiro serviços
# não pode conter serviços com o mesmo nome
  hop-server:
  # após o nome do serviçom é necessário informar a origem da imagem.
  # pode ser uma imagem pronta ou uma custonizada
  #
    # image: apache/hop:2.7.0 -> exemplo de imagem quem alguém fez o build e disponibilizou para utilizar
# vamos fazer um build customizado com a tag buiid
    build: 
# context: é onde o arquivo Dockerfile está, no caso está no mesmo núvel do docker-compose, por este motivo utilizamos o . para indicar o diretório atual
# caso esteja em outro diretório, você utilizar ./nome_do_diretório
# o ideal é a pasta ou o Dockerfile estarem a partir da origem do docker-compose
      context: .
      dockerfile: Dockerfile
# aqui podemos passar os ARGS - Argumentos no momento do Build
      args:
        - IMAGE_VERSION=2.9.0
        - ENVIRONMENT=dev 
# container_name é para a identificação do container de forma exclusiva, não pode repetir.
# caso não use, você precisa obter o Container ID
    container_name: hop-server
# 
# aqui podemos definir em qual porta o container ficará exposto
# há casos onde os containers se comunicam apenas de forma interna.
# mais isso depende de cada 
    ports:
      - "8182:8182"

# nome do sergundo
  postgres:
    image: postgres:14
    container_name: postgres
# environment é utilizado para passar alguns parametros para a imagem
# no exemplo, passamos: Usuário, Senha e Nome do Banco para que o Postgres crie uma configuraçãio inicial
# há muitas possivilidades, por isso, estudo bem e faça exemplos para reformar seu aprendizado
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgres
      POSTGRES_DB: postgres
# volumes é a forma que o docker utilzar para armazenar os dados do container
# por padrão um container não grava dados, e caso deseje armezar em algum lugar esse essa tag com as devidas configurações da sua imagem
    volumes:
      - postgres:/var/lib/postgresql/data
# deixo essas para que você pesquisar
    restart: always
    networks:
      - postgres
    ports:
      - 5432:5432

volumes:
  postgres:

# nome de n serviços
````
Aqui você encontrará duas formas de conternização.

Por padrão o `docker compose` procura o arquivo `docker-compose.yml` e caso utilize outros nomes, pode utilizar o comando abaixo.

````bash
docker compose -f docker-compose-build.yml  up -d --build
````

ou utilizar o comando padrão.

```bash
docker compose up -d --build
```
para buildar uma imagem com args de forma manual utilizamso o comando abaixo

```bash
docker build --build-arg SOFTWARE_NAME=software-package --build-arg VERSION=1.0 -t myimage:1.0 .
```

para buildar uma imagem de forma manual utilizamos o comando abaixo

```bash
docker build -t myimage:1.0 .
```


A saida que você verá é
![](./image/out-comand-docker-compose.png)


Não deixe de conferir a [Documentação](https://docs.docker.com/manuals/) oficial para mais detalhes.


**Dicas**

Fiquem sempre atentos as mudanças no Docker.

O comando docker build está caindo e desuso, e em seu lugar está o buildx que é mais eficiente.

[Documentação](https://docs.docker.com/reference/cli/docker/buildx/)

ou siga os passos para instalar:

````bash
mkdir -p ~/.docker/cli-plugins/
curl -SL https://github.com/docker/buildx/releases/download/v0.10.0/buildx-v0.10.0.linux-amd64 -o ~/.docker/cli-plugins/docker-buildx
chmod +x ~/.docker/cli-plugins/docker-buildx
````

agora sim, pode seguir com os builds.