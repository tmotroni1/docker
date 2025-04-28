Exercicio 9 - Imagem Docker com Nginx e Material Kit
1- Clonar o repositório do Material Kit
git clone https://github.com/creativetimofficial/material-kit.git
cd material-kit
2- Crie o Dockerfile
FROM nginx:alpine

RUN rm -rf /usr/share/nginx/html/*

COPY . /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
3- Construa a imagem e a execute
docker build -t template:1.0v .
docker run -dp 8080:80 template:1.0v
