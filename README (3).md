Project Overview

The Vehicle Management System is a microservices-based application designed to manage users and their associated vehicles. It consists of the following services:

User Service: Handles user-related operations such as registration, retrieval, and association with vehicles.

Vehicle Service: Manages vehicle-related operations such as adding vehicles and retrieving vehicle details.

Eureka Discovery Service: Provides service discovery functionality for microservices.

API Gateway: Acts as a single entry point for all microservices, enabling routing and load balancing.



Architectures

Microservices Architecture

User Service:

Handles CRUD operations for users.

Communicates with the Vehicle Service using Feign Client for vehicle-related data.

Vehicle Service:

Handles CRUD operations for vehicles.

Provides endpoints for retrieving vehicle details.

Eureka Discovery Service:

Enables service registration and discovery.

Ensures dynamic scaling and fault tolerance.

API Gateway:

Routes requests to appropriate microservices.

Provides centralized authentication and logging.

Technology Stack

Programming Language: Java

Frameworks: Spring Boot, Spring Cloud

Database: H2 (In-memory database)

Service Discovery: Eureka

API Gateway: Spring Cloud Gateway

Build Tool: Maven

Database Table Design    

User Table

Vehicle Table



Endpoints

User Service

Vehicle Service



Sequence Diagram

User Registration:

User sends a POST request to /api/users/.

User Service saves the user details in the database.

Response is returned with the registered user details.

Fetch User with Vehicles:

User sends a GET request to /api/users/{userId}/vehicles.

User Service fetches user details from the database.

User Service calls Vehicle Service using Feign Client to fetch associated vehicles.

Combined response is returned.



Column Name | Data Type | Constraints | Description
userId | BIGINT | Primary Key, Auto-Increment | Unique identifier for the user
name | VARCHAR(255) | NOT NULL | Name of the user
email | VARCHAR(255) | NOT NULL, UNIQUE | Email address of the user
phone | VARCHAR(15) | NOT NULL | Phone number of the user
address | VARCHAR(255) |  | Address of the user
passwordHash | VARCHAR(255) | NOT NULL | Hashed password of the user

Column Name | Data Type | Constraints | Description
vehicleId | BIGINT | Primary Key, Auto-Increment | Unique identifier for the vehicle
make | VARCHAR(255) | NOT NULL | Manufacturer of the vehicle

Endpoint | Method | Description | Request Body/Params
/api/users/ | POST | Register a new user | User object
/api/users/{email} | GET | Retrieve user by email | email (Path Variable)
/api/users | GET | Retrieve all users | None
/api/users/{userId}/vehicles | GET | Retrieve vehicles associated with a user | userId (Path Variable)

Endpoint | Method | Description | Request Body/Params
/api/vehicles/ | POST | Add a new vehicle | VehicleRequest object
/api/vehicles/user/{userId} | GET | Retrieve vehicles by user ID | userId (Path Variable)

