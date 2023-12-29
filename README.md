# Project: spring-boot-jwt-authentication

## Dependency

```xml
<dependency>
  <groupId>com.mysql</groupId>
  <artifactId>mysql-connector-j</artifactId>
  <scope>runtime</scope>
</dependency>
```

## Configure Spring Datasource, JPA, App properties

```properties
spring.datasource.url= jdbc:postgresql://localhost:5432/testdb
spring.datasource.username= postgres
spring.datasource.password= 123

spring.jpa.properties.hibernate.jdbc.lob.non_contextual_creation= true
spring.jpa.properties.hibernate.dialect= org.hibernate.dialect.PostgreSQLDialect

# Hibernate ddl auto (create, create-drop, validate, update)
spring.jpa.hibernate.ddl-auto= update

# App Properties
bezkoder.app.jwtSecret= bezKoderSecretKey
bezkoder.app.jwtExpirationMs= 86400000
```

## Run Spring Boot application

```
mvn spring-boot:run
```

## Run following SQL insert statements

```
INSERT INTO roles(name) VALUES('ROLE_USER');
INSERT INTO roles(name) VALUES('ROLE_MODERATOR');
INSERT INTO roles(name) VALUES('ROLE_ADMIN');
```

For more detail, please visit:
https://www.bezkoder.com/spring-boot-jwt-authentication/

## API Documentation

### Signup

1. Role = user
Endpoint POST: http://localhost:8080/api/auth/signup
Body 
```json
{
  "username": "test",
  "email" : "test@test.com",
  "password" : "12345678"
}
```

2. Role admin
Endpoint POST: http://localhost:8080/api/auth/signup
Body
```json
{
  "username": "test",
  "email" : "test@test.com",
  "password" : "12345678",
  "role": ["admin"]
}
```

### Signin
Endpoint POST: http://localhost:8080/api/auth/signin
Body
```json
{
  "username": "test",
  "password" : "12345678"
}
```
Response
```json
{
  "id": 1,
  "username": "test",
  "email": "test@test.com",
  "roles": [
    "ROLE_USER"
  ],
  "accessToken": "eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJtYW5qb3QiLCJpYXQiOjE3MDM4NDE1MzksImV4cCI6MTcwMzkyNzkzOX0.el59jHdPbhbqX5MPDCAidZQWpd2Y0FfGdb2gwmIzMzs",
  "tokenType": "Bearer"
}
```

### UserAccess
Endpoint GET: http://localhost:8080/api/test/user
Header : Authorization: Bearer {token}
Response : User Content.

### AdminAccess
Endpoint GET: http://localhost:8080/api/test/admin
Header : Authorization: Bearer {token}
Response : Admin Board.