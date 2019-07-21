DOCKER

* DOCKER HUB
- Repositorios oficiais do Docker

* OBSERVAÇÕES
-> Simbolo do comando 
* Simbolo to titulo da aula
- e -- Comentarios logo abaixo do comando para o entendimento
 
COMANDOS

* RUN
- Faz o pull
- Faz a criação
- Inicia
- Executa

* MODO INTERATIVO - Para testes
-> sudo docker container run debian bash --version
-- Instala um container com o debian e retorna a versão do bash

* PS
-> docker container ps
-- Mostra os containers ativos
-> docker container ps -a
-- Mostra todos os containers ativos ou inativos
- docker container run --rm debian
-- Ele exec um container e em seguida remove

* RUN CRIA SEMPRE UM NOVO CONTAINER
-> docker container run -it debian bash
-- Acessa o terminal do container

* NOMEAR UM CONTAINER
-> docker container run --name debian -it debian bash
- Caso tenta criar um container com o mesmo nome da erro

* REUTILIZANDO CONTAINERS
-> docker container ls -a
-> docker container start -ai debian
-- Com containers nomeados você consegue reutilizar o mesmo container

* MAPEAR PORTAS DOS containers
-> docker container run -p 8080:80 nginx
-- Cria container do server nginx expondo a porta 8080 e local 80
-- Abrir um novo terminal e acessa curl http://localhost:8080 ou acessar pelo navegador
-> docker container ps 
-- Mostra o container ngnix ativo

* MAPEAMENTO DE VOLUMES
-> docker container run -p 8080:80 -v $(pwd)/not-found:/usr/share/nginx/html nginx
-- Aqui o comando esta mapeando para a porta 8080 que o caminho /usr/share/nginx/html vai
-- apontar para a pasta not-found
-- Acessando o localhost:8080 da erro de servidor forbiden por que a pasta not-found ainda não existe
- Fazendo o mapeamento para uma pasta criada no container html/index.html e não para o padrão do nginx
-> docker container run -p 8080:80 -v $(pwd)/html:usr/share/nginx/html nginx

* EXECUTAR UM SERVIDOR WEB EM BACKGROUND
-> docker container run -d --name ex-daemon-basic -p 8080:80 -v $(pwd)/html:/usr/share/nginx/html nginx
-> -d modo Daemon
-- Retorna o id do container em execução ex: e1c48cffc55b497e7ab1d46c345f6edbf26e842909f32005c53bb470be2d7b09
-> docker container ps
-> docker container stop ex-daemon-basic

* GERENCIAR CONTAINER EM BACKGROUND
-> docker container start ex-daemon-basic
-> docker ps
-> docker container restart ex-daemon-basic
-> docker container stop ex-daemon-basic

* MANIPULAÇÃO DE CONTAINERS EM MODO DAEMON
-> docker container ls
-> docker container list
-> docker container ps
-> docker container ls -a
-> docker container list -a
-> docker contaner ps -a 
-> docker ps -a
-> docker container logs ex-daemon-basic
-> docker container inspect ex-daemon-basic
-- Inspeciona o container mostrando varias informações
-> docker container exec ex-daemon-basic uname -or
-- Executa um comando no container, nesse caso a versão do sistema

* NOVA SINTAXE NO CLIENT DO DOCKER
-> docker container ls
-> docker image ls
-> docker volume ls
-> docker container ps -a
-> docker image rm -f 00bf7fdd8baf
-- Remove pelo id da image


########################################################################

* DIFERENÇAS ENTRE CONTAINERS E IMAGENS
-> docker container --help
-> docker image --help
-> docker volume --help

* ENTENDENDO MELHOR AS IMAGENS
-> docker image pull redis:latest
-- Faz o pull no docker hub da ultima versão tagueada
-> docker image ls
-> docker image inspect redis:latest
-> docker image tag redis:latest coder-redis
-- Criando outra imagem redis com outra tag
-> docker image rm redis:latest coder-redis
-- Dica sempre usar uma versão latest e não a ultima