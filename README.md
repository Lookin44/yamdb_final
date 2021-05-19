# Описание сервиса
Проект YaMDb собирает отзывы пользователей на произведения. Произведения делятся на категории: «Книги», «Фильмы»,
«Музыка».

[![yamdb_final workflow](https://github.com/lookin44/yamdb_final/)]
(https://github.com/lookin44/yamdb_final/)

# Установка сервиса
1. Скопируйте проект к себе на компютер ```git clone https://github.com/Lookin44/infra_sp2.git```
2. Создайте файл .env со значениями: 
```DB_ENGINE=django.db.backends.postgresql```
```DB_NAME=postgres```
```POSTGRES_USER=postgres```
```POSTGRES_PASSWORD=postgres```
```DB_HOST=db```
```DB_PORT=5432```
```EMAIL_HOST_PASSWORD=<Ваш пароль от почты>```
3. Запустите Docker: ```sudo docker-compose up```
4. Выполните миграции внутри докера ```sudo docker-compose exec web python manage.py migrate --noinput```
5. Создайте суперюзера внутри докера ```sudo docker-compose exec web python manage.py createsuperuser```
6. Соберите всю статику внутри докера ```sudo docker-compose exec web python manage.py collectstatic --no-input```
7. Загрузите тестовые данные ```sudo docker-compose exec web python manage.py loaddata fixtures.json```

# Алгоритм регистрации пользователей
1. Пользователь отправляет запрос с параметром email и username на ```/auth/email/```.
2. **YaMDB** отправляет письмо с кодом подтверждения (confirmation_code) на адрес email .
3. Пользователь отправляет запрос с параметрами email, username и confirmation_code на ```/auth/token/```, в ответе на запрос ему приходит token (JWT-токен).
4. При желании пользователь отправляет PATCH-запрос на ```/users/me/``` и заполняет поля в своём профайле (описание полей — в документации).

# Пользовательские роли
* Аноним — может просматривать описания произведений, читать отзывы и комментарии.
* Аутентифицированный пользователь — может, как и Аноним, читать всё, дополнительно он может публиковать отзывы и ставить рейтинг произведениям (фильмам/книгам/песенкам), может комментировать чужие отзывы и ставить им оценки; может редактировать и удалять свои отзывы и комментарии.
* Модератор — те же права, что и у Аутентифицированного пользователя плюс право удалять любые отзывы и комментарии.
* Администратор — полные права на управление проектом и всем его содержимым. Может создавать и удалять категории и произведения. Может назначать роли пользователям.
* Администратор Django — те же права, что и у роли Администратор.

# Информация по запросам
1. Запустите сервер
2. Перейдите на http://localhost:8000/redoc/

#### Проект разработан командой:
* [Лукин Егор](https://github.com/Lookin44)
  - Роль: TL, Developer; develop: приложение User
* [Екатерина Павлова](https://github.com/pavlovsdog110691)
  - Роль: Developer; develop: приложение Api: модели, вьюхи, пермишены, сериалайзеры, эндпоинты для Category, Genre, Title
* [Петр Балдаев](https://github.com/spqr-86)
  - Роль: Developer; develop: приложение Api: модели, вьюхи, пермишены, сериалайзеры, эндпоинты для Review, Comment
