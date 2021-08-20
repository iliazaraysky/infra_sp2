# Проект: запуск docker-compose
Это версия проекта [api_yamdb](https://github.com/iliazaraysky/api_yamdb) в котором добавлен Docker. После установки мы получаем полностью рабочее веб-приложение с базой данных PostgreSQL и веб-сервером Nginx


# Инструкция по установке
### Внимание! На компьютере должен быть установлен [Docker](https://www.docker.com/products/docker-desktop)

1. Клонируем репозиторий

<code>git clone https://github.com/iliazaraysky/infra_sp2</code>

2. Переходим в папку с проектом

<code>cd infra_sp2/</code>

3. После перехода в папку infra_sp2, создаем файл .env (файл не имеет расширения, но его имя обязательно должно начинаться с точки). Открываем файл любым редактором кода или блокнотом. Вписываем следующие данные:

```
DB_ENGINE=django.db.backends.postgresql # указываем, что работаем с postgresql
DB_NAME=postgres # имя базы данных
POSTGRES_USER=postgres # логин для подключения к базе данных
POSTGRES_PASSWORD=postgres # пароль для подключения к БД (установите свой)
DB_HOST=db # название сервиса (контейнера)
DB_PORT=5432 # порт для подключения к БД 
```

4. Запускаем Docker

<code>docker-compose up</code>
# 
5. После того, как Docker соберется и запустится, необходимо сделать миграций, чтобы инициализировать наши модели данных
вводим по очереди команды:

```docker-compose exec web python manage.py makemigrations users

docker-compose exec web python manage.py makemigrations titles

docker-compose exec web python manage.py makemigrations reviews

docker-compose exec web python manage.py migrate

docker-compose exec web python manage.py createsuperuser

docker-compose exec web python manage.py collectstatic
```


Приложение работает по адресу [http://127.0.0.1/](http://127.0.0.1/)
# Требования
Python 3.6 +
Docker Desktop 3.5 +

Работает под ОС Linux, Windows, macOS, BSD
