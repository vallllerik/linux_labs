# Курс "Основы работы с сетевыми операционными системами"

# Список заданий
- [X] На серверах rrobin, web1, web2 установить nginx.
- [X] На серверах web1, web2 Nginx должен работать по порту 8080 и отдавать кастомную страницу, зайдя на которую можно понять на каком сервере вы находитесь.
- [X] На сервере rrobin Nginx должен обеспечить балансировку нагрузки серверов web1 и web2 в режиме round-robin. Вес каждого сервера одинаковый.
- [X] Установка и настройка всего ПО должна быть обеспечена Ansible-сценарием.
- [x] Все файлы по этому заданию выложить в Github и написать ReadMe со скринами работоспособности и инструкцию по запуску вашего Ansible-сценария

P.S. Использовать по максимуму переменные. Переменные должны называться ЛОГИЧНО Все конфиги на серверах должны генерироваться через templates

![photo_2023-04-11_16-20-04](https://user-images.githubusercontent.com/114299007/231192748-7706abf7-870b-46b6-a68e-e3b8e256a9c9.jpg)

Ход выполнения работы
---------------------------
+ Скачаем все необходимые данные. Открывает Vagrantfile и ставим нужные machine и ip, который принадлежит каждому серверу.

![Снимок экрана от 2023-04-11 12-28-11](https://user-images.githubusercontent.com/114299007/231192619-30f95d51-7838-44fe-ab37-19e24acfce6a.png)

+ Открываем и редактируем inventory-чтобы ansible мог управлять нашими хостами.
+ Открываем и редактириуем ansible.cfg-чтобы указать наш inventory файл со всеми нужными нам параметрами(более подробно [ansible documention](https://docs.ansible.com/ansible/2.6/reference_appendices/config.html)
+ Создаем папку(roles) где будут хранится все playbooks и конифуграции для наших webservers и backend-server.
    - Роль balancer:
        * Создаем папку tasks, а в ней playbook, который установить последнюю версию nginx, обновит и запустить его.
        * Создаем папку templates, где будет хранится необходимая конфигурация для nginx - nginx.conf.j2 (указываем разрешение j2, так как у нас несколько серверов, и делаем присваивание через цикл)
        * Создадим папку vars, где будут хранится все переменные которые испольюзуются во многих файлах и могут изменится при необходимости. Тем самым мы автоматизируем весь процесс. 
    - Роль webservers:
        * Cоздаем папку tasks, а в ней playbook, который установить последнюю версию nginx, обновит и запустить его.
        * Создаем папку templates, где будет хранится необходимая конфигурация для nginx - nginx.conf, а так же index.html.j2 - код нашей веб-странички
        * Создадим папку vars, где будут хранится все переменные которые испольюзуются во многих файлах и могут изменится при необходимости. Тем самым мы автоматизируем весь процесс. 
    - Роль selinux-disable:
        * Меняем в конфигурационном файле на `SELINUX=disabled`
        * в tasks используем модуль selinux для обеспечения идемпотентности (свойство объекта или операции при повторном применении операции к объекту давать тот же результат, что и при первом)
+ Запускаем nginx.yml, в котором прописано к каким hosts принадлежат папки
+ Заходим в браузер. Вбиваем адреса, которые мы указывали в inventory - webserver и порт, который указывали в vars. Если они показываю сайт, то круто.

--------------------------

+ Забиваем адрес - backend-server. Если при каждому обновлении он показывает сайт web1, а потом web2, поочередно, следовательно мы сделали все правильно.

![Снимок экрана от 2023-04-07 11-31-15](https://user-images.githubusercontent.com/114299007/231191724-83532910-55c2-4b46-bed2-06a44c680ac4.png)

![Снимок экрана от 2023-04-07 11-31-21](https://user-images.githubusercontent.com/114299007/231191762-fde4dd91-bee5-47e8-8143-98581a294442.png)

---------------------------