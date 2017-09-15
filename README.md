# Descrição

Docker utilizando o compose, arquivo de configuração com variáveis de ambiente, criando um container nginx 1.13.3 e um container php 7.1.9-fpm ligados através de um link e criando um container mysql 5.7.19.

# Configuração Container Nginx

1. Exposição de portas

	80 e 443

2. Volume (Obs: verificar se na configuração do docker -> drivers compartilhados, as unidades c: e/ou d: estão habilitadas)

	Aplicação: htdocs -> /var/www/html
	
	Logs: nginx/logs -> /var/log/nginx
	
	Virtual Host: nginx/sites -> /etc/nginx/conf.d
	
3. Virtual Host

	Criação do vhost modelo http://api.dev (vhost modificável)

# Configuração Container Php

1. Exposição de portas

	9000

2. Volume (Obs: verificar se na configuração do docker -> drivers compartilhados, as unidades c: e/ou d: estão habilitadas)

	Aplicação: htdocs -> /var/www/html
	
3. Bibliotecas

	Habilitação de bibliotecas do php através de arquivo de configuração. Ex: MBSTRING, GD, MCRYPT, PDO_MYSQL, etc.
	
# Configuração Container Postgresql

1. Exposição de portas

	5432

2. Volume (Obs: verificar se na configuração do docker -> drivers compartilhados, as unidades c: e/ou d: estão habilitadas)

	Aplicação: postgresql/data -> /var/lib/postgresql/data

3. Configuração para conexão

	- POSTGRES_DB       = default
	
    - POSTGRES_USER     = default
	
    - POSTGRES_PASSWORD = secret
	
    - POSTGRES_PORT     = 5432
	
# Como utitilizar

1. Clone o repositório usando o comando:

   git clone https://github.com/danielnogueira-dev/Docker-Compose-Nginx-Php-Postgresql

2. Entre na pasta Docker-Compose-Nginx-Php-Postgresql e copie o arquivo env-example para .env.

   cp env-example .env

3. Rode seu container:

   docker-compose up -d

4. Adicione os domínios no arquivo de hosts do windows.

   127.0.0.1 localhost

   127.0.0.1 api.dev

5. Abra no navegador

   http://localhost

   http://api.dev

6. Acessar o shell do container:
    
	winpty docker exec -it nginx bash

	winpty docker exec -it php-fpm bash
	
	winpty docker exec -it postgresql bash

7. Acessar o banco de dados dentro do container Postgresql

	psql default default

8. Comandos básicos para utilizar o banco de dados

	\l;

	CREATE DATABASE teste;
	
	\connect teste;
	
	\dt;