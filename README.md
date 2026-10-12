# Grievance Management API

A Spring Boot REST backend for a citizen/employee grievance redressal system. Users
raise grievances against departments; the system categorises them, threads comments,
and notifies by email as they move through resolution.

**Spring Boot · Java · Spring Security · Spring Data JPA · MySQL · Spring Mail · Lombok**

---

## Domain

| Entity | Role |
|---|---|
| **User** | Account that raises and tracks grievances |
| **Department** | Owning unit a grievance is routed to |
| **GrievanceCategory** | Classification of a grievance |
| **Grievance** | The complaint itself, with status and ownership |
| **Comment** | Threaded updates and responses on a grievance |

## Architecture

Clean layered architecture — each concern in its own package:

```
com.examly.springapp
├── controller/   # REST endpoints: User, Department, GrievanceCategory, Grievance, Comment
├── service/      # business logic (interface + Impl per domain)
├── repository/   # Spring Data JPA repositories
├── model/        # JPA entities
├── dto/          # request DTOs (UserRequest, GrievanceCategoryRequest)
└── exception/    # GlobalExceptionHandler for consistent error responses
```

- **Spring Security** guards the API.
- **Spring Mail** sends grievance notifications.
- **Bean validation** (`spring-boot-starter-validation`) validates incoming DTOs.
- **GlobalExceptionHandler** centralises error handling into consistent responses.

## Run it

Requires Java and a running MySQL instance.

```bash
cd springapp
# set your DB + mail credentials in src/main/resources/application.properties
./mvnw spring-boot:run        # mvnw.cmd on Windows
```

Build and test:

```bash
./mvnw clean test
./mvnw clean package
```

## Notes

Configure `application.properties` with your own MySQL URL, credentials, and SMTP
settings before running. No credentials are committed to this repository.
