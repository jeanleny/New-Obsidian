Open ssl is a way to generate key and certificates freely.

You can run it with `openssl`

There's several flags but here the full cmd to generate a key and a certificate for a docker purpose.

openssl req -x509 -nodes -days 365 -subj "/CN=localhost"