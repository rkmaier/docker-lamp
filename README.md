# Lamp stack for local development

## Apache and PHP + NodeJS + Maria DB  + Adminer
Based on Ubuntu 18.04 - Apache and PHP 7.2


**Installation**
-------------------
- git clone https://github.com/rkmaier/docker-lamp
- cd docker-lamp

**Configuration and Usage**
----------------------------
- move your app files into the **public** directory
- create/import your database inside **database_1**
- modify the **docker-compose** file according your needs
- docker-compose up -d 


```yaml
version: '3'
services:
  web:
    container_name: server_1
    build: ./docker/apache2-php7
    restart: always
    tty: true
    stdin_open: true
    ports:
      - 80:80
    links:
      - db
    volumes:
      - ./public:/var/www/public
      - ./data/logs/apache:/var/log/apache2
  db:
    container_name: database_1
    image: mariadb:10.0
    ports:
      - 3306:3306
    volumes:
      - ./data:/var/lib/mysql
      - ./docker/conf/my.cnf:/etc/mysql/my.cnf
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_USER: erik
      MYSQL_PASSWORD: skipjack
      MYSQL_DATABASE: database_1
  adminer:
    container_name: adminer
    image: adminer
    restart: always
    volumes:
      - ./docker/conf/adminer.ini:/usr/local/etc/php/conf.d/0-upload_large_dumps.ini
    ports:
      - 8080:8080
    links:
      - db
```


