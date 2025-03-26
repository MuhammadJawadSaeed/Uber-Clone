# API Documentation: /users/register Endpoint

## 📌 Endpoint Overview

The `/users/register` endpoint allows users to **create an account** by providing their details such as name, email, and password.

## 🔗 Endpoint Details

- **URL:** `/users/register`
- **Method:** `POST`
- **Request Type:** `application/json`
- **Authentication:** Not required

## 📥 Request Body

The request body should be in JSON format and include the following fields:  

- **fullname** (object):  
  - **firstname** (string, required): User's first name (minimum 3 characters).  
  - **lastname** (string, optional): User's last name (minimum 3 characters if provided).  
- **email** (string, required): User’s email address (must be a valid email).  
- **password** (string, required): User’s password (minimum 6 characters).  

### **Example Request:**

```json
{
  "fullname": { "firstname": "John", "lastname": "Doe" },
  "email": "john@example.com",
  "password": "securePassword123"
}
```

## 📤 Response

### **Success (201 Created)**

```json
{
  "token": "jwt_token_here",
  "user": {
    "_id": "user_id_here",
    "fullname": { "firstname": "John", "lastname": "Doe" },
    "email": "john@example.com"
  }
}
```

### **Example Response:**

- **user** (object):  
  - **fullname** (object):  
    - **firstname** (string): User’s first name (minimum 3 characters).  
    - **lastname** (string): User’s last name (minimum 3 characters if provided).  
  - **email** (string): User’s email address (must be valid).  
  - **password** (string): User’s password (minimum 6 characters).  
- **token** (String): JWT Token  

```json
{
  "message": "User registered successfully",
  "user": {
    "_id": "65f9e5d2b8f8a2d1a3f9c7a4",
    "fullname": {
      "firstname": "Alice",
      "lastname": "Smith"
    },
    "email": "alice@example.com"
  },
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjY1ZjllNWQyYjhmOGEyZDFhM2Y5YzdhNCIsImlhdCI6MTY5MDU5MjA4OX0.7gJH3GltxL4P6tR6qEzFhE2N3zB9Wb_9P9F5x0s-4Q8"
}
```

### **Validation Errors (400 Bad Request)**

```json
{
  "errors": [
    {
      "msg": "First name must be 3 characters long",
      "param": "fullname.firstname"
    },
    { "msg": "Invalid Email", "param": "email" }
  ]
}
```

### **Server Error (500 Internal Server Error)**

Occurs when there is an issue with the database or backend logic.

```json
{
  "error": "Internal Server Error"
}
```

## 🛠️ Notes

- Ensure all required fields are provided.
- Email should be unique in the database.
- Password is hashed before saving.

## 🚀 Try it Out

Use **Postman** or **Thunder Client** in VS Code to send a `POST` request to `/users/register` with the above request body.
