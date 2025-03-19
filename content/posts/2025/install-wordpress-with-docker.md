---
title: "Install Wordpress With Docker"
date: 2025-03-17T13:27:19-07:00
url: /install-wordpress-with-docker/
tags:
  - linux
  - docker
  - wordpress
  - apache
  - mariadb
cover:
  image: "/images/wordpress-with-docker.png"  # Path to your image
  alt: ""  # Alt text for the image
  caption: ""
  hidden: true  # Set to true if you don't want to show the image in the
  hiddenInList: false  # Show the image in the post list
  hiddenInSingle: true  # Hide the image in the single post view
---
Here are the steps to install WordPress under Docker, including setting up a directory for file backups and adding an uploads.ini file to customize PHP settings.

Step 1: Create a Directory for Your Project

Open a terminal and create a directory for your WordPress project:
```
mkdir wordpress-docker
cd wordpress-docker
```

Step 2: Create a docker-compose.yml file

Create a docker-compose.yml file in the wordpress-docker directory with the following content:
```
version: '3.8'  # Specifies the Docker Compose file format version

services:
  wordpress:
    image: wordpress:latest
    container_name: wordpress
    ports:
      - "8000:80"
    volumes:
      - ./html:/var/www/html
      - ./uploads.ini:/usr/local/etc/php/conf.d/uploads.ini
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: wordpress
      WORDPRESS_DB_NAME: wordpress
    restart: unless-stopped

  db:
    image: mariadb:latest
    container_name: wordpress_db
    volumes:
      - db_data:/var/lib/mysql
    environment:
      MYSQL_ROOT_PASSWORD: somewordpress
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: wordpress
    restart: unless-stopped

volumes:
  db_data:
```

Step 3: Create the uploads.ini File

Create an uploads.ini file in the wordpress-docker directory with the following content:
```
file_uploads = On
memory_limit = 64M
upload_max_filesize = 64M
post_max_size = 64M
max_execution_time = 600
```

Step 4: Start the Docker Containers

Run the following command to start the Docker containers:
```
docker-compose up -d
```

Step 5: Access Your WordPress Site

Open your web browser and navigate to http://localhost:8000 to complete the WordPress installation.

Step 6: Backup Your Files

Ensure that your WordPress files are backed up by mapping the ./html directory to /var/www/html in the Docker container. This way, all your WordPress files will be stored in the html directory on your host machine.

Explanation of version: '3.8'
- Compatibility: Version 3.8 is compatible with Docker Engine 19.03.0 and above.
- Features: It includes features like support for secrets, configs, and improved networking options.

You can change the version number if needed, but it depends on the features you require and the version of Docker Engine you are using. For example, you can use version 3.7 by changing the first line to:
```
version: '3.7'
```
Make sure to check the Docker Compose documentation for the specific features and compatibility of each version.


