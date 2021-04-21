git clone https://github.com/AnotherOneGit/literate-couscous.git

docker-compose up --build

cp literate-couscous/.env.examlpe literate-couscous/.env

В файле literate-couscous/.env меняем строчки:
DB_HOST=db
DB_DATABASE=library
DB_PASSWORD=example

docker-compose exec web bash - входим в консоль проекта в докере, в нём:
php artisan key:generate
php artisan migrate
vendor/bin/phpunit - для тестов

По адресу http://127.0.0.1:6080/ с логином root и паролем example
входим в админер и создаём бд library

Открываем http://127.0.0.1:8080/public

Запросы:
POST http://127.0.0.1:8080/public/api/register - регистрация юзера. Необходимые поля:
name, email, password, password_confirmation
POST http://127.0.0.1:8080/public/api/login - email, password 

GET http://127.0.0.1:8080/public/api/authors - список всех авторов с его книгами
POST http://127.0.0.1:8080/public/api/authors - создание автора - name
GET http://127.0.0.1:8080/public/api/authors/{author} - просмотр конкретного автора
PUT http://127.0.0.1:8080/public/api/authors/{author} - редактирование автора
DELETE http://127.0.0.1:8080/public/api/authors/{author} - удаление автора

GET http://127.0.0.1:8080/public/api/books - просмотр всех книг. 
Если добавить в запрос ключ sort с пустым значением - будут отсортированы по средней оценке
POST http://127.0.0.1:8080/public/api/books - создание книги. Поля:
author_id, title. Автор с данным id уже должен существовать
GET http://127.0.0.1:8080/public/api/books/{book} - просмотр конкретной книги
PUT http://127.0.0.1:8080/public/api/books/{book} - редактирование книги
DELETE http://127.0.0.1:8080/public/api/books/{book} - удаление книги

GET http://127.0.0.1:8080/public/api/search - поиск среди книг и авторов по значению ключа search 
POST http://127.0.0.1:8080/public/api/score - выставление оценки существуещей книге. Поля: book_id, score