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

DB_ENGINE=django.db.backends.postgresql
DB_NAME=postgres
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
DB_HOST=db
DB_PORT=5432

```

4. Запускаем Docker (из терминала или Git Bash)

<code>docker-compose up</code>

# 
5. После того, как Docker соберется и запустится (мы поймем, что все работает, когда в терминале ничего не будет происходить а последней строкой будет надпись **Attaching to db_1, nginx_1, web_1**)

6. Теперь необходимо сделать миграций, чтобы инициализировать модели данных. Открываем новое окно терминала, переходим в папку проекта (если терминал открылся в домашней директории), вводим по очереди команды:

```
docker-compose exec web python manage.py makemigrations users

docker-compose exec web python manage.py makemigrations titles

docker-compose exec web python manage.py makemigrations reviews

docker-compose exec web python manage.py migrate

docker-compose exec web python manage.py createsuperuser
# Если происходит ошибка "Superuser creation skipped due to not running in a TTY...", значит вы набираете из Git Bash.
# Чтобы все заработало, необходимо запускать команду используя winpty

winpty docker-compose exec web python manage.py createsuperuser # Применять только если выдает ошибку, иначе пропускаем

docker-compose exec web python manage.py collectstatic
```


Приложение работает по адресу [http://127.0.0.1/](http://127.0.0.1/)
# Требования
Python 3.6 +
Docker Desktop 3.5 +

Работает под ОС Linux, Windows, macOS, BSD
