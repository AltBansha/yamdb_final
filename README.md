# YaMDb API

![Status badge](https://github.com/AltBansha/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)

### Сайт: http://84.252.138.10/api/v1/

### Описание
Проект **YaMDb** позволяет собирать отзывы пользователей на произведения. Произведения делятся на категории: «Книги», «Фильмы», «Музыка».

### Алгоритм регистрации пользователей:
1. Пользователь отправляет запрос с параметром *email* на */auth/email/*.
2. **YaMDB** отправляет письмо с кодом подтверждения (*confirmation_code*) на адрес *email*.
3. Пользователь отправляет запрос с параметрами *email* и *confirmation_code* на */auth/token/*, в ответе на запрос ему приходит *token* (JWT-токен).
4. При желании пользователь отправляет PATCH-запрос на */users/me/* и заполняет поля в своём профайле (описание полей — в документации).

Подробная API документация находится по адресу /redoc

### Установка
Проект собран в Docker 20.10.06 и содержит три образа:
- web - образ проекта
- postgres - образ базы данных PostgreSQL v 12.04
- nginx - образ web сервера nginx 

#### Запуск проекта:
- Установите Docker
- Выполнить команду docker pull dockerfirst1/yamdb:v2.2021

#### Первоначальная настройка Django:
- docker-compose exec web python manage.py migrate --noinput
- docker-compose exec web python manage.py collectstatic --no-input 

#### Загрузка тестовой фикстуры в базу:
docker-compose exec web python manage.py loaddata fixtures.json

#### Создание суперпользователя:
- docker-compose exec web python manage.py createsuperuser
