# Lab_6 Dockerfile
-----------------------------------------------------------------------
### Задание

1. Создайте свой кастомный образ nginx на базе alpine. После запуска nginx должен отдавать кастомную страницу (достаточно изменить дефолтную страницу nginx)

2. Собранный образ необходимо запушить в docker hub и дать ссылку на ваш репозиторий.

### Задание со *:

1. Создайте кастомные образы nginx и php, объедините их в docker-compose.

2. После запуска nginx должен показывать php info.

3. Все собранные образы должны быть в docker hub.


#### Let's go

1. Создаем свой docker image на базе alpine

- Создаем отдельную папку и в ней 2 файла:

  - Dockerfile (во вложении)
    - Команды которые могут понадобиться: 
        - docker ps
        - docker ps -a
        - docker run -d -p port:port container_name
        - docker stop container_name
        - docker logs container_name - вывод логов контейнеров
        - docker inspect container_name - информация по запущенному контейнеру 
        - docker build -t dockerhub_login/reponame:ver
        - docker push/pull
        - docker exec -it container_name bash

  - Файл index.html с любым содержимым

2. Собираем наш образ командой ```docker build -t dockerhub_login/reponame:ver .```

3. Далее запускаем наш контейнер ```docker run -d -p port:port container_name```

- Видим наш образы можно с помощью ```docker image``` и наши контейнеры ```docker ps / ps -a```

4. Пушим в docker hub 

- Выполняем  ```docker login```, и вводим логин и пароль от аккаунта из docker-hub:

- Push ```docker push dockerhub_login/reponame:ver```:

- Затем в браузере откройте страницу
   " http://localhost:8080 " .

## Задание со *:

1. Создайте кастомные образы nginx и php, объедините их в docker-compose

- Выполняем:
```
docker-compose up --build   
- Затем в браузере откройте страницу
   " http://localhost:8080 " .
```
