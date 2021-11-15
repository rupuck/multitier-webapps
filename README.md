# DevOps Technical Test

This repository created as a technical test for DevOps position at **Awal Mula**. 
The Task :
> 1. Design an architecture for Multi-tier web apps with docker or kubernetes.  
> 2. Build and Deploy the application in local environment. 
## About the Project
For this test, I will use docker to create multi-tier web apps using php with laravel framework that have connection with MySql database and Redis. The web server will be handled by Nginx.
## Technical Specification

 - VirtualBox v.6.1.26
 - CentOS v,8.4.2105 64 bit
 - Docker v.20.10.8
 - Docker Compose v.1.26.0
 

## Architecture
The application architecture will be 3-tier web apps but Laravel will handle both the front-end and the back-end.
![enter image description here](https://i.imgur.com/ixBcH7O.png)
 ## Services

1. App - Laravel v.8.62.0
2. Web Server - Nginx:alpine
3. DB - Mysql v.5.7.22
4. Redis v.6.2
```
docker/
├── App
│   ├── Laravel/
│   │   └── Dockerfile
├── Web Server/
│   ├── Nginx/
│   │   └── app.cnf
│   │   └── Dockerfile_Nginx
├── DB
│   ├── MySQL/
├── Redis
└── docker-compose.yml
```

 **List Container**
 
![Docker Image](https://i.imgur.com/qUX2n1F_d.webp?maxwidth=760&fidelity=grand)

 **Start Services**
 
 ![enter image description here](https://i.imgur.com/POHkxTK.jpg)

## Docker Hub Images

I have uploaded the docker images to docker hub that can be accessed here
https://hub.docker.com/repository/docker/andreasp9605/awalmula-technicaltest/general

## Config
nginx configuration files
```
server{
   listen 80;
   index index.php index.html;
   error_log  /var/log/nginx/error.log;
   access_log /var/log/nginx/access.log;
   root /var/www/public;
   location ~ \.php$ {
       try_files $uri =404;
       fastcgi_split_path_info ^(.+\.php)(/.+)$;
       fastcgi_pass app:9000;
       fastcgi_index index.php;
       include fastcgi_params;
       fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
       fastcgi_param PATH_INFO $fastcgi_path_info;
   }
   location / {
       try_files $uri $uri/ /index.php?$query_string;
       gzip_static on;
   }
}

```
