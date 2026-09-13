```nginx
events {}

http {
    server {
	listen 80;
        server_name localhost lperis.42.fr;
	return 403;
    }

    server {
        listen 443 ssl;
        server_name localhost lperis.42.fr;

        ssl_certificate     /etc/nginx/certs/server.crt;
        ssl_certificate_key /etc/nginx/certs/server.key;

	root /var/www/html;

	index index.php index.html;

        location / {
            try_files $uri $uri/ /index.php?$args;
        }

	location ~ \.php$ {
            fastcgi_pass wordpress:9000;

            fastcgi_index index.php;

            include fastcgi_params;

            fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        }
    }
}
```
**http** : all the web traffic config goes inside this block.

**Server** : These are blocks that handle certain types of connection.
In the first block it manages the logic of all port 80 incoming connections.

**listen** : tells nginx to listen for connections on port 80 which is the default http port.
*listen 443 ssl* : 

**server_name** : defines the domain names where you can access the nginx server. nginx ignore the others.

**ssl_certificate** : The path to the certificate
**ssl_certificate_key** : the path to the ssl key

**index** :  index.php index.html; These are the files used when a request comes in for a directory.
which means, if a request is like this :
`https://localhost/` there is no filename is that URL.
So the index config serves index.php or index.html to PHP_FM which is where wordpress puts the website page.

**location** : this block handles logic for certain files.
*location /* handles EVERY request by default whith the "/" flag.
"~" means match using a regular expression
".php" if for URL ending in .php

**try_files** `$uri $uri / /index.php?$args;` try to serve the request in the order.
NGINX has its own set of built-in variables and they all starts with $.
$uri is the path of the URL without the domain and without the query string.
$args passes the query string along. Wordpress needs it.
```
Full URL:   https://localhost/wp-content/style.css?ver=1.0
$uri = /wp-content/style.css
```

THe whole fastcgi is here because nginx cannot execute php so PHP_FPM does it with the fastCGI protocol.

**fastcgi_pass** is a request to PHP_FPM using the FastCGI protocol.
9000 is the port where PHP_FPM listens.

**fastcgi_index** same as the index config used before but for fastcgi.

**include** : load a file that contains fastCGI variables like REQUEST_METHOD, QUERY_STRING SERVER_NAME.
PHP_FPM needs it.

**fastcgi_param** : the include used before.
We store the nginx built-in variable inside suche as 
- `$document root` expands to the root directive.
- `$fastcgi_script_name` the php file requested. Here is "index.php"
This the params PHP_FPM needs to work.
