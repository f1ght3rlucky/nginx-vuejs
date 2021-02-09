```
server {
    listen	 80;
    listen [::]:80;
    server_name  yourdomain.com www.yourdomain.com;
    root   /var/www/FOLDER_NAME;
    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.html;
    }
    error_page 404 /404.html;
    error_page 500 502 503 504 /50x.html;

    location = /50x.html {
        root /var/www/FOLDER_NAME;
    }

    location ~ \.php$ {
        try_files $uri =404;
        fastcgi_pass unix:/var/run/php-fpm/php-fpm.sock;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
}
```
