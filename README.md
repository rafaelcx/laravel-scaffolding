# Laravel-scaffolding
A pretty simplified docker-compose workflow that sets up a LEMP network of containers for local Laravel development.

## Usage

To get started, make sure you have [Docker](https://docs.docker.com/docker-for-mac/install/) and [Composer](https://getcomposer.org/download/) on your system, and then clone this repository.

First we need to install a fresh Laravel application on the `/src` folder and them get the containers up and running using the commads:

-  Fresh Laravel app - `cd src && composer create-project laravel/laravel .`
-  Up and run containers - `docker-compose up -d --build`

Now you should be able to see the Laravel application running at you http://localhost:8080.

There are three containers that handle Composer, NPM, and Artisan commands without having to have these platforms installed on your local computer. Use the following command templates from your project root, modifiying them to fit your particular use case:

- `docker-compose run --rm composer update`
- `docker-compose run --rm npm run dev`
- `docker-compose run --rm artisan migrate` 

Containers created and their ports (if used) are as follows:

- **nginx** - `:8080`
- **mysql** - `:3306`
- **php** - `:9000`
- **npm**
- **composer**
- **artisan**

## Front-end handling

You can use Bootstrap to build a Laravel application with the following steps:

- To use basic Bootstrap CSS you must first run - `docker-compose run --rm composer require laravel/ui` 
- For generating basic scaffolding for bootstrap we can use artisan command -`docker-compose run --rm artisan ui bootstrap`
- Now install the packages with - `docker-compose run --rm npm install`
- For asset compilation you can run - `docker-compose run --rm npm run dev` or `docker-compose run --rm npm run watch`

## Persistent MySQL Storage

By default, whenever you bring down the docker-compose network, your MySQL data will be removed after the containers are destroyed. If you would like to have persistent data that remains after bringing containers down and back up, do the following:

1. Create a `mysql` folder in the project root, alongside the `nginx` and `src` folders.
2. Under the mysql service in your `docker-compose.yml` file, add the following lines:

```
volumes:
  - ./mysql:/var/lib/mysql
```