# rpgtables-docker
Containers used to dev the rpgtables project

# How to use
 - Unzip;
 - Create directory `code`, maps to /var/www/app;
 - Create directory `data`, maps to /var/lib/mysql;
 - `chomod -R 0777 data`;
 - If it is the first time
   - `docker-machine create rpgtables`
   - `docker-machine start rpgtables`;
   - `docker-machine env rpgtables`;
   - `eval $(domach env rpgtables)`;
   - `docker-compose build`;
   - `docker-compose up -d`;
 - Use this to enter apache container
   - docker exec -it tables4dmsdocker_php_1 /bin/bash



# What is inside
 - Apache + PHP + PDO-MYSQL
   - port: 80;
   - ServerName: localdev
   - DocumentRoot: /var/www/app/public
 - xDebug
   - port: 9001;
   - idekey: XDEBUG
 - Composer;
 - mySQL
   - port: 3306
