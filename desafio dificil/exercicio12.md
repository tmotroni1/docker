Exercicio 12 - Corrigindo vulnerabilidades encontradas
Dockerfile vulnerável
FROM python:3.9
WORKDIR /app 
COPY requirements.txt . 
RUN pip install -r requirements.txt
COPY . .
CMD ["python", "app.py"]
requirements.txt
flask==1.1.1
requests==2.22.0
Podemos realizar diversas atualizações nesse arquivo e utilizar outras imagens para reduzir as vulnerabilidades como usar uma imagem menor como o python:3.9-slim ou utilizar uma imagem mais recente como o python:3.14-slim.

Devemos também atualizar as bibliotecas que usaremos como o Flask e o Requests. Além Disso, deveremos garantir que o usuário não acesse como root, deixando assim o usuário com menos privilégios tornando mais difícil algum possível ataque ao container

Dockerfile Seguro/Atualizado
FROM python:3.14-slim

WORKDIR /app 

COPY requirements.txt . 

RUN pip install -r requirements.txt

RUN groupadd -r usuario && useradd -r -g usuario anti-attack

RUN chown -R anti-attack:usuario /app

USER anti-attack

COPY . .

CMD ["python", "app.py"]
requirements atualizado:
flask
requests
