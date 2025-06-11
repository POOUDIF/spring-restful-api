# Spring RESTful API Project README

This document provides a README for the Spring RESTful API project, detailing its features, API specifications, and setup instructions.

### Project Overview

This project implements a RESTful API using Spring Boot, designed to manage users, contacts, and addresses. It includes functionalities for user registration, authentication (login/logout), and CRUD operations for contacts and their associated addresses.

### Features

* **User Management**: Register, log in, get current user details, update user information, and log out.
* **Contact Management**: Create, update, retrieve, search, and delete contact information.
* **Address Management**: Create, update, retrieve, delete, and list addresses associated with a contact.
* **Token-based Authentication**: Secure API endpoints using `X-API-TOKEN`.
* **Database Integration**: Utilizes MySQL as the database.
* **Validation**: Includes request body validation for API endpoints.

### Technologies Used

* Java 17
* Spring Boot 3.5.0
* Spring Data JPA
* Spring Web
* Maven
* MySQL Connector/J
* Lombok

### Database Schema

The database `spring_restful_api` contains the following tables:

* **`users`**:
    * `username` (VARCHAR(100), PRIMARY KEY)
    * `password` (VARCHAR(100), NOT NULL)
    * `name` (VARCHAR(100), NOT NULL)
    * `token` (VARCHAR(100), UNIQUE)
    * `token_expired_at` (BIGINT)

* **`contacts`**:
    * `id` (VARCHAR(100), PRIMARY KEY)
    * `username` (VARCHAR(100), NOT NULL)
    * `first_name` (VARCHAR(100), NOT NULL)
    * `last_name` (VARCHAR(100))
    * `phone` (VARCHAR(100))
    * `email` (VARCHAR(100))
    * `FOREIGN KEY fk_users_contacts (username) REFERENCES users (username)`

