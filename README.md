# Technical Exam for V-Unite

This is a todo list application built for V-Unite's technical exam.

It was created within roughly 30 hours using Vue and Laravel.

## Features
Main Features:
1. A list of todo items with CRUD.
2. A REST API for performing CRUD operations.
3. API based on Laravel.
4. Data can be saved on a database.

Added features:
1. Created a login mechanism and user authentication.
2. Todo list items are visible to their own makers.

## Setting Up
1. Clone this repository to your local machine.
2. Run `npm i` to install Vue dependencies.
3. Run `composer install` to install Laravel dependencies.
4. Set up an empty database.
5. Copy the contents of `.env-example` into a new file named `.env`. Make sure this new file is on the project root directory.
6. Change the database details on the `.env` file to match your database's environment settings.
7. Run `npm run dev` to run the Vue frontend development environment.
8. Run `php artisan serve` to run the Laravel server.
