# Docker Comandos - Cheatsheet

## 🐳 Comandos básicos do Docker

- `docker --version`  
  Mostra a versão do Docker instalada.

- `docker help`  
  Lista todos os comandos disponíveis do Docker.

## 📦 Imagens

- `docker pull <imagem>`  
  Baixa uma imagem do Docker Hub.  
  **Ex:** `docker pull nginx`

- `docker images`  
  Lista todas as imagens disponíveis localmente.

- `docker rmi <imagem>`  
  Remove uma imagem do sistema.

- `docker build -t <nome> .`  
  Cria uma imagem a partir de um `Dockerfile`.  
  **Ex:** `docker build -t minha-app .`

## 📦 Containers

- `docker run <imagem>`  
  Cria e inicia um container.  
  **Ex:** `docker run nginx`

- `docker run -d <imagem>`  
  Roda o container em segundo plano (modo *detached*).

- `docker run -p 8080:80 <imagem>`  
  Mapeia portas (host:container).

- `docker ps`  
  Lista containers em execução.

- `docker ps -a`  
  Lista todos os containers (inclusive parados).

- `docker stop <container>`  
  Para um container em execução.

- `docker start <container>`  
  Inicia um container parado.

- `docker restart <container>`  
  Reinicia um container.

- `docker rm <container>`  
  Remove um container.

- `docker logs <container>`  
  Mostra os logs do container.

- `docker exec -it <container> bash`  
  Acessa o terminal do container.

## 💾 Volumes

- `docker volume ls`  
  Lista volumes.

- `docker volume create <nome>`  
  Cria um volume.

- `docker volume rm <nome>`  
  Remove um volume.

## 🌐 Redes

- `docker network ls`  
  Lista redes Docker.

- `docker network create <nome>`  
  Cria uma rede.

- `docker network rm <nome>`  
  Remove uma rede.

## 🧹 Limpeza

- `docker system prune`  
  Remove containers, imagens e redes não usadas (⚠ cuidado).

