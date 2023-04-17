# CI и CD проекта YaMDb
![example event parameter](https://github.com/GAFisher/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg?event=push)
### Описание
Проект YaMDb собирает отзывы пользователей на произведения. Произведения делятся на категории, такие как «Книги», «Фильмы», «Музыка».

В проекте с помощью Continuous Integration и Continuous Deployment реализованы: 
* автоматический запуск тестов,
* обновление образов на Docker Hub,
* автоматический деплой на боевой сервер при пуше в главную ветку main.

### Начало работы
1. Клонируйте репозиторий на локальную машину.
2. Создайте и активируйте виртуальное окружение:
```
python3 -m venv venv
source venv/bin/activate
```
2. Установите зависимости из файла requirements.txt:
```
python3 -m pip install --upgrade pip
pip install -r requirements.txt
```
### Подготовка репозитория на GitHub
Добавьте в Secrets GitHub Actions переменные окружения: 
* DOCKER_USERNAME и DOCKER_PASSWORD - для 

* DB_ENGINE, DB_NAME, POSTGRES_USER, POSTGRES_PASSWORD, 

### Подготовка сервера 
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
5. Проект будет доступен по адресу: `http://<ipбоевогосервера>`

Workflow состоит из четырёх шагов:
1. Тестирование проекта.
2. Сборка и публикация образа.
3. Автоматический деплой.
4. Отправка уведомления в персональный чат.

Документация будет доступна по адресу `http://<ipбоевогосервера>/redoc/` после того, как вы запустите проект. В документации описано, как должен работать ваш API. Документация представлена в формате Redoc.
