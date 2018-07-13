# WSL Ubuntu
/etc/nginx/nginx.conf
~~~bat
http {
    ...
    fastcgi_buffering off;
    ...
}
~~~

/etc/nginx/site-enabled 
~~~bat
server {
        listen 127.0.0.1:80 default_server;
        ......
        
        location ~ \.php$ {
        #       include snippets/fastcgi-php.conf;
        #
        #       # With php-fpm (or other unix sockets):
        #       # With php-cgi (or other tcp sockets):
        #       fastcgi_pass unix:/run/php/php7.2-fpm.sock;
                fastcgi_pass 127.0.0.1:9000;
                fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
                 include fastcgi_params;
        }
        
        }
~~~

/etc/php/7.0/fpm/pool.d/www.conf
~~~bat
pm = dynamic
pm.start_servers = 1
pm.min_spare_servers = 1
pm.max_children = 5
pm.max_spare_servers = 5

listen = 127.0.0.1:9000;
~~~
