Exercício 10: Aplicação Python Executando como Usuário Não-Root
Neste exercício, vamos criar uma aplicação Python utilizando Flask e rodá-la dentro de um container Docker como um usuário não-root, melhorando a segurança do ambiente.

Passo 1: Código do Arquivo app.py
Primeiro, crie um arquivo app.py com o seguinte código:

from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello():
    return "Olá! Este aplicativo está rodando como um usuário não-root!\n"

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
Este código cria uma aplicação Flask simples que retorna uma mensagem quando acessado.

Passo 2: Criando o Arquivo requirements.txt
Em seguida, crie o arquivo requirements.txt para listar as dependências do seu projeto. Nesse caso, vamos adicionar apenas o Flask:

Passo 3: Conteúdo do Dockerfile
Agora, crie o Dockerfile com o seguinte conteúdo:

FROM python:slim

WORKDIR /app

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY . .

RUN groupadd -r dev && useradd -r -g dev leonardo

RUN chown -R leonardo:dev /app

USER leonardo

EXPOSE 5000

CMD ["python", "app.py"]
Explicação:
FROM python:slim: Usamos uma imagem Python leve.

WORKDIR /app: Define o diretório de trabalho dentro do container.

COPY requirements.txt .: Copia o arquivo requirements.txt para o container.

RUN pip install --no-cache-dir -r requirements.txt: Instala as dependências do projeto.

COPY . .: Copia todo o conteúdo do projeto para o container.

RUN groupadd -r dev && useradd -r -g dev leonardo: Cria um grupo dev e um usuário leonardo.

RUN chown -R leonardo:dev /app: Altera a propriedade dos arquivos para o usuário leonardo.

USER leonardo: Executa o container com o usuário leonardo, não root.

EXPOSE 5000: Expõe a porta 5000 para o acesso externo.

CMD ["python", "app.py"]: Executa a aplicação Flask.

Passo 4: Construindo e Rodando a Imagem
Agora, construa a imagem Docker com o seguinte comando:

docker build -t nome_app:1.0v .
E depois execute o container com o comando:

docker run -dp 5000:5000 nome_app:1.0v
Isso vai rodar o container em segundo plano e mapear a porta 5000 do container para a mesma porta no seu sistema.

Passo 5: Verificando o Usuário Dentro do Container
Para garantir que a aplicação está rodando como o usuário não-root, execute o comando abaixo para verificar o usuário atual no container:

docker exec nome_app:1.0v whoami
O comando whoami deve retornar o nome do usuário leonardo, confirmando que o container está executando como um usuário não-root.
