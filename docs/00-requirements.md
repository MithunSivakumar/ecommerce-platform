# 🛒 E-Commerce Platform – Basic Requirements

## 1. Objective

Design and develop an e-commerce platform where customers can browse, purchase products, and track orders, while sellers manage their own products and admins manage the platform.

---

## 2. User Roles

The platform supports three types of users:

| Role     | Description                                     |
|----------|-------------------------------------------------|
| Admin    | Manages the platform, users, and overall system |
| Seller   | Lists and manages their own products            |
| Customer | Browses and purchases products                  |
 --------------------------------------------------------------
---

## 3. User Capabilities

### Admin

- Manage users (Admin, Seller, Customer)
- View platform-level data
- Has full administrative access

### Seller

- Create, update, and delete their own products
- View orders related to their products
- Update order status (e.g., shipped, delivered)

### Customer

- Browse products
- Add products to cart
- Place orders
- View current and past orders

---

## 4. Product & Category Management

- Products are grouped into categories
- Each category can contain multiple products
- Each product must include:
    - Name
    - Description
    - Price
    - Quantity (stock)
    - Category
    - Seller information

---

## 5. Cart Management

Customers can:

- Add products to cart
- Remove products from cart
- Update quantities
- View all items in their cart

Cart should store:

- Product list
- Quantity
- Total price

---

## 6. Order & Checkout

- Customers can convert a cart into an order
- On checkout:
    - Payment processing is initiated
    - An order is created
    - Initial order status is `PENDING`

Customers must be able to:

- View current orders
- View past order history
- Check order status

---

## 7. Order Status & Seller Updates

- Sellers can update the status of orders related to their products
- Example order statuses:
    - `PENDING`
    - `PAID`
    - `SHIPPED`
    - `DELIVERED`
    - `FAILED`

---

## 8. Notifications

Notifications must be sent to customers when:

- An order is placed
- Payment succeeds or fails
- Order status changes

---

## 9. Security & Authentication

- Users must be able to:
    - Sign up
    - Log in
- The system must support:
    - Role-based access control (Admin, Seller, Customer)
    - Secure authentication (e.g., JWT)
    - API-level authorization
