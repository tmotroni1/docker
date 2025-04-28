EXERCÍCIO 5 – Criando e utilizando volumes para persistência de dados
Projeto utilizado:
react-express-mysql

1- Configuração do volume para o MySQL
No arquivo docker-compose.yaml, foi configurado o serviço db com persistência de dados através de um volume:

volumes:
  - my-sql-data:/var/lib/mysql
Esse volume armazena os dados do banco de forma persistente, garantindo que eles não sejam perdidos mesmo após reiniciar ou remover o container.

2- Execução da aplicação
docker compose up -d
