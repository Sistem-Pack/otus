# Установка и настройка PostgreSQL в контейнере Docker
## Установка Docker Engine
Установка Docker Engine согласно оф. документации:
1. sudo apt-get remove docker docker-engine docker.io containerd runc
2. sudo apt-get update 
3. apt-get install \    ca-certificates \    curl \    gnupg \    lsb-release
4. sudo mkdir -p /etc/apt/keyrings
5. curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
6.echo \ "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

## сделать каталог /var/lib/postgres

mkdir /var/lib/postgres

## развернуть контейнер с PostgreSQL 14 смонтировав в него /var/lib/postgres

1. Подготовимся к следующим пунктам 
1.1. Создадим Докер-сеть:
	docker network create pg-net
	ea75b5d386df7da459d235d9c3251f4bff5f5e6266ffcf0727fc91ec2c649901
2. подключаем созданную сеть к контейнеру сервера Postgres:
2.1. sudo docker run --name pg --network pg-net -e POSTGRES_PASSWORD=1 -d -p 5432:5432 -v /var/l
ib/postgres:/var/lib/postgresql/data postgres:14
Unable to find image 'postgres:14' locally
14: Pulling from library/postgres
461246efe0a7: Pull complete
8d6943e62c54: Pull complete
558c55f04e35: Pull complete
186be55594a7: Pull complete
f38240981157: Pull complete
e0699dc58a92: Pull complete
066f440c89a6: Pull complete
ce20e6e2a202: Pull complete
c0f13eb40c44: Pull complete
3d7e9b569f81: Pull complete
2ab91678d745: Pull complete
ffc80af02e8a: Pull complete
f3a57056b036: Pull complete
Digest: sha256:3e2eba0a6efbeb396e086c332c5a85be06997d2cf573d34794764625f405df4e
Status: Downloaded newer image for postgres:14
338db57784cfeb70860a45077b3f96e7b53f04dfbda95506d6d2dc3e35b630fd

