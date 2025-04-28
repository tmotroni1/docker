EXERCICIO 11 - Analisando vulnerabilidades
1- Instalando o Trivy
curl -sfL https://raw.githubusercontent.com/aquasecurity/trivy/main/contrib/install.sh | sudo sh -s -- -b /usr/local/bin v0.61.1
2- Analisando a imagem
trivy image --severity HIGH,CRITICAL python:3.9
3- Solução
Algumas Bibliotecas afetadas: libaom3, libbluetooth-dev, libexpat1, libharfbuzz0b O principal problema se encontra na imagem base que está desatualizada, então a melhor sugestão é atualizar a imagem base e suas dependencias para que seja reduzida as vulnerabilidades em seu sistema
