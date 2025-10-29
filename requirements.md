# Airbnb Clone Backend - Requirements Specification

##  Objective
This document defines the technical and functional requirements for the Airbnb Clone backend system. It focuses on three core backend modules: User Authentication,Property Management, and Booking System.


# 📘 1. User Authentication

# 🔹 Functional Overview
The authentication system allows users (Guests, Hosts, Admins) to securely register, log in, and manage their accounts.

### 🔹 API Endpoints
| Method | Endpoint             | Description                               |
|--------|----------------------|-------------------------------------------|
| `POST` | `/api/auth/register` | Registers a new user                      |
| `POST` | `/api/auth/login`    | Authenticates user credentials            |
| `GET`  | `/api/auth/profile`  | Retrieves user profile (JWT required)     |
| `PUT`  | `/api/auth/profile`  | Updates user profile information          |
| `POST` | `/api/auth/logout`   | Logs out a user by invalidating the token |

### Input Specifications
# ` /api/auth/register`
```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "strongPassword123",
  "role": "host"
}
```
Output (Success)
```json 
{
  "message": "User registered successfully",
  "user": {
    "id": "u123",
    "name": "John Doe",
    "email": "john@example.com",
    "role": "host"
  },
  "token": "jwt_token_here"
}
```
### Validation Rules

Email must be unique and valid.

Password must have at least 8 characters, including uppercase, lowercase, and a number.

Role must be one of: guest, host, admin.

###  Performance Criteria

Registration response time < 2 seconds

JWT token valid for 24 hours

Failed login attempts limited to 5 per hour per IP

# 📗2. Property Management

🔹 Functional Overview
Hosts can create, edit, delete, and manage property listings.

Guests can view and search properties based on location, price, and availability.

### API Endpoints


| Method | Endpoint             | Description                               |
|--------|----------------------|-------------------------------------------|
| `POST` | /api/properties	    |Add a new property (Host only)             |
| `GET ` | /api/properties	    |  Get all properties with filters          |
| `GET`  | /api/properties/:id	|  Get a single property by ID              |
| `PUT| ` /api/properties/:id	  | Update property details                   |
| `POST` | `/api/auth/logout`   | 	Delete property listing                 |

Input Example

### /api/properties (Add Property)
```json
{
  "title": "Modern Apartment in Addis Ababa",
  "description": "2-bedroom apartment with Wi-Fi and parking.",
  "price": 85,
  "location": "Addis Ababa, Ethiopia",
  "amenities": ["Wi-Fi", "Parking", "Kitchen"],
  "availability": true
}
```
##  Output Example
```json
{
  "message": "Property added successfully",
  "property": {
    "id": "p101",
    "title": "Modern Apartment in Addis Ababa",
    "price": 85,
    "host_id": "u123"
  }
}
```

### Validation Rules

-- Title, description, price, and location are required.

-- Price must be a positive integer.

-- Host must be authenticated and authorized.

### Performance Criteria
-- Database query time for property search: < 500ms

-- Support pagination (default 10 properties per page)

-- Use caching for frequent search queries.

# 📙 3. Booking System

###  Functional Overview

The booking system handles all booking-related operations, including availability checks, booking confirmation, cancellations, and notifications.

🔹 API Endpoints 

| Method | Endpoint                | Description                               |
|--------|----------------------   |-------------------------------------------|
| `POST` |  /api/bookings          | Create a new booking                      |
| `GET ` |  /api/bookings/:id  	   | Retrieve booking details                  |
| `GET`  |  /api/bookings/user/:id | Get all bookings by user                  |
| `DELETE| `/api/bookings/:id      | Cancel a booking                          |


 ## Input Example

/api/bookings (Create Booking)
```json
{
  "property_id": "p101",
  "user_id": "u555",
  "check_in": "2025-11-01",
  "check_out": "2025-11-05",
  "payment_method": "credit_card"
}
```
## Output Example

```json
{
  "message": "Booking confirmed successfully",
  "booking": {
    "id": "b567",
    "property_id": "p101",
    "user_id": "u555",
    "status": "confirmed",
    "total_price": 340
  }
}
```
### Validation Rules

-- Dates must be valid and not overlap with existing bookings.

-- Property must be available.

-- Payment must be confirmed before booking confirmation.

### Performance Criteria

-- Booking confirmation time < 3 seconds

-- Prevent duplicate or overlapping bookings.

-- Implement asynchronous confirmation notifications via email.

### General Notes

All APIs return appropriate HTTP status codes:

-- 200 OK for successful requests

-- 400 Bad Request for validation errors

-- 401 Unauthorized for invalid JWT

-- 404 Not Found for missing resources

-- All sensitive data (passwords, tokens) are encrypted using bcrypt and JWT.

### Summary

-- This document ensures the Airbnb Clone backend supports:

-- Secure user registration and authentication.

-- Scalable property listing management.

-- Reliable and validated booking functionality.