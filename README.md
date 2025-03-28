# API Documentation

## 📌 Overview
This API allows users to register, login, retrieve their profile, and log out. It uses JWT authentication for secure access.

---

## 📍 User Registration (`/users/register`)

### 🔗 Description
This endpoint allows new users to create an account by providing their full name, email, and password. Upon successful registration, the user receives a JWT token for authentication.

### 🔗 Endpoint Details
- **Method:** `POST`
- **Authentication:** Not required

### 📥 Request Body
- **fullname** (object):  
  - **firstname** (string, required): User's first name (minimum 3 characters).  
  - **lastname** (string, optional): User's last name (minimum 3 characters if provided).  
- **email** (string, required): User’s email address (must be a valid email).  
- **password** (string, required): User’s password (minimum 6 characters).  

### 📤 Example Request
```json
{
  "fullname": { "firstname": "John", "lastname": "Doe" },
  "email": "john@example.com",
  "password": "securePassword123"
}
```

### 📤 Example Response
- **user** (object):  
  - **fullname** (object):  
    - **firstname** (string): User’s first name.  
    - **lastname** (string): User’s last name (if provided).  
  - **email** (string): User’s email address.  
- **token** (string): JWT Token.  

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

---

## 📍 User Login (`/users/login`)

### 🔗 Description
This endpoint allows registered users to log in by providing their email and password. If the credentials are correct, a JWT token is issued, which must be used for authentication in future requests.

### 🔗 Endpoint Details
- **Method:** `POST`
- **Authentication:** Not required

### 📥 Request Body
- **email** (string, required): User’s email address (must be a valid email).  
- **password** (string, required): User’s password (minimum 6 characters).  

### 📤 Example Request
```json
{
  "email": "john@example.com",
  "password": "securePassword123"
}
```

### 📤 Example Response
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

---

## 📍 Get User Profile (`/users/profile`)

### 🔗 Description
This endpoint allows authenticated users to retrieve their profile information. The request must include a valid JWT token.

### 🔗 Endpoint Details
- **Method:** `GET`
- **Authentication:** ✅ Required (JWT Token)

### 📥 Request Headers
```json
{
  "Authorization": "Bearer jwt_token_here"
}
```

### 📤 Example Response
```json
{
  "_id": "user_id_here",
  "fullname": { "firstname": "John", "lastname": "Doe" },
  "email": "john@example.com"
}
```

---

## 📍 User Logout (`/users/logout`)

### 🔗 Description
This endpoint allows authenticated users to log out. The system blacklists the token to prevent further use.

### 🔗 Endpoint Details
- **Method:** `GET`
- **Authentication:** ✅ Required (JWT Token)

### 📥 Request Headers
```json
{
  "Authorization": "Bearer jwt_token_here"
}
```

### 📤 Example Response
```json
{
  "message": "Logged out"
}
```

---

## 🛠️ Notes
- JWT tokens must be included in the `Authorization` header for protected endpoints.
- Passwords are securely hashed before storage.
- Tokens are blacklisted upon logout, ensuring security.

🚀 Try it Out:
- `/users/register` → Create a new user.
- `/users/login` → Authenticate and receive a token.
- `/users/profile` → Retrieve authenticated user details.
- `/users/logout` → Log out and invalidate the token.

