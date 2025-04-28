Exercício 8: PostgreSQL + pgAdmin com Docker Compose
Neste exercício, vamos criar um arquivo Docker Compose para rodar uma aplicação com um banco de dados PostgreSQL e o pgAdmin para gerenciamento.

Passo 1: Clonando o Repositório
Primeiro, clone o repositório que contém o exemplo da configuração:
git clone https://github.com/docker/awesome-compose.git
cd awesome-compose/postgresql-pgadmin
Passo 2: Criando o Arquivo docker-compose.yml
Agora, crie ou edite o arquivo docker-compose.yml com o seguinte conteúdo:
services:
  db:
    image: postgres:15
    restart: unless-stopped
    environment:
      POSTGRES_USER: meu_usuario
      POSTGRES_PASSWORD: minha_senha_segura
      POSTGRES_DB: meu_banco
    volumes:
      - postgres_data:/var/lib/postgresql/data
    ports:
      - "5432:5432"
    networks:
      - postgres-net

  pgadmin:
    image: dpage/pgadmin4:latest
    restart: unless-stopped
    environment:
      PGADMIN_DEFAULT_EMAIL: meu_email@dominio.com
      PGADMIN_DEFAULT_PASSWORD: senha_pgadmin
    ports:
      - "8080:80"
    depends_on:
      - db
    networks:
      - postgres-net

networks:
  postgres-net:
    driver: bridge

volumes:
  postgres_data:
Explicação:
db: Serviço que executa o banco de dados PostgreSQL, configurado com um usuário, senha e banco de dados iniciais. O volume postgres_data é usado para persistir os dados do banco.

pgadmin: Serviço que executa o pgAdmin para gerenciar o banco de dados. Ele depende do serviço db e é acessado na porta 8080.

postgres-net: Rede personalizada para conectar os serviços de forma isolada.

postgres_data: Volume persistente para os dados do PostgreSQL.

Passo 3: Inicializando os Containers
Depois de configurar o arquivo docker-compose.yml, inicie os containers com o seguinte comando:
docker-compose up -d
Isso fará com que o Docker Compose baixe as imagens necessárias e inicie os containers em segundo plano.
