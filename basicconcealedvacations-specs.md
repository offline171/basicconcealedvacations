# Basic Concealed Vacations

## 1. Overview

Basic Concealed Vacations is a vacation viewing website that allows users to browse through all the best vacation spots in the United States, bookmark their favorites, and save it for later. 

## 2. System Requirements

### 2.1 Functional Requirements

#### User Management
- User registration with email and password
- User login/logout functionality
- Password reset capability
- User profile management
- Session management and persistence

#### Vacation Management
- Allow contributers to add location to the website's database
- Let users view the entire database list
- Have each location have some (minimal) information about itself
- Bookmark locations
- Allow users to view all their bookmarked locations
- Likely mostly reuse the UI between the main location list and the bookmarked one

#### UI/UX Requirements
- Responsive design for mobile and desktop devices
- Intuitive, clean user interface
- Dark/light mode toggle

### 2.2 Non-Functional Requirements

#### Performance
- Page load time under 2 seconds
- Bookmarks should register within 1 second (no idea if databases are realistically this fast)

#### Security
- Secure password storage (hashed and salted)
- HTTPS for all communications
- Protection against common web vulnerabilities (XSS, CSRF, SQL injection)
- Rate limiting for login attempts

#### Scalability
- Support for at least 10,000 concurrent users
- Support for at least 100,000 bookmarks per user

#### Reliability
- 99.9% uptime
- Automated backups
- Error logging and monitoring

## 3. Technical Architecture

### 3.1 Frontend
- **Framework**: React.js
- **State Management**: Redux or Context API
- **UI Components**: Material-UI or Tailwind CSS
- **HTTP Client**: Axios
- **Form Handling**: Formik or React Hook Form

### 3.2 Backend
- **Framework**: Node.js with ExpressJS
- **Authentication**: JWT (JSON Web Tokens)
- **API Design**: RESTful API

### 3.3 Database
- **Primary Database**: MongoDB or PostgreSQL
- **Caching**: Redis for session management and frequently accessed data

### 3.4 Infrastructure
- **Hosting**: AWS, Google Cloud, or Azure
- **Deployment**: Docker containers with Kubernetes orchestration
- **CI/CD**: GitHub Actions or Jenkins
- **Monitoring**: Prometheus and Grafana

## 4. Data Models

### 4.1 User Model
```json
{
  "id": "UUID",
  "email": "string",
  "password": "string (hashed)",
  "firstName": "string",
  "lastname": "string",
  "createdAt": "timestamp",
  "updatedAt": "timestamp",
  "lastLogin": "timestamp",
  "preferences": {
    "theme": "string (light/dark)",
    "emailNotifications": "boolean"
  }
}
```

### 4.2 Location Model
```json
{
  "id": "UUID",
  "title": "string",
  "address": "string",
  "city": "string",
  "state": "string",
  "description": "string",
  "image": "PNG (or something similar idk)",
  "createdAt": "timestamp",
  "updatedAt": "timestamp"
}
```

### 4.3 Bookmark Model
```json
{
  "id": "UUID",
  "userId": "UUID (foreign key)",
  "locationId": "UUID (foreign key 2)",
  "createdAt": "timestamp",
  "updatedAt": "timestamp"
}
```

## 5. API Endpoints

### 5.1 Authentication Endpoints
- `POST /api/auth/register` - Create a new user account
- `POST /api/auth/login` - Authenticate user and generate token
- `POST /api/auth/logout` - Invalidate current token
- `POST /api/auth/reset-password` - Request password reset
- `POST /api/auth/reset-password/:token` - Reset password with token

### 5.2 User Endpoints
- `GET /api/users/me` - Get current user profile
- `PUT /api/users/me` - Update current user profile
- `PUT /api/users/me/preferences` - Update user preferences

### 5.3 Location Endpoints (only for contributers, not users)
- `GET /api/locations` - Get all locations
    - Check locations to see if they're bookmarked to be able to tell frontend to show certain locations as bookmarked
- `POST /api/locations` - Create a new location
- `GET /api/locations/:id` - Get a specific location
- `PUT /api/locations/:id` - Update a location
- `DELETE /api/locations/:id` - Delete a location

### 5.4 Bookmark Endpoints
- `GET /api/bookmarks` - Get all bookmarks for current user
- `POST /api/bookmarks` - Create a new bookmark
    - (give logic to bookmarks to always check to make sure that user hasn't bookmarked the same location twice. Might pre-check or check when trying to make it)
- `GET /api/bookmarks/:id` - Get a specific bookmark
- `PUT /api/bookmarks/:id` - Update a bookmark
- `DELETE /api/bookmarks/:id` - Delete a bookmark
