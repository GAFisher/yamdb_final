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
Workflow состоит из четырёх шагов:
1. Тестирование проекта.
2. Сборка и публикация образа.
3. Автоматический деплой.
4. Отправка уведомления в персональный чат.

Добавьте в Secrets GitHub Actions переменные окружения: 
* DOCKER_USERNAME и DOCKER_PASSWORD - для загрузки и скачивания образа с Docker Hub;
* HOST, USER, SSH_KEY, PASSPHRASE - для подключения к удалённому серверу;
* DB_ENGINE, DB_NAME, POSTGRES_USER, POSTGRES_PASSWORD, DB_HOST и DB_PORT - для работы базы данных; 
* TELEGRAM_TO и TELEGRAM_TOKEN - для отправки уведомлений в Телеграм. 


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

### Запуск проекта 
1. Выполните по очереди команды:
```
docker-compose exec web python manage.py makemigrations user
docker-compose exec web python manage.py makemigrations reviews
docker-compose exec web python manage.py migrate
```
* Выполните команду для заполнения базы данными:  
```
docker-compose exec web python manage.py import_csv_to_orm
```
* Создайте суперпользователя: 
```
docker-compose exec web python manage.py createsuperuser
```
* Выполните команду для сбора статических файлов:
```
docker-compose exec web python manage.py collectstatic --no-input
```
* Создайте дамп (резервную копию) базы:
```
docker-compose exec web python manage.py dumpdata > fixtures.json 
```
2. Проект будет доступен по адресу `http://<ipбоевогосервера>/`.
3. Документация будет доступна по адресу `http://<ipбоевогосервера>/redoc/`. В документации описано, как должен работать ваш API. Документация представлена в формате Redoc.

### Команда разработчиков
[Витас Вакаускас](https://github.com/Qerced)
[Виталий Асташкевич](https://github.com/Vitalino13/)
[Галина Фишер](https://github.com/GAFisher)
