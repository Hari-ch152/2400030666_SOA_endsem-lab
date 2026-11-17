# Library Management System – SOA CRUD Service

A simple Service-Oriented Architecture (SOA) lab project built with Java 17, Spring Boot REST APIs, Spring Data JPA and MySQL. The Book Service exposes CRUD operations over HTTP.

## Requirements
- JDK 17+
- Maven 3.6+
- MySQL 8+

## 1. Create the database
Open MySQL Workbench or the MySQL command line and run:
```sql
CREATE DATABASE library_db;
```

## 2. Configure database credentials
Open `src/main/resources/application.properties` and replace `YOUR_MYSQL_PASSWORD` with your MySQL root password. Change the username too if needed.

## 3. Run the project
From the project root:
```bash
mvn spring-boot:run
```
Or import the folder into Spring Tool Suite / IntelliJ IDEA as an existing Maven project and run `LibraryManagementApplication.java`.

The service starts at `http://localhost:8080`.

## REST API endpoints

| Operation | Method | URL |
|---|---|---|
| Create book | POST | `/api/books` |
| Get all books | GET | `/api/books` |
| Get one book | GET | `/api/books/{id}` |
| Update book | PUT | `/api/books/{id}` |
| Delete book | DELETE | `/api/books/{id}` |

### Example JSON
```json
{
  "title": "The Alchemist",
  "author": "Paulo Coelho",
  "category": "Fiction",
  "quantity": 5
}
```

### Test with Postman
1. Create: `POST http://localhost:8080/api/books`, choose Body → raw → JSON, and send the example JSON.
2. Read all: `GET http://localhost:8080/api/books`.
3. Read one: `GET http://localhost:8080/api/books/1`.
4. Update: `PUT http://localhost:8080/api/books/1` with updated JSON.
5. Delete: `DELETE http://localhost:8080/api/books/1`.

## Project structure
```text
LibraryManagementSOA/
├── pom.xml
├── README.md
└── src/
    └── main/
        ├── java/com/example/library/
        │   ├── LibraryManagementApplication.java
        │   ├── controller/
        │   │   ├── BookController.java
        │   │   └── GlobalExceptionHandler.java
        │   ├── model/Book.java
        │   ├── repository/BookRepository.java
        │   └── service/
        │       ├── BookService.java
        │       └── BookNotFoundException.java
        └── resources/application.properties
```

## SOA explanation
- **Service provider:** Book REST service.
- **Service interface/contract:** HTTP endpoints under `/api/books`.
- **Business logic:** `BookService`.
- **Data access:** `BookRepository`.
- **Data store:** MySQL `library_db`.
- **Consumers:** Postman, a web frontend, or another application can call the REST endpoints.

This is a small SOA-style service for a lab demonstration. A larger deployment can split books, members, and borrowing into separately deployed services.
