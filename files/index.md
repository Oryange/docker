## Conceitos docker
#### Docker Desktop:
É uma interface para trabalhar no terminal.

#### Container
Container é o docker rodando alguma imagem (utiliza da imagem para poder ser executado) - consequentemente executando algum código proposto por ela.
Os containers do docker não tem conexão com nada de fora deles - por isso precisamos expor portas. 

#### Imagem
É o projeto que será executado pelo container, todas as instruções estarão declaradas nela. 
Imagens são originadas de arquivos que programamos para que o docker crie uma estrutura que execute determinadas ações em containers (programamos uma imagem e a executamos por meio de um container).
* imagens contém informações como: imagens base, diretório base, comandos a serem executados, porta de aplicação e etc;
* ao rodar um container baseado na imagem, as isntruções serão executadas em camadas.


------------------------------------

## Trabalhando com Containers
* docker-compose up -d = `senão admin, utilizar 'sudo'` 
* docker run - `rodar container`
ex: docker run docker/whalesay cowsay
* docker run it <image> - `executar container com interação`
* docker ps - `ver containers rodando`
* docker ps -a - `ver containers executados`
* docker run -d <image> - `executar container em background`
* docker stop <nome> - `parar o container`
* docker run -p 3000:80 <image> 
ex: expor porta 3000 do pc(localhost:3000) na porta 80 que é onde quero receber do container
* docker stop <id ou nome> - `parando container`
* docker start <id> - `re/iniciar container`
* flag --name - `definir nome do container`
ex: docker run -d p 80:80  --name <nomeQueQuero>
* docker logs <id> - `verificar logs`
* docker rm <id> - `remover container da máquina`
* docker rm <id>  -f - `forçar a remoção do container rodando`
* docker run --rm <id> - `remove container automaticamente após sua utilização`
* docker rmi <id imagem> - `remover imagem da máquina`
* docker rmi <id imagem> -f - `forçar a remoção da imagem da máquina`
* docker system prune - `Limpeza de imagens, containers e networks não utilizados`
* docker pull <image> - `baixar uma imagem específica`
* flag --help - `ver todas as opções disponíveis nos comandos`
* docker cp <nome container>:<caminho><onde quero a copia> - `copiar arquivos entre containers`
ex: docker cp meu_app:/app/app.js ./copia/
* docker top <nome> -`verificar informações de processamento de um container`
* docker inspect <nome> -`verificar dados de um container`
* docker stats -`verificar o processamento que está sendo executado em um container`


 ------------------------------------
## Containers e imagens
### Criando uma imagem
Para criar uma imagem, precisa-se de um arquivo `Dockerfile` em uma pasta que ficará o projeto. Este arquivo precisara de algumas instruções para ser executado:
 * FROM: imagem base
 * WORKDIR: diretória da aplicação 
 * EXPOSE: porta da aplicação 
 * COPY: quais arquivos precisam ser copiados
**EXECUTANDO UMA IMAGEM:** Para executar a imagem primeiramente é necessário fazer o build. 
* docker build <diretorio da imagem> `faz o build - se estiver na mesma pasta, basta rodar 'docker build .'`
- para buildar com a imagem já nomeada: `docker build -t o_nome_que_quero .`
* docker run <id imagem> `executa imagem`
ex 1: docker run -d --name <nome que eu quero> -p 3000:3000 <id image>
ex 2: docker run -d --name meu_app -p 5000:3000 553824a135ba
* docker image ls `para ver todas as imagens que rodaram`
### Multiplas aplicações, mesmo container
Podemos inicializar vários containers com a mesma imagem. 
As aplicações funcionarão em parelelo - para isso faz-se necessário uma porta diferente para cada aplicação e rodar no modo detached.
Exemplo: 
- docker run -d p 3000:3000  --name <nomeQueQuero1>
- docker run -d p 4000:3000  --name <nomeQueQuero2>
- docker run -d p 5000:3000  --name <nomeQueQuero3>
### Alterando o nome da imagem e tag
- docker tag <id imagem> `docker tag 6be9e7fc3e4b minhaimagem`
- docker tag <nome>:<tag>
### Autenticação no Docker Hub
- autenticar pelo terminal: docker login
- inserir usuário e senha
- enviar as próprias imagens para o HUB
- encerrar a conexão no Docker HUb: docker logout
### Enviar imagem para o Docker Hub
- criar repositório
- autenticar
- docker push <image>
