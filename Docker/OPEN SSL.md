Open ssl is a way to generate key and certificates freely.

You can run it with `openssl`

There's several flags but here the full cmd to generate a key and a certificate for a docker purpose.

```bash
mkdir -p /etc/nginx/certs && \
openssl req -x509 -noenc -days 365 \
-newkey rsa:2048 \
-keyout /etc/nginx/certs/server.key \
-out /etc/nginx/certs/server.crt \
-subj "/CN=localhost"
```

**openssl req** is to create a certificate request.

**-x509** is what makes it self signed and no authority certificate is involved

**-noenc** if this option is specified then if a private key is created it will not be encrypted. So no password will be requested to check the key.

**-days 365** By default, the certificate will last 30 days.
This flag can reset it.

**-newkey** rsa:2048 
This will generate a [[RSA]] key pair of a 2048 bits size.
It creates a private key and a public certificate linked to it.

**-keyout** /etc/nginx/certs/server.key
**-out** /etc/nginx/certs/server.crt
Flags to set the certificate and key location.
Important to set niginx certificate.
The server.key is the private key that will never be shared.
The server.crt is the Certificate that is safe to share with other clients.

**-subj "/CN=localhost"**
This is used to avoid the interactive prompts that openssl runs when generating the key.
Since the docker container cannot answer it it important to avoid it.


