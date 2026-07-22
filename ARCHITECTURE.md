# Architecture Overview

## System Architecture

The project follows a three-tier architecture.

```
+----------------------+
|     Admin Panel      |
|      (Next.js)       |
+----------+-----------+
           |
           | REST API
           |
+----------v-----------+
|     Express.js API   |
| Authentication       |
| Page Management      |
| Business Logic       |
+----------+-----------+
           |
           | Mongoose
           |
+----------v-----------+
|      MongoDB         |
+----------------------+

           ^
           |
           | REST API
           |
+----------+-----------+
|    Public Website    |
|      (Next.js)       |
+----------------------+
```

---

# Components

## Admin Panel

The Admin Panel is responsible for:

- Administrator Login
- Administrator Logout
- Managing website pages
- Creating content
- Editing content
- Deleting content

The admin communicates with the backend through REST APIs using Axios.

Redux Toolkit manages the authentication and page state.

---

## Backend

The backend is built using Express.js.

Responsibilities include:

- JWT Authentication
- Authorization
- CRUD APIs
- Database communication
- Business logic
- Error handling

The backend exposes REST APIs consumed by both the Admin Panel and the Public Website.

---

## Database

MongoDB stores:

- Administrator information
- Website pages
- Page content

Mongoose is used as the ODM.

---

## Public Website

The public website never contains hardcoded content.

Every page fetches data from the backend APIs and renders it dynamically.

---

# Authentication Flow

1. Administrator enters credentials.
2. Backend validates credentials.
3. JWT token is generated.
4. Token is returned to the frontend.
5. Token is stored in localStorage.
6. Redux Toolkit maintains authentication state.
7. Protected API requests include the JWT token in the Authorization header.

---

# State Management

Redux Toolkit is used for:

- Authentication state
- Page state

Local component state is used for:

- Form inputs
- Loading indicators
- Temporary UI state

This keeps Redux focused on globally shared application state.

---

# API Design

Authentication

- POST /api/admin/login
- GET /api/admin/profile

Pages

- GET /api/pages
- GET /api/pages/:slug
- POST /api/pages
- PUT /api/pages/:id
- DELETE /api/pages/:id

---

# Folder Structure

```
renewcred-cms/
│
├── admin/
│
├── backend/
│   ├── controllers/
│   ├── middleware/
│   ├── models/
│   ├── routes/
│   └── server.js
│
├── website/
│
├── README.md
└── ARCHITECTURE.md
```

---

# Design Decisions

## Express.js

Express.js was selected because it provides a lightweight and scalable backend suitable for REST APIs.

## MongoDB

MongoDB was chosen because page content is naturally document-oriented and can evolve without frequent schema changes.

## Redux Toolkit

Redux Toolkit manages global application state such as authentication and page data while leaving local UI state inside React components.

## JWT Authentication

JWT provides a stateless authentication mechanism that is easy to integrate with REST APIs.

---

# Future Improvements

- Rich text editor
- Image uploads
- Content versioning
- Draft & Publish workflow
- Role-based access control
- Docker deployment
- Automated testing