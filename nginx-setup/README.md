# nginx-setup
nginx basic setup (gzip, proxy pass, etc)

/etc/nginx/sites-available/default
```
server {
        
        # Allow both HTTP and HTTPS
        listen 80 default_server;
        listen [::]:80 default_server;
        listen 443 ssl http2 default_server;
        listen [::]:443 ssl http2 default_server;
        server_name iothardware.cc www.iothardware.cc;
        
        include snippets/ssl-iothardware.cc.conf;
        include snippets/ssl-params.conf;

        if ($host = 'iothardware.cc' ) {
                rewrite  ^/(.*)$  https://www.iothardware.cc/$1  permanent;
        }
        
        root /var/www/html;

        # Add index.php to the list if you are using PHP
        index introduction.html;

        location /.well-known {
                allow all;
        }
        
        # error page not found handling
        error_page 404 = @default;

        location @default {
                rewrite ^/.* / permanent;
        }
        
        # Need to change to io("/", {path:"/lorademoSocket"}) at client-side
        location /lorademoSocket/ {
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header Host $http_host;
                proxy_set_header X-NginX-Proxy true;

                proxy_pass http://localhost:8080/socket.io/;
                proxy_redirect off;

                proxy_http_version 1.1;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection "upgrade";
        }
        
        location /lorademo/ {
                # First attempt to serve request as file, then
                # as directory, then fall back to displaying a 404.
                #try_files $uri $uri/ =404;
                proxy_http_version 1.1;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection 'upgrade';
                proxy_set_header Host $host;
                proxy_cache_bypass $http_upgrade;

                proxy_pass http://localhost:8080/;
                proxy_redirect off;
                rewrite ^/lorademo/(.*)$ /$1 break;

        }
}
```
/etc/nginx/nginx.conf

```
http {

        gzip on;
        gzip_disable "msie6";
        
        gzip_vary on;
        gzip_proxied any;
        gzip_comp_level 6;
        gzip_buffers 16 8k;
        gzip_http_version 1.1;
        gzip_min_length 256;
        gzip_types text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript;

}
```
        
        
        

        
        

        
