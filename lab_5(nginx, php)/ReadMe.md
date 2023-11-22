# WEB

1. устанавливаем nginx
2. Меняем в /etc/php-fpm.d/www.conf user и group на nginx
3. Там же меняем listen_allowed clients на 127.0.0.1:9000
4. Запускаем 
systemctl start php-fpm.service
systemctl enable php-fpm.service
5. Добавляем новый location в /etc/nginx/nginx.conf 
------------------------------------
 - `location ~ .php$ {
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_index index.php;
        include fastcgi_params;
        fastcgi_pass 127.0.0.1:9000;
        try_files $uri =404;
        }`
------------------------------------
6. добавляем в основной блок server строчку "index index.php", комментируем или удаляем строчку "listen  [::]:80"
7. Создаем файлик index.php: nano /usr/share/nginx/html/index.php
8. Отключаем SeLinux (меняем enabled на disabled)
9. Запускаем Nginx 
`systemctl start nginx
 systemctl enable nginx`


# PG
 
1. устанавливаем PostgreSQL
2. В nano /var/lib/pgsql/14/data/postgresql.conf

    ---------------------------------
    -  добавляем строку ip-address server
    - listen_addresses = '*'
    - host    all       all        192.168.11.90/24      azfscram-sha-256
    --------------------------------

3. Запускаем PostgreSQL 
    systemctl start postgresql-14.service 
    systemctl enable postgresql-14
4. Скачиваем и распаковываем БД файл 
5. Ставим пароль на БД
6. Отключаем SeLinux (меняем enabled на disabled)
7. Restart PG и Web

