# InferiorGold_microservices
InferiorGold microservices repository
# ДЗ по docker-3
 - Загружено приложение reddit-microservices;
 - Реализовано через Dockerfile сборка и разворачивание трех приложений "comment" "post-py" "ui";
 - Дополнительно оптимизирована сборка приложения post-py (обновлены версии компонентов и отключен лог так как мешало запуску, требуется привлечение разработчика для обновления кода) тем самым убраны при сканировании в 0 уязвимости приложения;
 - Оптимизировано использование базовых образов тем самым уменьшены размеры докер образов в десятки раз;
 - Дополнительно запускаем mongodb с подключением локального volme для хранения сообщений;

 #### Задания со ⭐
1. Запуск контейнеров с другими алиасами и передача данных с помощью переменных.
```
docker run -d --network=reddit --network-alias=post_db_01 --network-alias=comment_db_01 mongo:latest
docker run -d --network=reddit -e POST_DATABASE_HOST=post_db_01 -e POST_DATABASE=posts_01 --network-alias=post_01 vvakhitov/post:1.0
docker run -d --network=reddit -e COMMENT_DATABASE_HOST=comment_db_01 -e ENV COMMENT_DATABASE=comments_01 --network-alias=comment_01 vvakhitov/comment:1.0
docker run -d --network=reddit -e  POST_SERVICE_HOST=post_01 -e COMMENT_SERVICE_HOST=comment_01 -p 9292:9292 vvakhitov/ui:1.0
```
2. Образ на основе alpine **Dockerfile.01**.
```
FROM alpine
RUN apk update --no-cache \
    && apk add --no-cache ruby ruby-dev ruby-bundler build-base \
    && gem install bundler --no-rdoc --no-ri \
    && rm -rf /var/cache/apk/*
```
собираем:
```
docker build -t vvakhitov/ui:3.0 ./ui --file ui/Dockerfile.01
```
сравниваем:
```
REPOSITORY            TAG                 IMAGE ID            CREATED             SIZE
vvakhitov/ui        3.0                 1d1f07f71eec        5 minutes ago       228MB
vvakhitov/ui        2.0                 deff8e92e9d2        16 minutes ago      490MB
```



# ДЗ по docker-2
В рамках данного ДЗ:
- Установил docker, docker-compose, docker machine
- Создал свой образ
- Создал docker host
- Зарегистрировался на Docker Hub и загрузил образ в публичное хранилище
