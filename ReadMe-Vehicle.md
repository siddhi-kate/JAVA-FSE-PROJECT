## 📚 Table of Contents

- [Vehicle Service](#vehicle-service)
- [Component Diagram](#component-diagram)
- [Key Features](#key-features)
- [Database Table Design](#database-table-design)
- [Endpoints](#endpoints)
- [Sequence Diagrams](#sequence-diagrams)
- [Swagger Documentation](#swagger-documentation)

---

# 🚗 Vehicle Service

The **Vehicle Service** is a core microservice in the system responsible for managing vehicle-related operations such as creation, retrieval, update, and deletion. It integrates with the **User Service** via Feign Client to fetch user-specific vehicle data.

---

## Database Table Design
---
#### Vehicle Table

| Column Name         | Data Type      | Constraints                 | Description                             |
|---------------------|----------------|------------------------------|-----------------------------------------|
| `vehicleId`         | `BIGINT`       | Primary Key, Auto-Increment | Unique identifier for the vehicle       |
| `userId`            | `BIGINT`       | Foreign Key, NOT NULL       | ID of the user who owns the vehicle     |
| `make`              | `VARCHAR(255)` | NOT NULL                    | Manufacturer of the vehicle             |
| `model`             | `VARCHAR(255)` | NOT NULL                    | Model name of the vehicle               |
| `year`              | `INT`          | NOT NULL                    | Manufacturing year of the vehicle       |
| `registrationNumber`| `VARCHAR(50)`  | NOT NULL, UNIQUE            | Vehicle's registration number           |

---

## Endpoints

#### Vehicle Service Endpoints

| Endpoint                                | Method | Description                        | Request Body/Params         |
|-----------------------------------------|--------|------------------------------------|------------------------------|
| `/api/vehicles/`                        | POST   | Add a new vehicle                  | `VehicleRequest` object      |
| `/api/vehicles/user/{userId}`           | GET    | Retrieve vehicles by user ID       | `userId` (Path Variable)     |
| `/api/vehicles/{vehicleId}`             | GET    | Retrieve vehicle by vehicle ID     | `vehicleId` (Path Variable)  |
| `/api/vehicles/{vehicleId}`             | PUT    | Update vehicle details             | `VehicleRequest` object      |
| `/api/vehicles/{vehicleId}`             | DELETE | Delete a vehicle                   | `vehicleId` (Path Variable)  |

---

## Sequence Diagrams

### Vehicle Registration

```mermaid
sequenceDiagram
    participant User
    participant API Gateway
    participant VehicleService
    participant VehicleDB

    User->>API Gateway: POST /api/vehicles/ (VehicleRequest object)
    API Gateway->>VehicleService: Route request
    VehicleService->>VehicleService: Validate vehicle data
    VehicleService->>VehicleDB: Save vehicle details
    VehicleDB-->>VehicleService: Vehicle details saved
    VehicleService-->>API Gateway: Response with added vehicle details
    API Gateway-->>User: Response with added vehicle details
```

## Swagger Documentation
The Vehicle Service provides interactive API documentation using Swagger.

### Access Swagger UI
Swagger UI for Vehicle Service
    - http://localhost:8083/swagger-ui/index.html
