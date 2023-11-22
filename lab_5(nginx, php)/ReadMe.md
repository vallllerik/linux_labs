*1) Webserver*

1. устанавливаем nginx
2. Меняем в /etc/php-fpm.d/www.conf user и group на nginx
3. Там же меняем listen_allowed clients на 127.0.0.1:9000
4. Запускаем 
systemctl start php-fpm.service
systemctl enable php-fpm.service
5. Добавляем новый location в /etc/nginx/nginx.conf 
------------------------------------
location ~ .php$ {
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_index index.php;
        include fastcgi_params;
        fastcgi_pass 127.0.0.1:9000;
        try_files $uri =404;
        }
------------------------------------
добавляем в основной блок server строчку "index index.php", комментируем или удаляем строчку "listen  [::]:80"
6. Создаем файлик index.php: nano /usr/share/nginx/html/index.php
7. Отключаем SeLinux (меняем enabled на disabled)
8. Запускаем Nginx 
systemctl start nginx
systemctl enable nginx


*2) PG*
 
1. устанавливаем PostgreSQL
2. В nano /var/lib/pgsql/14/data/postgresql.conf
    - добавляем строку ip-address server
    --------------------------------
    listen_addresses = '*'
    --------------------------------
    nano /var/lib/pgsql/14/data/pg_hba.conf
    --------------------------------
    host    all       all        192.168.11.90/24      azfscram-sha-256
    --------------------------------
4. Запускаем PostgreSQL 
    systemctl start postgresql-14.service 
    systemctl enable postgresql-14
5. Скачиваем и распаковываем БД файл 
6. Ставим пароль на БД
7. Отключаем SeLinux (меняем enabled на disabled)
8. Restart PG и Web
