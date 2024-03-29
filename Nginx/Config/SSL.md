
# 1️⃣Use certbot to get ssl_certificate and ssl_certificate_key
# 2️⃣Use this command to generate dhparam
```
sudo openssl dhparam -out /etc/ssl/certs/dhparam.pem 2048
```
# 3️⃣Create and Open to add this content to /etc/nginx/conf.d/ssl.conf

```
server {
    listen 80;
    listen [::]:80;
    server_name your_server_ip;
    return 301 https://$host$request_uri;
}

server {
    listen 443 default_server http2 ssl;
    listen [::]:443 default_server http2 ssl;

    server_name your_domain;

    ssl_certificate /etc/letsencrypt/live/your_domain;/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/your_domain;/privkey.pem;
    ssl_dhparam /etc/ssl/certs/dhparam.pem;

    ########################################################################
    # from https://cipherlist.eu/                                            #
    ########################################################################

    ssl_protocols TLSv1.3;# Requires nginx >= 1.13.0 else use TLSv1.2
    ssl_prefer_server_ciphers on;
    ssl_ciphers EECDH+AESGCM:EDH+AESGCM;
    ssl_ecdh_curve secp384r1; # Requires nginx >= 1.1.0
    ssl_session_timeout  10m;
    ssl_session_cache shared:SSL:10m;
    ssl_session_tickets off; # Requires nginx >= 1.5.9
    ssl_stapling on; # Requires nginx >= 1.3.7
    ssl_stapling_verify on; # Requires nginx => 1.3.7
    resolver 8.8.8.8 8.8.4.4 valid=300s;
    resolver_timeout 5s;
    # Disable preloading HSTS for now.  You can use the commented out header line that includes
    # the "preload" directive if you understand the implications.
    #add_header Strict-Transport-Security "max-age=63072000; includeSubDomains; preload";
    add_header X-Frame-Options DENY;
    add_header X-Content-Type-Options nosniff;
    add_header X-XSS-Protection "1; mode=block";
    ##################################
    # END https://cipherlist.eu/ BLOCK #
    ##################################
}
```