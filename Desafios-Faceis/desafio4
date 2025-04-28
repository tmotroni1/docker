Exercício 4: Criando um Dockerfile para uma Aplicação Simples em Python com Flask
Neste exercício, vamos configurar um container Docker para rodar uma aplicação simples em Python utilizando o Flask, que irá retornar uma mensagem ao acessar o endpoint.

Passo 1: Criando o Dockerfile
Crie um arquivo chamado Dockerfile e adicione o seguinte conteúdo:

dockerfile
Copiar
Editar
FROM python:alpine

WORKDIR /app
COPY requirements.txt /app/
RUN pip3 install -r requirements.txt

COPY . /app/

CMD [ "python3", "app.py" ]

EXPOSE 8000
Explicação:
FROM python:alpine: Usamos a imagem base do Python, otimizada e leve, chamada Alpine.

WORKDIR /app: Define o diretório de trabalho dentro do container como /app.

COPY requirements.txt /app/: Copia o arquivo requirements.txt para o diretório /app/ dentro do container.

RUN pip3 install -r requirements.txt: Instala as dependências listadas no arquivo requirements.txt.

COPY . /app/: Copia todos os arquivos do projeto para o diretório /app/ dentro do container.

CMD [ "python3", "app.py" ]: Define o comando para rodar a aplicação Flask.

EXPOSE 8000: Expõe a porta 8000 para que o container possa ser acessado externamente.

Passo 2: Construindo e Rodando a Imagem
Agora, crie a imagem Docker com o seguinte comando:

docker build -t flask:1.0v .
Depois, execute o container com o comando abaixo, mapeando a porta 8000 do container para a mesma porta no host:

docker run -dp 8000:8000 flask:1.0v
Passo 3: Testando
Para testar se a aplicação está funcionando corretamente, faça uma requisição curl ao endpoint:

curl localhost:8000
Você deverá receber a seguinte mensagem como resposta:

Hello world!
Essa versão reescrita mantém a mesma explicação, mas com uma forma diferente de apresentação.
