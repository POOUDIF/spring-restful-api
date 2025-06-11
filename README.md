
# Spring RESTful API

![Spring Boot Version](https://img.shields.io/badge/Spring%20Boot-3.5.0-6DB33F?style=for-the-badge&logo=spring-boot&logoColor=white)
![Java Version](https://img.shields.io/badge/Java-17-007396?style=for-the-badge&logo=java&logoColor=white)
![Maven Build](https://img.shields.io/badge/Build-Maven-CB2134?style=for-the-badge&logo=apache-maven&logoColor=white)
![MySQL Database](https://img.shields.io/badge/Database-MySQL-005F0F?style=for-the-badge&logo=mysql&logoColor=white)
![License](https://img.shields.io/badge/License-Apache%202.0-blue?style=for-the-badge)

This project implements a robust RESTful API using Spring Boot, designed to manage user accounts, personal contacts, and their associated addresses. It provides a foundational backend service for a contact management system, focusing on secure user authentication and comprehensive data management.

## Features

* **User Management**:
    * **User Registration**: Allows new users to create an account.
    * **User Login**: Authenticates users and provides a session token for subsequent API calls.
    * **Get Current User**: Retrieves the details of the currently authenticated user.
    * **Update User Profile**: Enables users to modify their name and password.
    * **User Logout**: Invalidates the user's session token.
* **Contact Management**:
    * **Create Contact**: Adds new contact information (first name, last name, email, phone) for an authenticated user.
    * **Update Contact**: Modifies existing contact details.
    * **Get Contact**: Retrieves a specific contact by its ID.
    * **Search Contacts**: Filters contacts by name, phone, or email, with pagination support.
    * **Remove Contact**: Deletes a contact from the user's list.
* **Address Management**:
    * **Create Address**: Adds a new address for a specific contact.
    * **Update Address**: Modifies details of an existing address.
    * **Get Address**: Retrieves a specific address by its ID.
    * **Remove Address**: Deletes an address associated with a contact.
    * **List Addresses**: Fetches all addresses for a given contact.

## Technologies Used

* **Backend:**
    * [Spring Boot](https://spring.io/projects/spring-boot) (v3.5.0)
    * [Java Development Kit (JDK)](https://www.oracle.com/java/technologies/downloads/) (v17)
    * [Spring Data JPA](https://spring.io/projects/spring-data-jpa)
    * [Lombok](https://projectlombok.org/) (to reduce boilerplate code)
    * [Spring Boot Starter Validation](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features.html#boot-features-validation)
    * [Spring Boot Starter Web](https://docs.spring.io/spring-boot/docs/current/reference/html/web.html)
* **Database:**
    * [MySQL](https://www.mysql.com/)
    * `mysql-connector-j`
* **Build Tool:**
    * [Apache Maven](https://maven.apache.org/)

## How to Run the Application

Follow these steps to set up and run the project in your local environment.

### Prerequisites

Ensure you have the following installed on your machine:

* **Java Development Kit (JDK) 17 or later**:
    * You can download it from [Oracle JDK](https://www.oracle.com/java/technologies/downloads/) or [Adoptium OpenJDK](https://adoptium.net/).
* **Apache Maven**:
    * If you don't have Maven installed globally, you can use the included Maven Wrapper (`./mvnw`).
* **MySQL Server**:
    * Ensure your MySQL server is running and accessible.

### Database Setup

1.  **Create Database**: Create a new database named `spring_restful_api` in your MySQL server.
    ```sql
    CREATE DATABASE spring_restful_api;
    ```
2.  **Use Database**: Switch to the newly created database.
    ```sql
    USE spring_restful_api;
    ```
3.  **Run SQL Script**: Execute the `database.sql` script located in the root of your project directory to create the necessary tables:
    ```bash
    -- From the project root directory
    SOURCE database.sql;
    ```
    This script will create the `users` and `contacts` tables.

### Application Configuration

Update the database connection properties in the `src/main/resources/application.properties` file:

```properties
spring.application.name=Spring RESTful API
spring.datasource.url=jdbc:mysql://localhost:3306/spring_restful_api
spring.datasource.username=root
spring.datasource.password=
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.datasource.type=com.zaxxer.hikari.HikariDataSource
spring.datasource.hikari.minimum-idle=10
spring.datasource.hikari.maximum-pool-size=50

# This is important for Hibernate to know the correct MySQL dialect
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL8Dialect
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
