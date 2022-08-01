# Cinema-app 🎦🎞
###  Project description

A simple web application that simulates buying tickets at cinemas.


### Features:

- New user registration
- Authentication and authorization (role-based)
- Browse movies and available sessions
- Adding tickets to the cart, completing the purchase
- Also, a user with administrator rights can view, delete, change users, movies, sessions, etc.

### Used technology:
- Java 11
- Apache Maven
- Apache Tomcat
- Apache TomCat 9.0.50
- MySQL
- Spring Core, Spring MVC, Spring Security
- Hibernate

### Project architecture
- DAO - Data access layer
- Service - Application layer
- Controllers - Presentation layer

### Database structure

![http://joxi.ru/brR3J14TBoJQDm](http://joxi.ru/brR3J14TBoJQDm.jpg)

### How to run a project?
- Clone this project into your repo
- Install and configure Tomcat v9.0 to your project
- Install and configure MySQL
- Configure the settings for connection to your db in the resources/db.properties
- Run

### How to test the project
This project does not have a user interface. You can test it via Postman or through something similar. 
By default, you have user with role admin `login: admin@test.ua, password: admin123`
Here are available endpoints with description:
- `POST /register` It provides registration of user with USER role. 
Fields: email, password, repeatPassword. 
Example: `{"email":"user@test.com", "password":"12345678","repeatPassword":"12345678"}`

- `POST /cinema-halls` for user with admin role. Provides inserting of cinema hall to database. 
Fields: capacity, description. 
Example: `{"capacity":300, "description":"IMAX hall"}`

- `GET /cinema-halls` for any users. It shows list of available cinema halls.

- `POST /movies` for admin user. Provides inserting of movie to database. 
Fields: title, description. 
Example: `{"title":"Terminator", "description":"Iron Arnie is the best"}`

- `GET /movies` for any users. It shows list of available movies.

- `POST /movie-sessions` for admin user. 
Fields: movieId, cinemaHallId, showTime. Show time must match pattern dd.MM.yyyy. 
Example: `{"movieId":"1", "cinemaHallId":1, "showTime":"01.08.2022"}`

- `GET /movie-sessions/available?movieId={movieId}&date={date]` for any users. 
Shows available movie sessions for movie with id {movieId} and date {date}. 
Example: `http://localhost:8080/movie-sessions/available?movieId=1&date=01.08.2022`

- `PUT /movie-sessions/{id}` for admin user. Updates movie session with id {id}. 
Fields: movieId, cinemaHallId, showTime. Show time must match pattern dd.MM.yyyy. 
Example: `{"movieId":"1", "cinemaHallId":1, "showTime":"28.03.2022"}`

- `DELETE /movie-sessions/{id}` for admin user. Deletes movie session with id {id}.

- `PUT /shopping-carts/movie-sessions/{movieSessionId}` for any users. 
Puts the movie session with id {id} to shopping cart of current authenticated user.

- `GET /shopping-carts/by-user` for any users. Shows shopping cart of current authenticated user.

- `GET /users/by-email?email={email}` shows user with email {email}. 
Example: `http://localhost:8080/users/by-email?email=user@test.ua`

- `POST /orders/complete` for any users. Creates an order from movie sessions from shopping cart of current user

- `GET /orders` for any users. Shows order history for current authenticated user.
