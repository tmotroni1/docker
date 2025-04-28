Exercício 1: Rodando um Container Básico com Nginx
Este exercício consiste em executar um container Docker usando a imagem oficial do Nginx e configurar uma página estática do TailwindCSS dentro do container.

Passo 1: Clonando a Landing Page
Primeiro, você vai clonar o repositório do GitHub que contém a landing page do TailwindCSS. Para isso, execute o seguinte comando no terminal:
git clone https://github.com/tailwindtoolbox/Landing-Page.git
Isso irá baixar o repositório com os arquivos da landing page para o seu computador.

Passo 2: Criando o Dockerfile
Agora, vamos criar o arquivo Dockerfile que será utilizado para configurar o container Docker. No diretório onde você clonou o repositório, crie um arquivo chamado Dockerfile e adicione o seguinte conteudo:
FROM nginx
COPY . /usr/share/nginx/html
CMD ["nginx", "-g", "daemon off;"]
Explicação:
FROM nginx: Define a imagem base para o container, que será a imagem oficial do Nginx.

COPY . /usr/share/nginx/html: Copia todos os arquivos do diretório atual (onde o Dockerfile está) para o diretório de conteúdo do Nginx no container.

CMD ["nginx", "-g", "daemon off;"]: Inicia o Nginx no modo foreground para manter o container rodando.

Passo 3: Construindo a Imagem
Agora que o Dockerfile está configurado, você precisa construir a imagem Docker. Execute o comando abaixo para criar a imagem com o nome Nginx e a tag 1.0v:
docker build -t Nginx:1.0v .
Este comando irá criar a imagem Docker a partir do Dockerfile e nomeá-la como Nginx:1.0v.

Passo 4: Rodando o Container
Com a imagem criada, você pode rodar o container. Use o seguinte comando para executar o container em segundo plano e mapear a porta 8080 do container para a porta 8080 do seu host:

docker run -dp 8080:8080 Nginx:1.0v
Agora, o Nginx estará rodando no seu container e você pode acessar a página da landing page do TailwindCSS no navegador através de http://localhost:8080.

