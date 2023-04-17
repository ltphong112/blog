# Install Jellyfin With Docker Compose


To install Jellyfin using Docker Compose, you will need to have Docker and Docker Compose installed on your system. If you don't already have these tools installed, you can follow the instructions provided by Docker to install them on your system.

Once you have Docker and Docker Compose installed, you can use the following steps to install Jellyfin using Docker Compose:

Create a new directory for your Jellyfin installation, and navigate to that directory in your terminal.
Create a new file called docker-compose.yml in your Jellyfin directory, and add the following contents to the file:

```
version: '3.7'
services:
  jellyfin:
    image: jellyfin/jellyfin
    container_name: jellyfin
    restart: always
    ports:
      - 8096:8096
      - 8920:8920
    volumes:
      - /path/to/your/config:/config
      - /path/to/your/media:/media
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Your/Timezone
      - UMASK_SET=022
```

Replace /path/to/your/config and /path/to/your/media with the actual paths on your system where you want to store your Jellyfin configuration and media files, respectively.
Replace Your/Timezone with your actual timezone (e.g., "America/New_York").
Save the docker-compose.yml file and close it.
Run the following command to start Jellyfin using Docker Compose:

```
docker-compose up -d

```

This will download the Jellyfin Docker image and start a new Jellyfin container using the configuration specified in your docker-compose.yml file.

Once the container is running, you can access the Jellyfin web interface by opening a web browser and navigating to http://localhost:8096.
That's it! You should now have a working Jellyfin installation running in a Docker container on your system.

Note: The above instructions are just a basic example of how to install Jellyfin using Docker Compose. There are many other options and configurations that you can specify in your docker-compose.yml file to customize your Jellyfin installation. For more information, you can refer to the Jellyfin documentation and the Docker Compose documentation.

