[![Python](https://img.shields.io/badge/-Python_3.9.10-464646??style=flat-square&logo=Python)](https://www.python.org/downloads/)
[![Django](https://img.shields.io/badge/-Django-464646??style=flat-square&logo=Django)](https://www.djangoproject.com/)
[![Django](https://img.shields.io/badge/-Django_rest_framework_3.12.4-464646??style=flat-square&logo=Django)](https://www.django-rest-framework.org)
[![Nginx](https://img.shields.io/badge/-Nginx-464646??style=flat-square&logo=Nginx)](https://nginx.org/ru/)
[![Gunicorn](https://img.shields.io/badge/-gunicorn-464646??style=flat-square&logo=gunicorn)](https://gunicorn.org/)
[![CI/CD](https://img.shields.io/badge/-CI/CD-464646??style=flat-square&logo=CI/CD)](https://resources.github.com/ci-cd/)
<br>
![badge](https://github.com/Evg-Che/kittygram_final/actions/workflows/main.yml/badge.svg)


# Kittygram

## Kittygram — социальная сеть для обмена фотографиями котиков. 

**Контейнеры и CI/CD для Kittygram.**

## Технологии

- Python 3.9
- Django 3.2.3
- Django REST framework 3.12.4
- JavaScript


# Установка 

Клонировать репозиторий на свой компьютер:

    ```bash
    git clone https://github.com/Evg-Che/kittygram_final.git
    ```
    ```bash
    cd kittygram
    ```
Выполнить запуск:

```bash
sudo docker compose -f docker-compose.yml up
```

## Миграции и сбор статических файлов бэкенда

После запуска необходимо выполнить сбор статических файлов и миграции бэкенда. 

```bash
sudo docker compose -f [имя-файла-docker-compose.yml] exec backend python manage.py migrate

sudo docker compose -f [имя-файла-docker-compose.yml] exec backend python manage.py collectstatic --no-input

sudo docker compose -f [имя-файла-docker-compose.yml] exec backend cp -r /app/collected_static/. /static/static/
```

## В директорию kittygram/ скопировать файлы docker-compose.production.yml и .env:

    ```bash
    scp -i path_to_SSH/SSH_name docker-compose.production.yml username@server_ip:/home/username/kittygram/docker-compose.production.yml
    * ath_to_SSH — путь к файлу с SSH-ключом;
    * SSH_name — имя файла с SSH-ключом (без расширения);
    * username — ваше имя пользователя на сервере;
    * server_ip — IP вашего сервера.
    ```

## Запустить docker compose в режиме демона:

    ```bash
    sudo docker compose -f docker-compose.production.yml up -d
    ```

## Настройка CI/CD

1. Файл workflow уже написан. Он находится в директории

    ```bash
    kittygram/.github/workflows/main.yml
    ```

2. На своем сервере добавить секреты в GitHub Actions:

    ```bash
    DOCKER_USERNAME                # имя пользователя в DockerHub
    DOCKER_PASSWORD                # пароль пользователя в DockerHub
    HOST                           # ip_address сервера
    USER                           # имя пользователя
    SSH_KEY                        # приватный ssh-ключ (cat ~/.ssh/id_rsa)
    SSH_PASSPHRASE                 # кодовая фраза (пароль) для ssh-ключа

    TELEGRAM_TO                    # id телеграм-аккаунта (можно узнать у @userinfobot, команда /start)
    TELEGRAM_TOKEN                 # токен бота (получить токен можно у @BotFather, /token, имя бота)
    ```


### Автор
Eva Che