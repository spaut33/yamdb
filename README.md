# 💬 [YaMDb - приложение для сбора отзывов](https://yacloud.telfia.com/)
![ci workflow](https://github.com/spaut33/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg) ![PyPI - Python Version](https://img.shields.io/pypi/pyversions/django) ![Django](https://img.shields.io/badge/Django-2.2.19-green) ![DRF](https://img.shields.io/badge/DRF-3.12.4-green) ![Docker](https://img.shields.io/badge/Docker-20.10-lightblue) ![Nginx](https://img.shields.io/badge/Nginx-1.21-lightblue) ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-13.0-lightblue)

Приложение для сбора отзывов пользователей о фильмах, книгах, музыке. Каждое произведение может быть объединено администратором в категории и назначены жанры. Посредством REST API пользователи могут регистрироваться в приложении, авторизироваться, добавлять обзоры, оставлять оценки и комментарии к произведениям.

## Содержание

- [Описание](#-описание)
- [Описание API](#Описание-API)
- [Установка и запуск](#%EF%B8%8F-установка-и-запуск)
- [Использованные технологии](#%EF%B8%8F-использованные-технологии)
- [Лицензия](#%EF%B8%8F-лицензия)
- [Авторы](#-авторы)

## 📖 Описание

Это готовый Docker-образ, содержащий REST API приложение, пользователи которого могут:
- регистрироваться в приложении, получая код подтверждения на свой e-mail
- получать токен для полноценного доступа к API, работа с токенами реализована с помощью библиотеки `SimpleJWT`
- авторизованные пользователи могут изменять свои учетные данные через специальный адрес `/users/me`
- администраторы могут создавать новых пользователей, изменять их учетные данные других пользователей
- пользователи могут запрашивать категории произведений, жанры, произведения, отзывы, комментарии к отзывам
- оставлять отзывы и рейтинг на произведения, комментировать другие отзывы, редактировать и удалять свои отзывыв и комментарии

Сайт приложения: [YaMDb](https://yacloud.telfia.com/)

### Описание API

Методы API имеют разграниченный доступ. Пользователи делятся на:
- пользователей
- модераторов
- администраторов

Пользователи могут создавать новые произведения. Писать ревью на произведенеия и комментировать их. Администраторы могут создавать пользователей и назначать им права.
Модераторы могут редактировать произведения, категории и жанры. 

💁 Подробное интерактивное описание всех доступных методов API расположено по адресу:
```http
  http://yacloud.telfia.com/swagger/
```
```http
  http://yacloud.telfia.com/redoc/
```
## 🛠️ Установка и запуск

Для запуска приложения должен быть установлен [git](https://git-scm.com/) и [docker](https://www.docker.com/).

```bash
git clone git@github.com:spaut33/infra_sp2.git
cd infra_sp2
```

Шаблон для создания .env файла (содержит необходимые для работы перменные окружения). Данный файл должен находится в папке `infra` проекта:
```env
EMAIL_HOST_USER=email@example.com
EMAIL_HOST_PASSWORD=password

DB_ENGINE=django.db.backends.postgresql
DB_NAME=postgres
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
DB_HOST=db
DB_PORT=5432

SECRET_KEY=django-secret-key
```

Собрать и запустить контейнеры
```bash
cd infra
sudo docker-compose build
sudo docker-compose up
```

После запуска контейнеров необходимо применить миграции, создать суперпользователя и собрать статику:
```bash
docker-compose exec web python3 manage.py migrate
docker-compose exec web python3 manage.py createsuperuser
docker-compose exec web python3 manage.py collectstatic --no-input
```

### Тесты

Для запуска тестов нужно перейти в директорию репозитория

```bash
cd infra_sp2
```

Cоздать и активировать виртуальное окружение:

```bash
python3 -m venv env
source env/bin/activate
```

Запустить тесты:

```bash
pytest
```

Для наполнения базы данных тестовыми данными можно использовать команду:

```bash
docker-compose exec web python3 manage.py flush --no-input
docker-compose exec web python3 manage.py loaddata fixtures.json
```

## ⚙️ Использованные технологии

- [Python 3.7](https://www.python.org/)
- [Django 2.2](https://www.djangoproject.com/)
- [Django Rest Framework 3.12](https://www.django-rest-framework.org/)
- [djangorestframework-simplejwt](https://github.com/jazzband/djangorestframework-simplejwt)
- [django-filter](https://github.com/carltongibson/django-filter/)
- [python-dotenv](https://github.com/theskumar/python-dotenv)
- [drf-yasg](https://github.com/axnsan12/drf-yasg)
- [pytest](https://docs.pytest.org/)
- [Docker](https://docker.com/)
- [PostgreSQL](https://www.postgresql.org/)
- [Nginx](https://www.nginx.com/)
    
## ⚠️ Лицензия

[MIT](https://choosealicense.com/licenses/mit/)


## 🧑‍💻 Авторы

- [Александр Ежов](https://www.github.com/Niea-under-7)
- [Егор Житников](https://www.github.com/egor-zhit)
- [Роман Петраков](https://www.github.com/spaut33) - Тимлид



- [Сергей Ивакин](https://github.com/sergej-i) - Наставник
- [Андрей Квичанский](https://www.github.com/kvichans) - Ревьюер
