# 📘 Backend Requirement Specifications – ALX Airbnb Project

This document outlines the functional and technical requirements for three core backend features of the Airbnb clone: **User Authentication**, **Property Management**, and **Booking System**.

---

## 1. 🔐 User Authentication

### ✅ Description
Handles user registration, login, and logout using token-based authentication (e.g., JWT).

### 🔗 API Endpoints
- `POST /api/register/` – Register a new user
- `POST /api/login/` – Log in and obtain token
- `POST /api/logout/` – Invalidate token

### 📥 Input Specifications
- **Register/Login**
  - `email`: string, required, valid format
  - `password`: string, required, min 8 characters
  - `username`: string, required (register only)

### 📤 Output
- On success: JSON with user info and auth token
- On failure: JSON with error messages

### ✅ Validation Rules
- Unique email and username
- Strong password (min length, symbols, numbers)

### ⚙️ Performance Criteria
- Token generation in < 500ms
- Rate limit login attempts (e.g., 5/min/IP)

---

## 2. 🏠 Property Management

### ✅ Description
Allows hosts to create, update, delete, and list properties they offer for booking.

### 🔗 API Endpoints
- `POST /api/properties/` – Create property
- `GET /api/properties/` – List all properties
- `GET /api/properties/<id>/` – Retrieve property
- `PUT /api/properties/<id>/` – Update property
- `DELETE /api/properties/<id>/` – Delete property

### 📥 Input Specifications
- `title`: string, required
- `description`: string, optional
- `location`: string, required
- `price_per_night`: float, required
- `host_id`: UUID, auto-assigned
- `available_dates`: array of date ranges

### 📤 Output
- JSON object with property details
- Error message if unauthorized or invalid

### ✅ Validation Rules
- Price must be positive
- Location must not be empty
- Authenticated users only

### ⚙️ Performance Criteria
- List properties with pagination (default: 20/page)
- Support filtering by location, price range

---

## 3. 📆 Booking System

### ✅ Description
Enables users to book available properties for specific dates.

### 🔗 API Endpoints
- `POST /api/bookings/` – Create booking
- `GET /api/bookings/` – List user bookings
- `DELETE /api/bookings/<id>/` – Cancel booking

### 📥 Input Specifications
- `property_id`: UUID, required
- `check_in`: date, required
- `check_out`: date, required
- `user_id`: auto-assigned from token

### 📤 Output
- Booking confirmation with total price
- Conflict or error message if invalid

### ✅ Validation Rules
- Check-out > Check-in
- Property must be available during selected dates
- Prevent double-booking

### ⚙️ Performance Criteria
- Booking creation response time < 1s
- Handle concurrent booking attempts (atomicity)

---

## ✅ General Notes
- All endpoints require authentication unless explicitly stated.
- API responses follow REST standards (status codes, JSON format).
- Logging and error handling should be implemented for all endpoints.

