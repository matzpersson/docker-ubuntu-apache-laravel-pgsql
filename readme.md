# Docker-Compose for Apache/Laravel/Postgres

Some information

## Install instructions

 * docker-compose down
 * docker-compose build
 * docker-compose up
 
This will start apache webserver and Mysql. Go into a second instance of the container to complete Composer installation:
 * docker exec -it #imagename# bash
 * composer install
 
Create the Mysql db. Use pwd's defined in docker-compose.yml:
 * psql -h next5_db_1 -U postgres
 * create database next5;
 * \quit
 
Modify Laravel environment to match db
 * Copy .env_example to .env
 * Open .env and change "DB_USERNAME" AND "DB_PASSWORD" to match docker-compose.yml

Migrate and seed db:
 * php artisan migrate
 * php artisan db:seed
