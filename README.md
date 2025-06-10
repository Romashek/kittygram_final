#  Как работать с репозиторием финального задания
[![CI/CD Status](https://github.com/Romashek/kittygram/actions/workflows/main.yml/badge.svg)](https://github.com/Romashek/kittygram/actions)
## Что нужно сделать

Настроить запуск проекта Kittygram в контейнерах и CI/CD с помощью GitHub Actions

## Как проверить работу с помощью автотестов

В корне репозитория создайте файл tests.yml со следующим содержимым:
```yaml
repo_owner: ваш_логин_на_гитхабе
kittygram_domain: полная ссылка (https://доменное_имя) на ваш проект Kittygram
taski_domain: полная ссылка (https://доменное_имя) на ваш проект Taski
dockerhub_username: ваш_логин_на_докерхабе
```

Скопируйте содержимое файла `.github/workflows/main.yml` в файл `kittygram_workflow.yml` в корневой директории проекта.

Для локального запуска тестов создайте виртуальное окружение, установите в него зависимости из backend/requirements.txt и запустите в корневой директории проекта `pytest`.

## Чек-лист для проверки перед отправкой задания

- Проект Taski доступен по доменному имени, указанному в `tests.yml`.
- Проект Kittygram доступен по доменному имени, указанному в `tests.yml`.
- Пуш в ветку main запускает тестирование и деплой Kittygram, а после успешного деплоя вам приходит сообщение в телеграм.
- В корне проекта есть файл `kittygram_workflow.yml`.

# Проект контейнеры и CI/CD для Kittygram

Проект подготовлен в рамках финального задания спринта в целях получения навыков настройки и запуска проектов в контейнерах, настройки автоматического тестирования и деплоя проектов на удалённый сервер.

# Стек технологий
- Python 3.9
- Django 
- gunicorn
- djoser 
- djangorestframework 

# Инструкция по запуску
1. форкнуть репозиторий проекта: Romashek/kittygram_final
2. клонировать форкнутый репозиторий
3. в репозитории проекта во вкладке settings/Secrets and variables/actions определить ваши secrets:
Логин и пароль вашего профиля на Docker.com:
- DOCKER_PASSWORD
- DOCKER_USERNAME
Данные вашего удалённого сервера:
- HOST (IP-адрес вашего сервера)
- SSH_KEY (закрытый SSH-ключ)
- USER (имя пользователя)
- SSH_PASSPHRASE (passphrase от закрытого SSH-ключа)
Данные для отправки сообщения о деплое проекта:
- TELEGRAM_TO (id получателя сообщения)
- TELEGRAM_TOKEN (token робота)
4. на сервере:

- создайте директорию kittygram и создайте в ней файл .env. В файле .env определите значения переменных SECRET_KEY и ALLOWED_HOSTS;

- определите настройки location в секции server в файле /etc/nginx/sites-enabled/default:
server {
    server_name <IP-адрес вашего сервера> <доменное имя вашего сайта>;
    location / {
        proxy_set_header Host $http_host;
        proxy_pass http://127.0.0.1:9000;
    }
}
5. в директории проекта в файле docker-compose.production.yml замените строчки
    image: roman200015/kittygram_gateway на image: <логин вашего профиля на Docker.com>/kittygram_gateway 
6. сделайте пуш:
    git add .
    git commit -m "<ваше сообщение коммита>"
    git push


# Авторы
- команда Яндекс Практикума [yandex-praktikum] (https://github.com/yandex-praktikum)
- Роман Кондрашов (https://github.com/Romashek)