# Docker - NGINX - MYSQL -DJANGO
- nginx server
- mysql server
- multi site (inlclude django template)
- nginx virtual host config file will be created

**install nginx:**

run following command
>>$ docker network create nginx-proxy

>>$ cd nginx-proxy

>>$ sudo docker-compose up -d


**install mysql:**
>>$ docker network create mysql-network


set mysql environments in /envs/mysql.env file

>>$ cd mysql
>>$ docker-compose up -d

every sql file will run in mysql/sql folder


make your database and mysql user , run following command:

>>$ docker exec -it mysql /bin/bash
>>$ mysql -u root -p
<br>

>> CREATE DATABASE IF NOT EXISTS < DB_NAME > CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;

>> CREATE USER IF NOT EXISTS '< DB_USER >'@'%' IDENTIFIED BY '< DB_PASS >';

>> GRANT ALL PRIVILEGES ON < DB_NAME >.* TO '< DB_USER >'@'%';
>> FLUSH PRIVILEGES;
>> exit;

>>$ exit


set app1/requirements.txt
<br>
set app1/web/web/settings_local.py , there is an example there
>>DEBUG = True
>>DEVEL = True
>>DB_NAME = ""
>>DB_USER = ""
>>DB_PASS = ""
>>BASE_URL = "http://127.0.0.1:8000"
>>LOCAL_ALLOWED_HOSTS = ['*']
>>DB_HOST="mysql"  // should be "mysql"



set app1 environment in /envs/app1.env


>>VIRTUAL_HOST= < domain >
>>VIRTUAL_PORT= 3000  // if you change this you sould change app1/docker-compose  expose "3000" the same
>>LETSENCRYPT_HOST= < domain >
>>LETSENCRYPT_EMAIL= < your-email@domain >

**install django app:**
(django , uwsgi)
>>$ cd app1

>>$ docker-compose up -d


>>$ docker exec -it app1 /bin/bash



set host (edit etc/hosts file)
<br>
127.0.0.1   < domain >
