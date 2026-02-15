# High Level Design (HLD)

## E-Commerce Platform

---

## 1. System Overview

This system is a microservices-based e-commerce platform that allows Customers to browse and purchase products, Sellers to manage their products, and Admins to manage the platform.  
The platform supports secure authentication, shopping cart, order processing, payment handling, and notifications.

The system is designed to be cloud-ready and deployable on SAP BTP.

---

## 2. Architecture Style

The system follows these architectural principles:

- Microservices-based architecture
- API Gateway / Router pattern
- Event-driven communication for order and payment workflows
- Stateless services
- Database-per-service pattern

Synchronous communication is done using REST APIs and asynchronous workflows are handled through Kafka.

---

## 3. High-Level Components

The system consists of the following components:

- API Gateway / Router
- User Service
- Product Service
- Category Service
- Cart Service
- Order Service
- Payment Service
- Notification Service
- Kafka (Event broker)
- Redis (Cart storage)
- PostgreSQL (Persistent data storage)

---

## 4. Service Responsibilities

| Service              | Responsibility                                            |
|----------------------|-----------------------------------------------------------|
| User Service         | User registration, login, roles (Admin, Seller, Customer) |
| Product Service      | Create, update, delete, and search products               |
| Category Service     | Manage product categories                                 |
| Cart Service         | Manage shopping cart for customers                        |
| Order Service        | Create and manage orders                                  |
| Payment Service      | Process payments and update payment status                |
| Notification Service | Send notifications on order and payment events            |

---

## 5. Data Ownership

Each microservice owns its own data store.

| Service              | Database                 |
|----------------------|--------------------------|
| User Service         | PostgreSQL               |
| Product Service      | PostgreSQL               |
| Category Service     | PostgreSQL               |
| Order Service        | PostgreSQL               |
| Payment Service      | PostgreSQL               |
| Cart Service         | Redis                    |
| Notification Service | PostgreSQL / Log storage |

No service is allowed to directly access another service’s database.

---

## 6. Communication Model

### Synchronous Communication (REST)

- Customer → API Gateway → User, Product, Category, Cart, Order services
- Seller → API Gateway → Product, Order services
- Admin → API Gateway → User, Product, Category services

### Asynchronous Communication (Kafka)

- Order Service publishes `OrderCreated` events
- Payment Service consumes `OrderCreated` events and processes payment
- Payment Service publishes `PaymentSuccess` or `PaymentFailed` events
- Order Service consumes payment events and updates order status
- Notification Service consumes order and payment events to notify users

---

## 7. Order Processing Flow

1. Customer places an order via API Gateway
2. Order Service creates the order with status `PENDING`
3. Order Service publishes an `OrderCreated` event to Kafka
4. Payment Service processes payment
5. Payment Service publishes result to Kafka
6. Order Service updates order status
7. Notification Service sends notifications to the customer

---

## 8. Security Model

- Users authenticate using username and password
- On successful login, a JWT token is issued
- API Gateway validates JWT on every request
- Role-based access control is applied (Admin, Seller, Customer)

---

## 9. Deployment View

- Each microservice is deployed independently
- Kafka, Redis, and PostgreSQL run as managed or containerized services
- API Gateway routes external requests to internal services
- The architecture is compatible with deployment on SAP BTP

---

## 10. Observability & Reliability

- Each service logs requests and errors
- Correlation IDs are used for tracing requests across services
- Kafka ensures reliable event delivery
- Failed payments and order updates can be retried

---
