Exercício 7: Comunicação Entre Containers com Rede Personalizada
Neste exercício, vamos criar uma rede personalizada no Docker para conectar diferentes containers de uma aplicação, garantindo que a comunicação entre os serviços seja isolada e segura.

Passo 1: Clonando o Repositório
Comece clonando o repositório que contém o projeto exemplo:
git clone https://github.com/docker/awesome-compose.git
cd awesome-compose/react-express-mongodb
Passo 2: Configurando o Arquivo docker-compose.yml
No arquivo docker-compose.yml, configure os três serviços da aplicação (frontend, backend e mongodb) da seguinte forma:
```
services:
  frontend:
    build: ./frontend
    ports:
      - "3000:3000"
    networks:
      - app-network
    depends_on:
      - backend

  backend:
    build: ./backend
    ports:
      - "3001:3001"
    environment:
      - MONGO_URI=mongodb://mongodb:27017/mydb 
    networks:
      - app-network
    depends_on:
      - mongodb

  mongodb:
    image: mongo
    ports:
      - "27017:27017"
    networks:
      - app-network

networks:
  app-network:
    driver: bridge
```
Explicação:
frontend: Serviço responsável pela interface do usuário, exposto na porta 3000.

backend: Serviço que executa a lógica do servidor, exposto na porta 3001, com uma variável de ambiente para se conectar ao MongoDB.

mongodb: Serviço que executa o banco de dados MongoDB, exposto na porta 27017.

app-network: Rede personalizada que conecta todos os serviços de forma isolada e segura.

Passo 3: Executando os Containers
Com a configuração pronta, execute os containers com o comando abaixo:
docker-compose up -d
Isso irá iniciar todos os serviços definidos no docker-compose.yml em segundo plano.

Passo 4: Verificando a Rede
Para verificar a configuração da rede personalizada, utilize o comando abaixo:
docker network inspect app-network
Isso exibirá detalhes sobre a rede app-network e como os containers estão conectados a ela.
