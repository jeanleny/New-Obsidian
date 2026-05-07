
Here is my Inception docker compose

```yaml
services :
  nginx :
    ports :
      - "443:443"
      - "80:80"
    build : ./nginx
    image : nginx:1.0
    container_name : nginx
    volumes:
    - wordpress_data:/var/www/html
    depends_on:
      - wordpress
    networks :
      - inception

  mariadb :
    build : ./mariadb
    image : mariadb:1.0
    container_name : mariadb
    env_file: .env
    volumes :
      - mariadb_data:/var/lib/mysql
    networks :
      - inception

  wordpress :
    build : ./wordpress
    image : wordpress:1.0
    container_name : wordpress
    env_file: .env
    volumes :
      - wordpress_data:/var/www/html
    networks : 
      - inception

volumes :
  wordpress_data:
    driver : local
    driver_opts :
      type : none
      device : /home/lperis/data/wordpress
      o : bind
  mariadb_data:
    driver : local
    driver_opts :
      type : none
      o : bind
      device : /home/lperis/data/mariadb

networks :
  inception :
    driver : bridge

```

**Services** : Where all the containers are defined. It contains each containers with there own options.

**ports** : syntax is like HOST_PORT:CONTAINER_PORT
HOST_PORT :
This defines the port number on your host machine where you want to receive traffic.
CONTAINER_PORT :
The port number within the container that's listening for connections.

**build** : Build the image from the dockerfile in the repo.


