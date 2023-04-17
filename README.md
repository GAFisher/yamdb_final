# CI и CD проекта YaMDb
## Описание
Проект YaMDb собирает отзывы пользователей на произведения. Произведения делятся на категории, такие как «Книги», «Фильмы», «Музыка».

В проекте с помощью Continuous Integration и Continuous Deployment реализованы: 
* автоматический запуск тестов,
* обновление образов на Docker Hub,
* автоматический деплой на боевой сервер при пуше в главную ветку main.

## Технологии
![example event parameter](https://github.com/GAFisher/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg?event=push)

## Подготовка сервера к работе
1. Остановите службу nginx: 
```
sudo systemctl stop nginx
```
2. Установите docker:
```
sudo apt install docker.io 
```
3. Установите docker-compose: 
```
curl -SL https://github.com/docker/compose/releases/download/v2.17.2/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```
Проверить успешность установки:
```
docker-compose --version
```
4. Скопируйте файлы `docker-compose.yaml` и `nginx/default.conf` на сервер в home/<ваш_username>/docker-compose.yaml и home/<ваш_username>/nginx/default.conf соответственно.
5. Проект будет доступен по адресу: `http://<ipбоевогосервера>:8000`

Workflow состоит из четырёх шагов:
1. Тестирование проекта.
2. Сборка и публикация образа.
3. Автоматический деплой.
4. Отправка уведомления в персональный чат.

## Запуск проекта
Аааааааа
