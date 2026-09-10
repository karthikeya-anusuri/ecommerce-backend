# E-Commerce Backend

A RESTful E-Commerce Backend application built using Java, Spring Boot, Spring Security, JWT, JPA/Hibernate, MySQL, and Swagger/OpenAPI.

## Features

- User registration and management
- BCrypt password encryption
- JWT-based authentication
- Role-based authorization
- USER and ADMIN roles
- Product CRUD operations
- Product search and filtering
- Product pagination
- Category management
- Shopping cart
- Order placement
- Order cancellation
- Automatic stock management
- Payment processing
- Order status management
- User data isolation
- Global exception handling
- Input validation
- Swagger/OpenAPI documentation

## Technologies

- Java 21
- Spring Boot 4
- Spring Security
- JWT
- Spring Data JPA
- Hibernate
- MySQL 8
- Maven
- Swagger / OpenAPI
- Postman
- Git
- GitHub
- Railway

## Architecture

The project follows a layered architecture:

```text
Controller
    ↓
Service
    ↓
Repository
    ↓
Database

### Main Packages

- `controller` - REST API controllers
- `service` - Business logic
- `repository` - Database access
- `entity` - JPA entities
- `dto` - Request and response DTOs
- `security` - JWT and Spring Security
- `exception` - Custom exceptions and global exception handling
- `config` - Application configuration
- `category` - Category management
- `user` - User management
- `cart` - Shopping cart
- `order` - Order management
- `payment` - Payment management

## Authentication

The application uses JWT-based authentication.

### Login

```http
POST /api/auth/login
Exampl request:

{
  "email": "user@example.com",
  "password": "your-password"
}

Example response:

{
  "token": "<JWT_TOKEN>",
  "tokenType": "Bearer"
}
> Example credentials are for demonstration purposes only.

## API Endpoints

### Authentication

| Method | Endpoint | Description |
|---|---|---|
| POST | `/api/auth/login` | User login |

### Products

| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/products` | Get all products |
| GET | `/api/products/{id}` | Get product by ID |
| POST | `/api/products` | Create product |
| PUT | `/api/products/{id}` | Update product |
| DELETE | `/api/products/{id}` | Delete product |

Additional product functionality:

- Search products by name
- Filter products by price
- Filter products by category
- Get products that are in stock
- Pagination

### Categories

| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/categories` | Get all categories |
| GET | `/api/categories/{id}` | Get category by ID |
| POST | `/api/categories` | Create category |
| PUT | `/api/categories/{id}` | Update category |
| DELETE | `/api/categories/{id}` | Delete category |

### Users

| Method | Endpoint | Description |
|---|---|---|
| POST | `/api/users` | Register user |
| GET | `/api/users` | Get all users |
| GET | `/api/users/{id}` | Get user by ID |
| PUT | `/api/users/{id}` | Update user |
| DELETE | `/api/users/{id}` | Delete user |

User management is protected using role-based authorization.

### Cart

| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/cart` | Get current user's cart |
| POST | `/api/cart/add/{productId}` | Add product to cart |
| PUT | `/api/cart/item/{itemId}` | Update cart item quantity |
| DELETE | `/api/cart/item/{itemId}` | Remove cart item |
| DELETE | `/api/cart/clear` | Clear cart |

### Orders

| Method | Endpoint | Description |
|---|---|---|
| POST | `/api/orders` | Place an order |
| GET | `/api/orders` | Get current user's orders |
| GET | `/api/orders/{orderId}/items` | Get order items |
| PUT | `/api/orders/{orderId}/cancel` | Cancel pending order |

### Admin Order Management

| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/orders/admin` | Get all orders |
| PUT | `/api/orders/admin/{orderId}/status` | Update order status |

Supported order statuses:

- `PENDING`
- `CONFIRMED`
- `SHIPPED`
- `DELIVERED`
- `CANCELLED`
- `PAID`

### Payments

| Method | Endpoint | Description |
|---|---|---|
| POST | `/api/payments/{orderId}` | Process payment |
| GET | `/api/payments/order/{orderId}` | Get payment for an order |

Supported payment methods:

- `UPI`
- `CARD`
- `COD`

## Database

The application uses:

- MySQL 8
- Spring Data JPA
- Hibernate

Main database entities include:

```text
User
Category
Product
Cart
CartItem
Order
OrderItem
Payment

## Validation and Exception Handling

The application implements input validation using Jakarta Validation.

Examples include:

- Required product name
- Required product description
- Positive product price
- Non-negative stock
- Required category
- Required user information

Global exception handling provides consistent API error responses for:

- Validation errors
- Resource not found
- Duplicate resources
- Invalid requests
- Unexpected server errors

## Order Processing

The order workflow includes:

```text
Cart
 ↓
