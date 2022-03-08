# Docker - Laravel

![Image](https://repository-images.githubusercontent.com/309769351/1c0dfc80-1def-11eb-9e5c-641da3e3c9b4)

Project forked [Docker Laravel 8](https://github.com/supermavster/docker-laravel-8)

[TOC]

A pretty simplified Docker Compose workflow that sets up a LEMP (Linux, NGINX,
MySQL, PHP) network of containers for local Laravel development.

## Ports

Ports used in the project:
| Software       | Port           |
| -------------- | -------------- |
| **nginx**      | 8787           |
| **mysql**      | 3306           |
| **php**        | 9000           |
| **redis**      | 6379           |

## Build

To get started, make sure you have [Docker installed](https://docs.docker.com/)
on your system and [Docker Compose](https://docs.docker.com/compose/install/),
and then clone this repository.

1. Clone this project:

```sh
git clone https://github.com/wdog/docker-laravel-8.git
```

2. Inside the folder `docker-laravel-8` and Generate your own `.env` to docker compose with the next command:

```sh
cp .env.example .env
```

3. You need **Create** or **Put** your laravel project in the folder source; to create follow the next instructions.

4. Build the project whit the next commands:

```sh
docker-compose build
docker-compose up -d nginx
```


## Remember

The configuration of the database **must be the same on both sides**  .

```dotenv
# .env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=db_name
DB_USERNAME=db_user
DB_PASSWORD=db_password
DB_ROOT_PASSWORD=secret
```

```dotenv
# source/.env
[...]
DB_CONNECTION=mysql
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=db_name
DB_USERNAME=db_user
DB_PASSWORD=db_password
[...]
```

The only change is the `DB_HOST` in the `source/.env` where is called to the container of `mysql`:

```dotenv
# source/.env
DB_HOST=mysql
DB_ROOT_PASSWORD=secret
```

change permission to source folder if needed

```bash
chown 1000:1000 source
```

### Make a new Project

```sh
docker-compose run --rm composer create-project laravel/laravel .
```

### Use extings sources

Copy your project into `./source` folder

### Copy Environment

```sh
cp .env.example .env
```

## Start Here

### Install Libraries from Node

```sh
docker-compose run --rm npm install
```

Run compiler (Webpack.mix.js) or Show the view compiler in node:

```sh
docker-compose run --rm npm run dev
# or
docker-compose run --rm npm run production
```


### Install Libraries from Composer

install

```sh
docker-compose run --rm composer install
```

or update


```sh
docker-compose run --rm composer update
```


### Clear/Clean the project

```sh
docker-compose run --rm artisan cache:clear
docker-compose run --rm artisan view:clear
docker-compose run --rm artisan route:clear
docker-compose run --rm artisan clear-compiled
docker-compose run --rm artisan storage:link
```


### Generate Keys

```sh
docker-compose run --rm artisan key:generate
```

### Run migrations

start the `docker-compose up -d `

```sh
docker-compose run --rm artisan migrate --seed
```

### Stop

To Down and remove the volumes we use the next command:

```sh
docker-compose down -v
```
