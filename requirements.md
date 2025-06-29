# Backend Requirement Specifications

This document outlines the technical and functional requirements for three core backend features in the Airbnb Clone project.

---

## 1. User Authentication

### Description:
Handles user registration and login for guests and hosts.

### API Endpoints:
- `POST /api/register/`  
- `POST /api/login/`

### Input Specifications:
- `email`: string (valid email format, required)
- `password`: string (min. 8 characters, required)
- `role`: string ("guest" or "host", required)

### Output Specifications:
- On success: JSON with user info and access token
- On error: JSON with error message and status code

### Validation Rules:
- Email must be unique
- Password must be at least 8 characters
- Role must be either "guest" or "host"

### Performance Criteria:
- Response time < 500ms
- Token-based authentication (JWT)

---

## 2. Property Management

### Description:
Enables hosts to add, edit, and delete property listings.

### API Endpoints:
- `POST /api/properties/`
- `PUT /api/properties/<id>/`
- `DELETE /api/properties/<id>/`
- `GET /api/properties/`

### Input Specifications:
- `title`: string (required)
- `description`: string (required)
- `location`: string (required)
- `price`: float (required, ≥ 0)
- `availability`: boolean (default true)

### Output Specifications:
- On success: JSON with property data
- On error: JSON with error message

### Validation Rules:
- Title and location must be non-empty
- Price must be ≥ 0

### Performance Criteria:
- Max listing response time: 300ms
- Supports pagination and filtering

---

## 3. Booking System

### Description:
Allows guests to book and cancel reservations.

### API Endpoints:
- `POST /api/bookings/`
- `DELETE /api/bookings/<id>/`
- `GET /api/bookings/`

### Input Specifications:
- `property_id`: UUID (required)
- `start_date`: date (required)
- `end_date`: date (required)

### Output Specifications:
- On success: Booking confirmation with reservation ID
- On error: Validation message or unavailability notice

### Validation Rules:
- Start date must be before end date
- Property must be available during selected dates

### Performance Criteria:
- Booking availability check in < 400ms
- Prevents double-booking with atomic transactions