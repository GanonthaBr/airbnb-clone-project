# 🏡 Airbnb Backend Clone

## Overview

This project is a backend clone of the Airbnb platform, designed to replicate core features such as property listings, bookings, user management, and reviews. The main goal is to build a robust, scalable, and API-driven backend that can serve as the foundation for a full-stack application or be integrated with a separate frontend (e.g., web or mobile).

## 🌟 Project Goals

- Implement essential Airbnb functionalities (user auth, listing management, bookings, reviews).
- Provide a modern and efficient API using GraphQL.
- Ensure secure, maintainable, and scalable backend architecture.
- Leverage Django’s built-in admin and ORM for rapid development.
- Store and manage relational data efficiently with PostgreSQL.

## 🛠️ Technology Stack

- **Django** – Web framework for building robust backend systems.
- **PostgreSQL** – Relational database for structured and reliable data storage.
- **GraphQL (Graphene-Django)** – API layer for flexible and efficient data querying.
- **Django REST Framework** *(optional)* – For RESTful API support if needed.
- **Docker** *(optional)* – Containerized development and deployment.
- **JWT Authentication** – Secure token-based user authentication.
- **Celery & Redis** *(optional)* – Background task processing (e.g., email notifications).

## 🗃️ Database Design

The project consists of several core entities to replicate Airbnb's functionality. Below is a summary of the key models and their relationships.

### 🔐 Users
Represents individuals using the platform, either as guests or hosts.

**Key Fields:**
- `id`: Unique identifier
- `username`: User’s login name
- `email`: User’s contact email
- `is_host`: Boolean to distinguish hosts from guests
- `date_joined`: Timestamp of account creation

**Relationships:**
- A user can list multiple properties (if a host)
- A user can make multiple bookings
- A user can write multiple reviews

---

### 🏠 Properties
Represents homes or spaces listed for rent.

**Key Fields:**
- `id`: Unique identifier
- `title`: Name or short description of the property
- `description`: Detailed property information
- `price_per_night`: Cost to book per night
- `owner`: Foreign key to the `User` (host)

**Relationships:**
- A property is owned by a single user (host)
- A property can have multiple bookings
- A property can receive multiple reviews

---

### 📅 Bookings
Represents a reservation made by a guest for a property.

**Key Fields:**
- `id`: Unique identifier
- `guest`: Foreign key to the `User` (guest)
- `property`: Foreign key to the `Property`
- `start_date`: Booking start date
- `end_date`: Booking end date

**Relationships:**
- A booking belongs to one property
- A booking is made by one user (guest)

---

### 📝 Reviews
Represents feedback from guests about properties.

**Key Fields:**
- `id`: Unique identifier
- `author`: Foreign key to the `User`
- `property`: Foreign key to the `Property`
- `rating`: Integer score (e.g., 1 to 5)
- `comment`: Textual feedback

**Relationships:**
- A review is written by one user
- A review is associated with one property

---

### 💳 Payments
Handles payment transactions for bookings.

**Key Fields:**
- `id`: Unique identifier
- `booking`: Foreign key to the `Booking`
- `amount`: Total amount paid
- `payment_status`: Status (e.g., "completed", "pending", "failed")
- `payment_date`: Date of transaction

**Relationships:**
- A payment is linked to one booking

---

### 🔄 Entity Relationships Summary

- A **User** can own multiple **Properties**
- A **User** can make multiple **Bookings**
- A **Property** can have multiple **Bookings**
- A **Booking** can have one **Payment**
- A **User** can write multiple **Reviews** for different **Properties**

## 🧩 Feature Breakdown

This section outlines the main features implemented in the Airbnb Backend Clone, highlighting their purpose and contribution to the overall functionality of the platform.

### 📄 API Documentation
The backend APIs are documented using the **OpenAPI** standard, making integration with frontend clients seamless and well-structured. It also includes **GraphQL** for more efficient and flexible queries, and the **Django REST Framework** to expose RESTful endpoints for CRUD operations.

### 🔐 User Authentication
Users can register, log in, and manage their profiles through dedicated endpoints (`/users/`, `/users/{user_id}/`). Secure authentication mechanisms ensure that only authorized users can access or modify their data.

### 🏠 Property Management
Hosts can list, edit, retrieve, or delete properties through endpoints such as `/properties/` and `/properties/{property_id}/`. This feature enables users to manage their rental spaces with ease and efficiency.

### 📅 Booking System
The booking system allows users to reserve properties for specific dates via `/bookings/` and `/bookings/{booking_id}/`. It handles all operations related to check-in, check-out, and booking modifications.

### 💳 Payment Processing
Payments related to bookings are handled securely via the `/payments/` endpoint. This feature ensures that financial transactions are tracked and processed efficiently.

### 📝 Review System
Guests can post and manage reviews about properties using `/reviews/` and `/reviews/{review_id}/`. Reviews help build trust among users and improve the quality of listings on the platform.

### 🚀 Database Optimizations
To maintain performance at scale, the backend employs **indexing** for frequently queried data and **caching** to reduce server load and latency. These strategies enhance the responsiveness and reliability of the system.

