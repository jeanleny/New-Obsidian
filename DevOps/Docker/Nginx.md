Nginx is a high performance web server with a reverse proxy that handle well the web trafic.

It is known for his low ressource use.

## Configuration

Nginx works with .conf files that sets up your server.
Example :
``` .conf
events {}
http {
	server {
		listen 80;
		server_name localhost;
		
		location / {
			return 200 "Par exemple hein"
		}
	}
}
```

This is a classic http server were we can connect with a browser with http://localhost

Nginx configs are located in the **/etc** folder.

To launch this specific specific folder, we need to add the path with the **-c** flag.
``nginx -c /path/to/nginx.conf

By default the nginx config will launch as a [[Daemon]]
To avoid this use the **-g "daemon off;"**
``nginx -c /path/nginx.conf -g "daemon off;"

