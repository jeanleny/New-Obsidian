
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

**image** : sets the image if it exist in local, pull one existing otherwise

**container_name** : Gives a nam to the container

**volumes** : the volumes to set:where to set it in the container

**Depends_on** :
This attribute is used for compose flow.
You can control the order of service startup and shutdown, it is useful if services are closely coupled, and the startup sequence impacts the application's functionality.
If your application needs to access the database and both services are started with docker compose up,
there is a chance this will fail since the application service might start before the database service and won't find a database able to handle its SQL stateme nts.

**networks** : The networks used by the container, in this case the inception network that is connected with everycontainer.

**env_files** : the environment file.



*Volumes part* : 
the name
**driver** : The driver that should be used, in this case local are the local folder.
**driver_opts** : specifies a list of options as key-value to pass thhe driver for this volume. 
-  type is not necesary in this case
-  o is for options, in this case bind.
-  device which is the actual host path.

*Network part* : 
the name
**driver** : the type of connection used.