Stock Validation
 ↓
Calculate Order Total
 ↓
Create Order
 ↓
Create Order Items
 ↓
Reduce Product Stock
 ↓
Clear Cart
> Order processing is transactional to maintain database consistency.

> When a pending order is cancelled:
Cancelled Order
       ↓
Restore Product Stock
       ↓
Update Order Status

## Security

Spring Security is used to protect the REST APIs.

Security features include:

- JWT authentication
- Role-based authorization
- Stateless authentication
- BCrypt password hashing
- User ownership validation
- Protected admin operations

Users can access only their own cart, orders, order items, and payments.

Administrative operations are restricted to users with the `ADMIN` role.

## API Documentation

Swagger/OpenAPI is integrated into the project for API documentation and testing.

### Local Swagger

```text
http://localhost:8080/swagger-ui/index.html

## Production Swagger
https://ecommerce-backend-production-ceaa.up.railway.app/swagger-ui/index.html

##Swagger provides:

- API endpoint documentation
- Request and response information
- JWT authorization
- Interactive API testing

## API Testing

The REST APIs were tested using:

- Postman
- Swagger/OpenAPI

Testing covered:

- Authentication
- Authorization
- Product operations
- Category operations
- User operations
- Cart operations
- Order processing
- Order cancellation
- Stock management
- Payment processing
- Admin operations
- Validation
- Error handling
- User data isolation

## Deployment

The application is deployed on Railway.

The backend is connected to a MySQL database and deployed as a Spring Boot application.

### Production API

```text
https://ecommerce-backend-production-ceaa.up.railway.app
```

### Production Swagger

```text
https://ecommerce-backend-production-ceaa.up.railway.app/swagger-ui/index.html
```

### Deployment Platform

- Railway (Cloud Hosting)
- MySQL Database
- Spring Boot Application
- Environment Variables for secure configuration

## Running Locally

### Prerequisites

- Java 21
- MySQL 8
- Git

### Clone the Repository

```bash
git clone https://github.com/karthikeya-anusuri/ecommerce-backend.git
```

Navigate to the project:

```bash
cd ecommerce-backend
```

### Configure MySQL

Create the database:

```sql
CREATE DATABASE ecommerce_db;
```

Configure the database connection in:

```text
src/main/resources/application.properties
```

Do not commit database passwords, JWT secrets, or other sensitive information to GitHub.

### Run the Application

For Windows:

```powershell
.\mvnw.cmd spring-boot:run
```

For Linux/macOS:

```bash
./mvnw spring-boot:run
```

The application will start on:

```text
http://localhost:8080
```

## Build the Project

For Windows:

```powershell
.\mvnw.cmd clean package
```

For Linux/macOS:

```bash
./mvnw clean package
```

A successful build confirms that the project compiles correctly and the required dependencies are available.

## Project Structure

```text
ecommerce
└── src
    └── main
        ├── java
        │   └── com.example.ecommerce
        │       ├── controller
        │       ├── entity
        │       ├── repository
        │       ├── service
        │       ├── dto
        │       ├── security
        │       ├── exception
        │       ├── config
        │       ├── category
        │       ├── user
        │       ├── cart
        │       ├── order
        │       └── payment
        │
        └── resources
            └── application.properties
```

## GitHub

Source code:

https://github.com/karthikeya-anusuri/ecommerce-backend

## Key Learning Areas

This project provided practical experience with:

- Java backend development
- Spring Boot
- REST API development
- Spring Security
- JWT authentication
- Role-based authorization
- Spring Data JPA
- Hibernate
- MySQL
- Database relationships
- DTO-based API design
- Input validation
- Exception handling
- Transaction management
- API testing
- Swagger/OpenAPI
- Git and GitHub
- Cloud deployment

## Future Improvements

Possible future enhancements include:

- Product image management
- Wishlist functionality
- Coupon and discount management
- Email notifications
- Advanced product sorting
- Payment gateway integration
- Refresh token support
- Automated tests
- Docker containerization
- CI/CD pipeline

## Author

**Karthikeya Anusuri**

CSE Graduate | Java | SQL | Backend Development

GitHub:

https://github.com/karthikeya-anusuri

LinkedIn:

www.linkedin.com/in/karthikeya0715

## License

This project is developed for learning and portfolio purposes.