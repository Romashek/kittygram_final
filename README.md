
[![Main Kittygram workflow](https://github.com/Romashek/kittygram_final/actions/workflows/main.yml/badge.svg)](https://github.com/Romashek/kittygram_final/actions/workflows/main.yml)

# Проект контейнеры и CI/CD для Kittygram

Проект подготовлен в рамках финального задания спринта в целях получения навыков настройки и запуска проектов в контейнерах, настройки автоматического тестирования и деплоя проектов на удалённый сервер.

# Стек технологий
- Django==3.2.3
- djangorestframework==3.12.4
- djoser==2.1.0
- webcolors==1.11.1
- psycopg2-binary==2.9.3
- Pillow==9.0.0
- pytest==6.2.4
- pytest-django==4.4.0
- pytest-pythonpath==0.7.3
- PyYAML==6.0
- python-dotenv==1.0.0 

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

- создайте директорию kittygram и создайте в ней файл .env. В файле .env определите значения переменных SECRET_KEY, ALLOWED_HOSTS, а также переменные для настройки бд: DB_NAME, DB_PORT, DB_HOST, POSTGRES_PASSWORD, POSTGRES_USER, POSTGRES_DB и переменную DEBUG;

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