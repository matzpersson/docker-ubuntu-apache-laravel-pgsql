# Docker-Compose for Apache/Laravel/Postgres

Some information

## Install instructions

 * docker-compose down
 * docker-compose build
 * docker-compose up
 
This will start apache webserver and Mysql. Go into a second instance of the container to complete Composer installation:
 * docker exec -it #imagename# bash
 * composer install
 
Create the Postgres db. Use pwd's defined in docker-compose.yml:
 * psql -h next5_db_1 -U postgres
 * create database next5;
 * \quit
 
Modify Laravel environment to match db
 * Copy .env_example to .env
 * Open .env and change "DB_USERNAME" AND "DB_PASSWORD" to match docker-compose.yml
 * Update DB_HOST to correct Docker name for the Db container. In this case: next5_db_1
 * Update DB_CONNECTION=pgsql and DB_PORT=5432

Migrate and seed db:
 * php artisan migrate
 * php artisan db:seed
