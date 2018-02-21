
# Laravel_Docker template

Includes docker file and shell script for launching the docker image. Script also creates a private subnet to communicate with seperate mysql/pgsql database container if applicable. The Docker file installs php extension for mysql/pgsql depedent on the Dockerfile you choose.

The runDocker.sh have a --network=my-net flag on the docker run command line. This creates a private network and enables this container to connect directly to other containers (db containers for example) with the same --network identifier.

## Install instructions

 * Make sure Docker is installed
 * git clone this directory
 * Change into the working directory. In this example, the project name is "managd" which will be the name of the image created from the build.
 * Rename Dockerfile_* to just Dockerfile dependent on your choice of db environment.
 * Build docker image with: "docker build -t managd ."
 * Launch docker with ./runDocker.sh
 * Check in browser: http://localhost:8181
 
 ## Configuration of Laravel
 
Once install is completed once again make sure you are in the working directory and stop the container instance:
````ruby
docker stop managd
````

If you chose mysql, use the mysql client to connect to your mysql instance to create a new mysql database. In this example mysql is installed in a seperate container named 'mysql_dev':

````ruby
mysql -h mysql_dev -u root -p
create database testdb;
CREATE USER 'homestead'@'%' IDENTIFIED BY '<yoursecret>';
grant all privileges on *.* to 'homestead'@'%';
````

Copy .env.example to .env and change the database variable in .env:
````ruby
DB_CONNECTION=mysql
DB_DATABASE=testdb
DB_PASSWORD=<yoursecret>
````

Generate the Artisan key:
````ruby
php artisan key:generate
````

Migrate the tables and seed the database:
````ruby
php artisan migrate:refresh --seed
````

Install NPM components listed in package.json:
````ruby
npm install
````

Run NPM dev to compile js:
````ruby
npm run dev
````

and restart the Docker instance:
````ruby
./runDocker.sh
````

You should now be able to browse this app on http://localhost:8181 but this time with a connected db. 
 

# docker-ubuntu-apache-laravel
# docker-ubuntu-apache-laravel
