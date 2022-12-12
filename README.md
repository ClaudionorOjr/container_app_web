# Jornada DevOps com AWS - Impulso

> Bootcamp gratuito promovido pela dio.

## Modulo Docker

**Desafio 01: Criando um Container de uma Aplicação WEB**

PASSO A PASSO:

1. Criar um arquivo YML com as definições de um servidor Apache (httpd); ✅
2. Especificar no arquivo YML o local onde os arquivos da aplicação estarão. A aplicação pode ser um simples Hello World. Será que você consegue executar uma aplicação web completa? ✅
3. Subir o arquivo YML e a aplicação para um repositório no GitHub. ✅

**Comentário:**  
Para esse desafio iniciei um projeto utilizando Vite + TypeScript, fiz uma pequena alteração na página de apresentação do build tool (para mostrar que pode ser costumizada), realizei o build e subi para um container rodando Apache, como pede o desafio.

### Info

> Outra maneira de realizar o desafio **utilizando multistage** do node com o apache.

Dessa forma não é necessário rodar com antecedência o comando build do vite no projeto. A pasta `./dist` já gerada, que se encontra na raiz do projeto, pode ser apagada, pois a image node no Dockerfile irá realizar o build automaticamente, gerando novamente a pasta, de onde irá copiar os arquivos buildados para dentro do servidor Apache.

**Alterar o arquivo `docker-compose.yml`:**

```yml
version: "3.8"

services:
  apache:
    container_name: my-apache-app
    build: ./website/
    ports:
      - "80:80"
```

**Descomentar linhas no arquivo `Dockerfile`:**

```
FROM node as builder

WORKDIR /app

COPY . .

RUN npm install && npm run build

FROM httpd

COPY --from=builder /app/dist /usr/local/apache2/htdocs/
```
