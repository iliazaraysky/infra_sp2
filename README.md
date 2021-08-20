# Проект: запуск docker-compose
Это версия проекта [api_yamdb](https://github.com/iliazaraysky/api_yamdb) в котором добавлен Docker. После установки мы получаем полностью рабочее веб-приложение с базой данных PostgreSQL и веб-сервером Nginx


## Инструкция по установке
### Внимание! На компьютере должен быть установлен [Docker](https://www.docker.com/products/docker-desktop)

Клонируем репозиторий

<code>git clone https://github.com/iliazaraysky/infra_sp2</code>

Переходим в папку с проектом

<code>cd infra_sp2/</code>

Запускаем Docker

<code>docker-compose up</code>

После того, как Docker соберется и запустится, необходимо сделать миграций, чтобы инициализировать наши модели данных
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
