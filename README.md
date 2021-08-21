# Nginx PHP7 MySQL NodeJS Docker

Fast lightweight Docker network using PHP MySQL Nginx and Node

## Run the project:

### Fetch everything and build
```bash
docker-compose up -d --build
```

### Create Symfony project folder
Go inside the /var/www/project folder:
```bash
docker exec -it php74-container bash
```

Install Symfony project folder with composer:
```bash
composer create-project symfony/skeleton .
```

### Open first Symfony page
http://localhost:8080

### Git
In your root folder, not in Docker container:
```bash
git init
```

### Symfony requirements
Back in the container:
```bash
symfony check:req
```

### Doctrine
Install Doctrine with Composer (orm-pack):
```bash
composer require doctrine
```

### MySQL
Configure MySQL credentials in .env file
uncomment line with `DATABASE_URL="mysql:`
and comment on line with `DATABASE_URL="postgresql:`
So we have: `DATABASE_URL="mysql://root:secret@mysql8-service:3306/docker-symfony?serverVersion=8"`
where:
* login: root
* password: secret
* host: mysql8-service (taken from the Dockerfile)
* port: 3306
* base name: choose what you want
* serverVersion: we use MySQL v8

### Exit the container
```bash
exit
```

For info: 
You may use `docker-compose run` instead of `docker exec`

### Creating database for Symfony
```bash
docker-compose run --rm php74-service php bin/console doctrine:database:create
```

Hint:
(docker exec for containers and docker-compose for services)

### Open MySQL container
```bash
docker exec -it mysql8-container bash
```

### Connect to MySQL to verify database...
```bash
mysql -uroot -psecret
```
... and YES! NO SPACE after -u and -p options!

### Show databases
```bash
show databases;
```

Then quit MySQL and exit MySQL container:
```bash
quit
```
then:
```bash
exit
```

### Install webpack-encore-bundle
First, connect to PHP74 container:
```bash
docker exec -it php74-container bash
```

Then install with Composer:
```bash
composer require encore
```
Then exit the container:
```bash
exit
```

### Use Node and yarn to install Encore
```bash
docker-compose run --rm node-service yarn install
```

### Compile assets
```bash
docker-compose run --rm node-service yarn dev
```