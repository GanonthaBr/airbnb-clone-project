# 🏠 Airbnb Database Entity-Relationship (ER) Diagram

## 📦 Entities and Attributes

### 1. **User**
- `user_id`: UUID, Primary Key, Indexed
- `first_name`: VARCHAR, NOT NULL
- `last_name`: VARCHAR, NOT NULL
- `email`: VARCHAR, UNIQUE, NOT NULL (Indexed)
- `password_hash`: VARCHAR, NOT NULL
- `phone_number`: VARCHAR, NULL
- `role`: ENUM (`guest`, `host`, `admin`), NOT NULL
- `created_at`: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP

---

### 2. **Property**
- `property_id`: UUID, Primary Key, Indexed
- `host_id`: UUID, Foreign Key → User(`user_id`)
- `name`: VARCHAR, NOT NULL
- `description`: TEXT, NOT NULL
- `location`: VARCHAR, NOT NULL
- `pricepernight`: DECIMAL, NOT NULL
- `created_at`: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP
- `updated_at`: TIMESTAMP, ON UPDATE CURRENT_TIMESTAMP

---

### 3. **Booking**
- `booking_id`: UUID, Primary Key, Indexed
- `property_id`: UUID, Foreign Key → Property(`property_id`)
- `user_id`: UUID, Foreign Key → User(`user_id`)
- `start_date`: DATE, NOT NULL
- `end_date`: DATE, NOT NULL
- `total_price`: DECIMAL, NOT NULL
- `status`: ENUM (`pending`, `confirmed`, `canceled`), NOT NULL
- `created_at`: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP

---

### 4. **Payment**
- `payment_id`: UUID, Primary Key, Indexed
- `booking_id`: UUID, Foreign Key → Booking(`booking_id`)
- `amount`: DECIMAL, NOT NULL
- `payment_date`: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP
- `payment_method`: ENUM (`credit_card`, `paypal`, `stripe`), NOT NULL

---

### 5. **Review**
- `review_id`: UUID, Primary Key, Indexed
- `property_id`: UUID, Foreign Key → Property(`property_id`)
- `user_id`: UUID, Foreign Key → User(`user_id`)
- `rating`: INTEGER (1–5), NOT NULL
- `comment`: TEXT, NOT NULL
- `created_at`: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP

---

### 6. **Message**
- `message_id`: UUID, Primary Key, Indexed
- `sender_id`: UUID, Foreign Key → User(`user_id`)
- `recipient_id`: UUID, Foreign Key → User(`user_id`)
- `message_body`: TEXT, NOT NULL
- `sent_at`: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP

---

## 🔗 Relationships

| Relationship                 | Cardinality           | Description                                                                 |
|-----------------------------|------------------------|-----------------------------------------------------------------------------|
| User → Property              | 1 to Many              | A host can create multiple properties.                                     |
| User → Booking               | 1 to Many              | A guest can make multiple bookings.                                        |
| Property → Booking           | 1 to Many              | A property can be booked many times.                                       |
| Booking → Payment            | 1 to 1                 | Each booking has exactly one payment.                                      |
| User → Review                | 1 to Many              | A user can leave many reviews.                                             |
| Property → Review            | 1 to Many              | A property can have multiple reviews.                                      |
| User (sender) → Message      | 1 to Many              | A user can send multiple messages.                                         |
| User (recipient) → Message   | 1 to Many              | A user can receive multiple messages.                                      |

---

## 🔒 Constraints and Indexes

- `User.email`: UNIQUE, Indexed
- `User.role`: ENUM constraint
- `Booking.status`: ENUM constraint (`pending`, `confirmed`, `canceled`)
- `Review.rating`: CHECK (1 <= rating <= 5)
- Foreign key constraints between all related entities
- All primary keys (`UUID`) are automatically indexed

---

