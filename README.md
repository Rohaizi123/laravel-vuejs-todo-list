## About This repo :

This repo is a sample of making Simple To do list web app using Laravel 8 as a backend and Vue Js as a front end. This simple web 
app used concept of rest api to store data.

## Project setup

clone the repo 
```
https://github.com/Rohaizi123/laravel-vuejs-todo-list.git
```


Then cd into the folder with this command-

```
cd laravel-vuejs-todo-list
```

Then do a composer install

```
composer install
```

copy .env.example file and rename it to .env
and make a new database in mySql database, and name it what it ever you want , make sure that this name match in your .env file .

make migration for the tables 

```
php artisan migrate
```

generate key 

```
php artisan key:generate
```


Then do a npm install

```
npm install
```
## Run server

Run server using this command-

```
php artisan serve
```
### for the front end part you need to open another terminal for the same project and make :
```
npm run dev
```

Then go to `http://localhost:8000` from your browser and see the web app.