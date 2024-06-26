## Описание проекта ***kittygram***

Сайт с возможностью публикации фотографий котов и их достижений.

### Стек технологий

- Python 3.9
- Django 3.2.3
- Django REST framework 3.12.4
- Nginx
- Docker compose

### Запуск проекта из образов с Docker Hub

1. Создаём папку проекта `kittygram` и переходим в нее:

    ```bash
    mkdir kittygram
    cd kittygram
    ```

2. В папку проекта копируем (или создаём) файл `docker-compose.production.yml` и запускаем его:

    ```bash
    sudo docker compose -f docker-compose.production.yml up
    ```

    Произойдет скачивание образов, создание и включение контейнеров, создание томов и сети.

### Запуск проекта из исходников GitHub

1. Клонируем себе репозиторий:

    ```bash
    git clone git@github.com:octrow/kittygram_final.git
    ```

2. Выполняем запуск:

    ```bash
    sudo docker compose -f docker-compose.yml up
    ```

    После запуска: Миграции, сбор статистики

###### Миграции и сбор статики

После запуска нужно выполнить сбор статистики и миграцию для бэкенда. Статистика фронтенда собирается во время запуска контейнера, после чего он останавливается.

```bash
sudo docker compose -f [имя-файла-docker-compose.yml] exec backend python manage.py migrate
sudo docker compose -f [имя-файла-docker-compose.yml] exec backend python manage.py collectstatic
sudo docker compose -f [имя-файла-docker-compose.yml] exec backend cp -r /app/collected_static/. /static/static/
```

## Описание переменных окружения

Ниже пример файла `.env` с переменными окружения, необходимыми для запуска приложения:

```bash
POSTGRES_DB=kittygram
POSTGRES_USER=kittygram_user
POSTGRES_PASSWORD=kittygram_password
DB_NAME=kittygram
DB_HOST=db
DEBUG=False
SECRET_KEY=django_secret_key_example
```

## Остановка оркестра контейнеров

```bash
sudo docker compose -f docker-compose.yml down
```
