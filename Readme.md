git clone https://github.com/AnotherOneGit/literate-couscous.git

docker-compose up --build

cp literate-couscous/.env.examlpe literate-couscous/.env

В файле literate-couscous/.env меняем строчки:</br>
DB_HOST=db</br>
DB_DATABASE=library</br>
DB_PASSWORD=example</br>

docker-compose exec web bash - входим в консоль проекта в докере, в нём:</br>
php artisan key:generate</br>
php artisan migrate</br>
vendor/bin/phpunit - для тестов

По адресу http://127.0.0.1:6080/ с логином root и паролем example
входим в админер и создаём бд library

Открываем http://127.0.0.1:8080/public

Запросы:</br>
POST http://127.0.0.1:8080/public/api/register - регистрация юзера. Необходимые поля:
name, email, password, password_confirmation</br>
POST http://127.0.0.1:8080/public/api/login - email, password 

GET http://127.0.0.1:8080/public/api/authors - список всех авторов с его книгами</br>
POST http://127.0.0.1:8080/public/api/authors - создание автора - name</br>
GET http://127.0.0.1:8080/public/api/authors/{author} - просмотр конкретного автора</br>
PUT http://127.0.0.1:8080/public/api/authors/{author} - редактирование автора</br>
DELETE http://127.0.0.1:8080/public/api/authors/{author} - удаление автора</br>

GET http://127.0.0.1:8080/public/api/books - просмотр всех книг. </br>
Если добавить в запрос ключ sort с пустым значением - будут отсортированы по средней оценке</br>
POST http://127.0.0.1:8080/public/api/books - создание книги. Поля:
author_id, title. Автор с данным id уже должен существовать</br>
GET http://127.0.0.1:8080/public/api/books/{book} - просмотр конкретной книги</br>
PUT http://127.0.0.1:8080/public/api/books/{book} - редактирование книги</br>
DELETE http://127.0.0.1:8080/public/api/books/{book} - удаление книги</br>

GET http://127.0.0.1:8080/public/api/search - поиск среди книг и авторов по значению ключа search </br>
POST http://127.0.0.1:8080/public/api/score - выставление оценки существуещей книге. Поля: book_id, score