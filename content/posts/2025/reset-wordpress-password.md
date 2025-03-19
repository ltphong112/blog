---
title: 'Reset Wordpress Password'
date: 2025-03-18T15:49:25-07:00
draft: false
tags: ["wordpress", "password", "docker"]
cover:
  image: "/images/wordpress-password-reset.webp"  # Path to your image
  alt: ""  # Alt text for the image
  caption: ""
  hidden: true  # Set to true if you don't want to show the image in the
  hiddenInList: false  # Show the image in the post list
  hiddenInSingle: true  # Hide the image in the single post view
---
You can reset your WordPress admin password in a Docker environment using WP-CLI. Here are the steps:

Access your Docker container:
```
docker exec -it <container_name> bash
```

Navigate to your WordPress directory:
```
cd /var/www/html
```

List the users:
```
wp user list
```

Update the password for the desired user:
```
wp user update <user_id> --user_pass=<new_password>
```

Exit the container:
```
exit
```

In case there is an error like ```wp command not found```, WP-CLI isn't installed in your Docker container. Let's install it:

Download WP-CLI:
```
curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar

```

Make the file executable:
```
chmod +x wp-cli.phar
```

Move it to a directory in your PATH:
```
sudo mv wp-cli.phar /usr/local/bin/wp
```

Verify the installation:
```
wp --info
```

If you prefer to use Docker Compose, you can add WP-CLI to your docker-compose.yml file:
```
version: '3.8'

services:
  wordpress:
    image: wordpress:latest
    ports:
      - "8000:80"
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: exampleuser
      WORDPRESS_DB_PASSWORD: examplepass
      WORDPRESS_DB_NAME: exampledb

  db:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: examplepass
      MYSQL_DATABASE: exampledb
      MYSQL_USER: exampleuser
      MYSQL_PASSWORD: examplepass

  wpcli:
    image: wordpress:cli
    volumes:
      - .:/var/www/html
    depends_on:
      - wordpress
```

After updating your docker-compose.yml, you can run WP-CLI commands like this:
```
docker-compose run --rm wpcli wp <command>
```

This should help you get WP-CLI up and running in your Docker environment.
