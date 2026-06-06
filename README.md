# CoachHub — Backend

A private coaching application REST API built with Spring Boot.

## Live Demo
- Backend API: Coming soon
- Frontend: Coming soon

## GitHub Repositories
- Backend: https://github.com/mdewmini/coaching-backend
- Frontend: https://github.com/mdewmini/coaching-frontend

## Tech Stack
- Java 17
- Spring Boot 3.5
- Spring Security
- JWT Authentication (jjwt 0.11.5)
- Spring Data JPA
- H2 In-Memory Database
- Lombok
- Maven

## API Endpoints

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/api/auth/health` | Health check | No |
| POST | `/api/auth/register` | Register new user | No |
| POST | `/api/auth/login` | Login user | No |

### Register Request
```json
POST /api/auth/register
{
  "name": "Maheesha Dewmini",
  "email": "maheesha@gmail.com",
  "password": "password123"
}
```

### Register Response
```json
{
  "token": "eyJhbGciOiJIUzI1NiJ9...",
  "email": "maheesha@gmail.com",
  "name": "Maheesha Dewmini",
  "message": "Registration successful"
}
```

### Login Request
```json
POST /api/auth/login
{
  "email": "maheesha@gmail.com",
  "password": "password123"
}
```

### Login Response
```json
{
  "token": "eyJhbGciOiJIUzI1NiJ9...",
  "email": "maheesha@gmail.com", 
  "name": "Maheesha Dewmini",
  "message": "Login successful"
}
```

### Error Response
```json
{
  "error": "Invalid email or password"
}
```

## Setup Instructions

### Prerequisites
- Java 17
- Maven

### Installation

```bash
# Clone the repo
git clone https://github.com/mdewmini/coaching-backend.git
cd coaching-backend

# Run the application
./mvnw spring-boot:run
```

API runs at http://localhost:8080

### Environment Variables
| Variable | Description | Default |
|----------|-------------|---------|
| `JWT_SECRET` | JWT signing key | Set in application.properties |
| `JWT_EXPIRATION` | Token expiry (ms) | 86400000 (1 day) |

## Project Structure

src/main/java/com/coaching/app/
├── CoachingBackendApplication.java
├── config/
│   └── SecurityConfig.java      # CORS + Security config
├── controller/
│   └── AuthController.java      # Auth endpoints
├── dto/
│   ├── LoginRequest.java
│   ├── RegisterRequest.java
│   └── AuthResponse.java
├── entity/
│   └── User.java                # User model
├── repository/
│   └── UserRepository.java      # Database queries
├── service/
│   ├── AuthService.java         # Business logic
│   └── JwtService.java          # JWT operations
└── exception/
└── GlobalExceptionHandler.java

## Security
- Passwords encrypted with BCrypt
- JWT tokens expire after 24 hours
- CORS configured for frontend URL
- Stateless session management

## Testing the API

```bash
# Health check
curl http://localhost:8080/api/auth/health

# Register
curl -X POST http://localhost:8080/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{"name":"Test","email":"test@gmail.com","password":"test123"}'

# Login
curl -X POST http://localhost:8080/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email":"test@gmail.com","password":"test123"}'
```