* **`addresses`**:
    * `id` (String)
    * `street` (String)
    * `city` (String)
    * `province` (String)
    * `country` (String)
    * `postal_code` (String)
    * `contact_id` (Foreign Key referencing `contacts` table's `id`)

### Getting Started

#### Prerequisites

* Java Development Kit (JDK) 17
* Maven
* MySQL Database

#### Setup Instructions

1.  **Clone the repository**:
    ```bash
    git clone <repository_url>
    cd spring-restful-api
    ```

2.  **Database Configuration**:
    * Create a MySQL database named `spring_restful_api`.
    * Run the provided SQL script to create the necessary tables:
        ```bash
        mysql -u your_username -p spring_restful_api < database.sql
        ```
    * Update the database connection properties in `src/main/resources/application.properties` if needed:
        ```properties
        spring.datasource.url=jdbc:mysql://localhost:3306/restful_api_db
        spring.datasource.username=root
        spring.datasource.password=
        ```

3.  **Build the project**:
    ```bash
    mvn clean install
    ```

4.  **Run the application**:
    ```bash
    mvn spring-boot:run
    ```
    The application will start on port 8080 by default.

### API Documentation

The API endpoints are categorized by resource: User, Contact, and Address. All endpoints requiring authentication will need an `X-API-TOKEN` in the request header.

#### User API

* **Register User**:
    * `POST /api/users`
    * Request Body: `{"username": "daffa", "pssword": "secret", "name": "Daffa Saputra"}`
    * Response (Success): `{"data": "OK"}`
    * Response (Failed): `{"errors": "Username must not blank !!!"}`

* **Login User**:
    * `POST /api/auth/login`
    * Request Body: `{"username": "daffa", "pssword": "secret"}`
    * Response (Success): `{"data": {"token": "TOKEN", "expiresAt": 234234234234}}`
    * Response (Failed): `{"errors": "username or password wrong"}`

* **Get Current User**:
    * `GET /api/users/current`
    * Request Header: `X-API-TOKEN : Token` (Mandatory)
    * Response (Success): `{"data": {"username": "daffa", "nama": "Daffa Saputra"}}`
    * Response (Failed): `{"errors": "Unauthorized"}`

* **Update User**:
    * `PATCH /api/users/current`
    * Request Header: `X-API-TOKEN : Token` (Mandatory)
    * Request Body: `{"name": "Daffa Saputra", "password": "new password"}`
    * Response (Success): `{"data": {"username": "daffa", "nama": "Daffa Saputra"}}`
    * Response (Failed): `{"errors": "Unauthorized"}`

* **Logout User**:
    * `DELETE /api/auth/logout`
    * Request Header: `X-API-TOKEN : Token` (Mandatory)
    * Response (Success): `{"data": "Ok"}`

#### Contact API

* **Create Contact**:
    * `POST /api/contacts`
    * Request Header: `X-API-TOKEN : Token` (Mandatory)
    * Request Body: `{"firstName": "Daffa", "lastName": "Saputra", "email": "daffa@example.com", "phone": "08987654321"}`
    * Response (Success): `{"data": {"id": "random-string", "firstName": "Daffa", "lastName": "Saputra", "email": "daffa@example.com", "phone": "08987654321"}}`
    * Response (Failed): `{"errors": "Email format invalid, phone format invalid, ..."}`

* **Update Contact**:
    * `PUT /api/contacts/{idContacts}`
    * Request Header: `X-API-TOKEN : Token` (Mandatory)
    * Request Body: `{"firstName": "Daffa", "lastName": "Saputra", "email": "daffa@example.com", "phone": "08987654321"}`
    * Response (Success): `{"data": {"id": "random-string", "firstName": "Daffa", "lastName": "Saputra", "email": "daffa@example.com", "phone": "08987654321"}}`
    * Response (Failed): `{"errors": "Email format invalid, phone format invalid, ..."}`

* **Get Contact**:
    * `GET /api/contacts/{idContacts}`
    * Request Header: `X-API-TOKEN : Token` (Mandatory)
    * Response (Success): `{"data": {"id": "random-string", "firstName": "Daffa", "lastName": "Saputra", "email": "daffa@example.com", "phone": "08987654321"}}`
    * Response (Failed, 404): `{"errors": "Contact is not found"}`

* **Search Contact**:
    * `GET /api.contacts/`
    * Query Params:
        * `name`: String, contact first name or last name (optional)
        * `phone`: String, contact phone (optional)
        * `email`: String, contact email (optional)
        * `page`: Integer, starts from 0
        * `size`: Integer, default 10
    * Request Header: `X-API-TOKEN : Token` (Mandatory)
    * Response (Success): Paged list of contacts
    * Response (Failed): `{"errors": "Unauthorized"}`

* **Remove Contact**:
    * `DELETE /api/contacts/{idContacts}`
    * Request Header: `X-API-TOKEN : Token` (Mandatory)
    * Response (Success): `{"data": "Ok"}`
    * Response (Failed): `{"errors": "Contact is not found"}`

#### Address API

* **Create Address**:
    * `POST /api/contacts/{idContact}/addresses`
    * Request Header: `X-API-TOKEN : Token` (Mandatory)
    * Request Body: `{"street": "Jalan", "city": "Kota", "province": "Provinsi", "country": "Negara", "postalCode": "12345"}`
    * Response (Success): `{"data": {"id": "random-string", "street": "Jalan", "city": "Kota", "province": "Provinsi", "country": "Negara", "postalCode": "12345"}}`
    * Response (Failed): `{"errors": "Address is not found"}`

* **Update Address**:
    * `PUT /api/contacts/{idContact}/addresses/{idAddress}`
    * Request Header: `X-API-TOKEN : Token` (Mandatory)
    * Request Body: `{"street": "Jalan apa", "city": "Kota", "province": "Provinsi", "country": "Negara", "postalCode": "12345"}`
    * Response (Success): `{"data": {"id": "random-string", "street": "Jalan apa", "city": "Kota", "province": "Provinsi", "country": "Negara", "postalCode": "12345"}}`
    * Response (Failed): `{"errors": "Address is not found"}`

* **Get Address**:
    * `GET /api/contacts/{idContact}/addresses/{idAddress}`
    * Request Header: `X-API-TOKEN : Token` (Mandatory)
    * Response (Success): `{"data": {"id": "random-string", "street": "Jalan apa", "city": "Kota", "province": "Provinsi", "country": "Negara", "postalCode": "12345"}}`
    * Response (Failed): `{"errors": "Addresses is not found"}`

* **Remove Address**:
    * `DELETE /api/contacts/{idContact}/addresses/{idAddress}`
    * Request Header: `X-API-TOKEN : Token` (Mandatory)
    * Response (Success): `{"data": "Ok"}`
    * Response (Failed): `{"errors": "Address is not found"}`

* **List Address**:
    * `GET /api/contacts/{idContact}/addresses`
    * Request Header: `X-API-TOKEN : Token` (Mandatory)
    * Response (Success): `{"data": {"id": "random-string", "street": "Jalan apa", "city": "Kota", "province": "Provinsi", "country": "Negara", "postalCode": "12345"}}`
    * Response (Failed): `{"errors": "Addresses is not found"}`

### Contributing

Fork the repository, create a new branch, commit your changes, and open a pull request.

### License

This project is licensed under the Apache License, Version 2.0.
