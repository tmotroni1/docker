EXERCICIO 1
Rodando um container básico
Executando um container usando a imagem do Nginx e acessando a landing page do TailwindCSS como site estático dentro do container.

1- Clonando o Landing page
Clone o repositorio do github da Landing page usando o comando:

git clone https://github.com/tailwindtoolbox/Landing-Page.git
2- Criando a DockerFIle
adicione as seguintes informações ao Dockerfile:

FROM nginx
COPY . /usr/share/nginx/html
CMD ["nginx", "-g", "daemon off;"]
3- Construindo a imagem
Utilize o comando:

docker build -t Nginx:1.0v .
4- Rodando o Container
docker run -dp 8080:8080 Nginx:1.0v
