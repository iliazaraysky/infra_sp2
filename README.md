# Проект: запуск docker-compose
Это версия проекта [api_yamdb](https://github.com/iliazaraysky/api_yamdb) в котором добавлен Docker. После установки мы получаем полностью рабочее веб-приложение с базой данных PostgreSQL и веб-сервером Nginx


# Инструкция по установке
### Внимание! На компьютере должен быть установлен [Docker](https://www.docker.com/products/docker-desktop)

1. Клонируем репозиторий

```
git clone https://github.com/iliazaraysky/infra_sp2
```

2. Переходим в папку с проектом

```
cd infra_sp2/
```

3. **Важно!** Это учебный проект и в нем есть файл .env. В реальной практике, такого не происходит. Файл необходимо создать вручную на этом этапе.
После перехода в папку infra_sp2, создаем файл .env (файл не имеет расширения, но его имя обязательно должно начинаться с точки). Открываем файл любым редактором кода или блокнотом. Вписываем следующие данные:

```
DB_ENGINE=django.db.backends.postgresql
DB_NAME=postgres
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
DB_HOST=db
DB_PORT=5432
PROJECT_SECRET_KEY=p&l%385148kslhtyn^##a1)ilz@4zqj=rq&agdol^##zgl9(vs
DEBUG_STATUS=False

```

4. Запускаем Docker (из терминала или Git Bash)

```
docker-compose up
```

# 
5. После того, как Docker соберется и запустится необходимо сделать миграций, чтобы инициализировать модели данных. Открываем новое окно терминала, переходим в папку проекта (если терминал открылся в домашней директории), вводим по очереди команды:

```
docker-compose exec web python manage.py makemigrations users

docker-compose exec web python manage.py makemigrations titles

docker-compose exec web python manage.py makemigrations reviews

docker-compose exec web python manage.py migrate

docker-compose exec web python manage.py createsuperuser
```

*Если происходит ошибка "Superuser creation skipped due to not running in a TTY...", значит вы набираете из Git Bash. Чтобы все заработало, необходимо запускать команду используя winpty*

```
winpty docker-compose exec web python manage.py createsuperuser

docker-compose exec web python manage.py loaddata fixtures.json

docker-compose exec web python manage.py collectstatic
```


Приложение работает по адресу [http://127.0.0.1/](http://127.0.0.1/)
# Требования
Python 3.6 +
Docker Desktop 3.5 +

Работает под ОС Linux, Windows, macOS, BSD
