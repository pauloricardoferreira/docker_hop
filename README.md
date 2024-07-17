## Bem-vindo

Neste repositório você encontrará dicas de como Customizar uma imagem do Apache Hop e também fazer o build .

## Antes de começar

Na [Documentação](https://hop.apache.org/tech-manual/latest/docker-container.html) do Apache Hop, você vao encontrar duas formas de utilizar com o Hop com Containers.

**short-lived** - é utilizada para execuções sob demanda, ou seja, o container é iniciado no momento da execução, muito utilizado em serviços em Cloud sendo executado sob demanda.

**long-lived** - neste tipo de execução, o Servidor Hop fica ligado a todo o momento.

## Introdução

Há diversas formas de buildar uma imagem, e vamos seguir com dois modelos e duas formas

**Modelos:**

- Build com ARGS

     Build com args é uma forma de passar parametros para a contruição da imagem como tokens no momento da contrução e após são exluidos por segurança.
    
     Exemplo de build args [aqui](https://www.youtube.com/watch?v=wYNPnbh6WCM).

- Build Padrão

    No build padrão, você também passa paramentros para o build, porém estes ficam para sempre na imagem

**Formas:**

* Build com Dockerfile e utilização postior no docker-compose
* Build direto com docker-compose

## Estrutuar do Repositório

[docker/docker-build-args](./docker/docker-build-args/) você encontrará como buidar sua imagem passando argumentos no momento do Build onde por exemplo todos os tokens passados no momento do Build serão limpos.
    
- [docker-build-args/build-manual](./docker/docker-build-args/build-manual/)  build da imagem e depois a utilização no docker-compose

- [docker-build-args/build-automatizado](./docker/docker-build-args/build-automatizado/)  build diretamente no docker-compose

[docker/docker-build](./docker-build/) você encotrará a forma de buildar porém passando parâmetros que ficam permanentes na imagem

## Importante

Você pode manter suas imagem localmente de forma segura ou utilizar um repositório de imagem.

Neste ponto há diversas alternativas que você deve estudar o que melhor te atende.

[Docker Hub](http://www.hub.docker.com) repositório de imagem do próprio Docker

Há também opções de Repositórios em Diversas Clouds.

Também é possível criar um repositório de imagem local com o [Harbor](https://goharbor.io/).

Ai é com vocês.

##

### **Observações**

Quer aprender mais sobre docker assista [Linux Tips - O TREINAMENTO DESCOMPLICANDO O DOCKER](https://www.youtube.com/watch?v=Wm99C_f7Kxw&list=PLf-O3X2-mxDn1VpyU2q3fuI6YYeIWp5rR)

Para que este projeto funcione corretamente é necessário seguir os passos em: [Docker - Instalar e Configurar](https://github.com/pauloricardoferreira/docker_instalar_configurar)

[Configurar um ambiente de Desenvolvimento Hop](https://github.com/pauloricardoferreira/hop_configurar_local_desenvolvimento)

[Documentação Apache Hop](https://hop.apache.org)

Caso o horário esteja diferente do GMT-3, atualize o horário do servidor e adicione os itens abaixo na sessão de volumes
- /etc/timezone:/etc/timezone:ro
- /etc/localtime:/etc/localtime:ro
