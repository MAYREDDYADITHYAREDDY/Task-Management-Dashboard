# Scalable REST API with Authentication & Role-Based Access

A complete full-stack application featuring a secure, scalable backend REST API with JWT authentication, role-based access control, and a modern React frontend for task management.

---
## Project Drive Link

Download the project Through The Below link:
(https://drive.google.com/file/d/1D9Vg85T50awazdFUpbqvuOuR0lpPNplp/view?usp=drive_link)**
Refer SETUP.md File for Installation Process.

---
## 🎯 Table of Contents

- [Features](#-features)
- [Quick Start](#-quick-start)
- [Project Structure](#-project-structure)
- [API Documentation](#-api-documentation)
- [Authentication & Security](#-authentication--security)
- [Database Schema](#-database-schema)
- [Technology Stack](#-technology-stack)
- [Development Guide](#-development-guide)
- [Deployment](#-deployment)
- [Scaling for Production](#-scaling-for-production)
- [Architecture](#-architecture)
- [Troubleshooting](#-troubleshooting)
- [Testing](#-testing)

---

## 🚀 Features

### Backend
- ✅ User authentication (Register/Login) with JWT tokens
- ✅ Password hashing using bcrypt
- ✅ Role-based access control (User/Admin)
- ✅ Complete CRUD operations for task management
- ✅ API versioning (v1)
- ✅ Input validation and sanitization
- ✅ Error handling middleware
- ✅ Rate limiting (100 requests/15 minutes)
- ✅ API documentation with Swagger
- ✅ SQLite database with Sequelize ORM (easily switchable to PostgreSQL)
- ✅ Security headers with Helmet
- ✅ CORS configuration

### Frontend
- ✅ React.js SPA with React Router
- ✅ User registration and login
- ✅ Protected routes with JWT
- ✅ Task management dashboard
- ✅ CRUD operations for tasks
- ✅ Filtering and search functionality
- ✅ Real-time statistics
- ✅ Responsive design
- ✅ Toast notifications

---

## 🚀 Quick Start

### Prerequisites
- Node.js (v16 or higher)
- npm or yarn

### Option 1: Manual Setup (Recommended)

**Step 1: Install Backend Dependencies**
```powershell
cd backend
npm install
```

**Step 2: Configure Backend**
The backend is already configured to use SQLite (no database setup needed!). The `.env` file is pre-configured.

**Step 3: Install Frontend Dependencies**
```powershell
cd frontend
npm install
```

**Step 4: Start Backend Server**
```powershell
cd backend
npm run dev
```
Backend will run on http://localhost:5000

**Step 5: Start Frontend (in new terminal)**
```powershell
cd frontend
npm start
```
Frontend will run on http://localhost:3000

### Option 2: Docker Setup

```powershell
docker-compose up -d
```

### 🎉 Access Points

| Service | URL | Purpose |
|---------|-----|---------|
| **Frontend** | http://localhost:3000 | Web application |
| **Backend API** | http://localhost:5000 | REST API |
| **API Docs** | http://localhost:5000/api-docs | Swagger UI |
| **Health Check** | http://localhost:5000/health | Server status |

---

## 📁 Project Structure

```
Adithya_AI/
├── backend/                    # Node.js/Express Backend
│   ├── src/
│   │   ├── config/            # Database & Swagger config
│   │   │   ├── database.js    # Sequelize configuration
│   │   │   └── swagger.js     # API documentation setup
│   │   ├── controllers/       # Business logic
│   │   │   ├── authController.js   # Authentication logic
│   │   │   └── taskController.js   # Task CRUD logic
│   │   ├── middleware/        # Auth, validation, error handling
│   │   │   ├── auth.js        # JWT verification
│   │   │   ├── errorHandler.js
│   │   │   └── validate.js    # Input validation
│   │   ├── models/            # Database models
│   │   │   ├── User.js        # User schema
│   │   │   ├── Task.js        # Task schema
│   │   │   └── index.js       # Model associations
│   │   ├── routes/            # API route definitions
│   │   │   ├── authRoutes.js
│   │   │   └── taskRoutes.js
│   │   └── server.js          # Application entry point
│   ├── .env                   # Environment variables (pre-configured)
│   ├── database.sqlite        # SQLite database (auto-created)
│   ├── Dockerfile             # Backend Docker config
│   └── package.json           # Dependencies
│
├── frontend/                   # React Frontend
│   ├── public/                # Static files
│   ├── src/
│   │   ├── components/        # Reusable components
│   │   │   └── PrivateRoute.js
│   │   ├── context/           # State management
│   │   │   └── AuthContext.js # Authentication context
│   │   ├── pages/             # Page components
│   │   │   ├── Login.js
│   │   │   ├── Register.js
│   │   │   ├── Dashboard.js
│   │   │   ├── Auth.css
│   │   │   └── Dashboard.css
│   │   ├── services/          # API integration
│   │   │   └── api.js         # Axios API client
│   │   ├── App.js             # Main component
│   │   ├── App.css
│   │   └── index.js           # Entry point
│   ├── .env                   # Frontend config
│   ├── Dockerfile             # Frontend Docker config
│   ├── nginx.conf             # Nginx configuration
│   └── package.json           # Dependencies (with proxy config)
│
├── docker-compose.yml         # Multi-container setup
├── Postman_Collection.json    # API testing collection
└── README.md                  # This file
```

---

## 📚 API Documentation

### Authentication Endpoints

#### Register New User
```http
POST /api/v1/auth/register
Content-Type: application/json

{
  "username": "testuser",
  "email": "test@example.com",
  "password": "Test123456",
  "role": "user"  // optional: "user" or "admin"
}

Response: 201 Created
{
  "success": true,
  "data": {
    "user": {
      "id": "uuid",
      "username": "testuser",
      "email": "test@example.com",
      "role": "user"
    },
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
  }
}
```

#### Login User
```http
POST /api/v1/auth/login
Content-Type: application/json

{
  "email": "test@example.com",
  "password": "Test123456"
}

Response: 200 OK
{
  "success": true,
  "data": {
    "user": { ... },
    "token": "..."
  }
}
```

#### Get Current User (Protected)
```http
GET /api/v1/auth/me
Authorization: Bearer <your_jwt_token>

Response: 200 OK
{
  "success": true,
  "data": {
    "id": "uuid",
    "username": "testuser",
    "email": "test@example.com",
    "role": "user"
  }
}
```

#### Update Profile (Protected)
```http
PUT /api/v1/auth/profile
Authorization: Bearer <your_jwt_token>
Content-Type: application/json

{
  "username": "newusername",
  "email": "newemail@example.com"
}
```

### Task Endpoints (All Protected)

#### Get All Tasks
```http
GET /api/v1/tasks?status=pending&priority=high&search=keyword&page=1&limit=10
Authorization: Bearer <your_jwt_token>

Response: 200 OK
{
  "success": true,
  "count": 5,
  "total": 25,
  "totalPages": 3,
  "currentPage": 1,
  "data": [
    {
      "id": "uuid",
      "title": "Complete project",
      "description": "Finish the REST API",
      "status": "in-progress",
      "priority": "high",
      "dueDate": "2025-11-30",
      "createdAt": "2025-11-27T10:00:00Z",
      "updatedAt": "2025-11-27T10:00:00Z"
    }
  ]
}
```

#### Get Single Task
```http
GET /api/v1/tasks/:id
Authorization: Bearer <your_jwt_token>
```

#### Create Task
```http
POST /api/v1/tasks
Authorization: Bearer <your_jwt_token>
Content-Type: application/json

{
  "title": "New Task",
  "description": "Task description",
  "priority": "high",  // low, medium, high, urgent
  "status": "pending", // pending, in-progress, completed, cancelled
  "dueDate": "2025-12-01"
}

Response: 201 Created
```

#### Update Task
```http
PUT /api/v1/tasks/:id
Authorization: Bearer <your_jwt_token>
Content-Type: application/json

{
  "title": "Updated Task",
  "status": "completed"
}

Response: 200 OK
```

#### Delete Task
```http
DELETE /api/v1/tasks/:id
Authorization: Bearer <your_jwt_token>

Response: 200 OK
{
  "success": true,
  "message": "Task deleted successfully"
}
```

#### Get Task Statistics
```http
GET /api/v1/tasks/stats
Authorization: Bearer <your_jwt_token>

Response: 200 OK
{
  "success": true,
  "data": {
    "total": 25,
    "pending": 5,
    "inProgress": 10,
    "completed": 8,
    "cancelled": 2
  }
}
```

### Query Parameters for Task Listing

| Parameter | Type | Description | Example |
|-----------|------|-------------|---------|
| status | string | Filter by status | `?status=pending` |
| priority | string | Filter by priority | `?priority=high` |
| search | string | Search in title/description | `?search=project` |
| page | number | Page number | `?page=1` |
| limit | number | Items per page | `?limit=10` |

### Interactive API Documentation

Access Swagger UI at http://localhost:5000/api-docs for:
- Interactive API testing
- Request/response examples
- Schema definitions
- Try-it-out functionality

---

## 🔐 Authentication & Security

### Password Requirements
- Minimum 6 characters
- Must contain uppercase letter
- Must contain lowercase letter
- Must contain number

### Username Requirements
- 3-50 characters
- Alphanumeric only

### Security Features

1. **Password Hashing**: Bcrypt with 10 salt rounds
2. **JWT Authentication**: Secure token-based auth (7-day expiration)
3. **Input Validation**: Express-validator for all inputs
4. **Rate Limiting**: 100 requests per 15 minutes per IP
5. **Helmet.js**: Security headers (CSP disabled in dev mode)
6. **CORS**: Configured cross-origin requests
7. **SQL Injection Prevention**: Sequelize ORM with parameterized queries
8. **XSS Protection**: Input sanitization

### JWT Token Flow

```
1. User registers/logs in
   ↓
2. Server generates JWT token
   ↓
3. Client stores token in localStorage
   ↓
4. Client includes token in Authorization header
   ↓
5. Server verifies token on each protected request
   ↓
6. Server extracts user info from token
   ↓
7. Request proceeds with authenticated user context
```

---

## 📊 Database Schema

### Users Table
```javascript
{
  id: UUID (Primary Key),
  username: STRING(50) UNIQUE,
  email: STRING(100) UNIQUE,
  password: STRING(255),  // Hashed with bcrypt
  role: ENUM('user', 'admin'),
  isActive: BOOLEAN,
  lastLogin: DATE,
  createdAt: TIMESTAMP,
  updatedAt: TIMESTAMP
}

Indexes:
- email (unique)
- username (unique)
```

### Tasks Table
```javascript
{
  id: UUID (Primary Key),
  title: STRING(200),
  description: TEXT,
  status: ENUM('pending', 'in-progress', 'completed', 'cancelled'),
  priority: ENUM('low', 'medium', 'high', 'urgent'),
  dueDate: DATE,
  userId: UUID (Foreign Key → users.id),
  createdAt: TIMESTAMP,
  updatedAt: TIMESTAMP
}

Indexes:
- userId (for efficient user task lookup)
- status (for filtering)
- priority (for filtering)

Relationship:
- One User has Many Tasks (One-to-Many)
- Tasks belong to User (Foreign Key: userId)
```

---

## 🎨 Technology Stack

### Backend
- **Runtime**: Node.js 18+
- **Framework**: Express.js 4.18
- **Database**: SQLite (with Sequelize ORM)
- **Authentication**: JWT (jsonwebtoken) + Bcrypt
- **Validation**: Express-validator
- **API Docs**: Swagger UI Express
- **Security**: Helmet, CORS, express-rate-limit
- **Dev Tools**: Nodemon

### Frontend
- **Library**: React 18.2
- **Routing**: React Router v6.20
- **HTTP Client**: Axios 1.6
- **Notifications**: React Toastify 9.1
- **Styling**: CSS3 (Flexbox/Grid)
- **Build Tool**: React Scripts 5.0

### DevOps
- **Containerization**: Docker
- **Orchestration**: Docker Compose
- **Web Server**: Nginx (production)

---

## 💻 Development Guide

### Environment Variables

**Backend (.env)**
```env
# Server Configuration
PORT=5000
NODE_ENV=development

# Database Configuration (SQLite)
DB_DIALECT=sqlite
DB_STORAGE=database.sqlite

# JWT Configuration
JWT_SECRET=your_super_secret_jwt_key_change_this_in_production
JWT_EXPIRE=7d

# API Configuration
API_VERSION=v1

# CORS Configuration
CORS_ORIGIN=http://localhost:3000

# Rate Limiting
RATE_LIMIT_WINDOW_MS=900000
RATE_LIMIT_MAX_REQUESTS=100
```

**Frontend (.env)**
```env
PORT=3000
```

### Adding New Features

#### 1. Adding a New API Endpoint

**Step 1**: Create model (if needed)
```javascript
// backend/src/models/Comment.js
module.exports = (sequelize, DataTypes) => {
  const Comment = sequelize.define('Comment', {
    id: {
      type: DataTypes.UUID,
      defaultValue: DataTypes.UUIDV4,
      primaryKey: true
    },
    content: {
      type: DataTypes.TEXT,
      allowNull: false
    },
    taskId: {
      type: DataTypes.UUID,
      allowNull: false
    },
    userId: {
      type: DataTypes.UUID,
      allowNull: false
    }
  });
  return Comment;
};
```

**Step 2**: Create controller
```javascript
// backend/src/controllers/commentController.js
exports.createComment = async (req, res, next) => {
  try {
    const comment = await Comment.create({
      content: req.body.content,
      taskId: req.params.taskId,
      userId: req.user.id
    });
    res.status(201).json({ success: true, data: comment });
  } catch (error) {
    next(error);
  }
};
```

**Step 3**: Create routes
```javascript
// backend/src/routes/commentRoutes.js
const express = require('express');
const router = express.Router();
const { protect } = require('../middleware/auth');
const { createComment } = require('../controllers/commentController');

router.post('/tasks/:taskId/comments', protect, createComment);

module.exports = router;
```

**Step 4**: Register routes in server.js
```javascript
const commentRoutes = require('./routes/commentRoutes');
app.use(`/api/${API_VERSION}`, commentRoutes);
```

#### 2. Adding Frontend Feature

**Step 1**: Update API service
```javascript
// frontend/src/services/api.js
export const commentAPI = {
  create: (taskId, content) => api.post(`/tasks/${taskId}/comments`, { content }),
  getAll: (taskId) => api.get(`/tasks/${taskId}/comments`)
};
```

**Step 2**: Create component
```jsx
// frontend/src/components/CommentList.js
import { useState, useEffect } from 'react';
import { commentAPI } from '../services/api';

export default function CommentList({ taskId }) {
  const [comments, setComments] = useState([]);

  useEffect(() => {
    loadComments();
  }, [taskId]);

  const loadComments = async () => {
    const response = await commentAPI.getAll(taskId);
    setComments(response.data.data);
  };

  return (
    <div>
      {comments.map(comment => (
        <div key={comment.id}>{comment.content}</div>
      ))}
    </div>
  );
}
```

### Code Style Guidelines

- Use ES6+ features (arrow functions, destructuring, async/await)
- Use meaningful variable and function names
- Add JSDoc comments for complex functions
- Use async/await instead of promises
- Handle errors with try-catch blocks
- Use environment variables for configuration
- Keep functions small and focused (single responsibility)
- Validate all user inputs
- Use proper HTTP status codes

---

## 🐳 Deployment

### Docker Deployment

**Build and run all services:**
```powershell
docker-compose up -d
```

**View logs:**
```powershell
docker-compose logs -f
```

**Stop services:**
```powershell
docker-compose down
```

**Rebuild after code changes:**
```powershell
docker-compose up -d --build
```

### Production Checklist

- [ ] Update JWT_SECRET to a strong random string
- [ ] Switch to PostgreSQL for production (update .env)
- [ ] Enable HTTPS/SSL certificates
- [ ] Set NODE_ENV=production
- [ ] Enable production logging
- [ ] Set up database backups
- [ ] Configure environment-specific CORS origins
- [ ] Set up monitoring (health checks, logs)
- [ ] Enable rate limiting (adjust limits for production)
- [ ] Review and update security headers
- [ ] Set up CI/CD pipeline
- [ ] Configure CDN for static assets
- [ ] Set up error tracking (Sentry, Rollbar)

### Cloud Deployment Options

#### AWS
- **Frontend**: S3 + CloudFront
- **Backend**: EC2 / ECS / Elastic Beanstalk
- **Database**: RDS (PostgreSQL)
- **Load Balancer**: Application Load Balancer

#### Azure
- **Frontend**: Azure Static Web Apps
- **Backend**: App Service / Container Instances
- **Database**: Azure Database for PostgreSQL

#### Heroku (Quick Deploy)
```bash
# Backend
cd backend
heroku create your-api-name
git push heroku main

# Frontend
cd frontend
npm run build
# Deploy build folder to Netlify/Vercel
```

---

## 📈 Scaling for Production

### Current Architecture (Single Server)
```
User → Frontend (Port 3000)
         ↓
    Backend API (Port 5000)
         ↓
    SQLite Database
```

### Scaling Path

#### Stage 1: Load Balancer + Multiple API Servers
```
Users
  ↓
Load Balancer (Nginx/AWS ELB)
  ↓
┌─────┬─────┬─────┐
│ API │ API │ API │ (3+ instances)
│  1  │  2  │  3  │
└─────┴─────┴─────┘
  ↓
PostgreSQL (Master)
  ↓
Read Replicas
```

#### Stage 2: Add Caching Layer
```
API Servers
  ↓
Redis Cache (Session, frequent queries)
  ↓
Database
```

#### Stage 3: Microservices
```
API Gateway
  ↓
┌──────────┬──────────┬───────────┐
│  User    │  Task    │  Notif    │
│ Service  │ Service  │  Service  │
└──────────┴──────────┴───────────┘
  ↓
Message Queue (RabbitMQ/Redis)
  ↓
Databases (one per service)
```

### Performance Optimization

#### 1. Database Optimization
```javascript
// Add indexes
Task.init({...}, {
  indexes: [
    { fields: ['userId'] },
    { fields: ['status'] },
    { fields: ['priority'] },
    { fields: ['createdAt'] }
  ]
});

// Use connection pooling (already configured)
const sequelize = new Sequelize({
  pool: {
    max: 10,
    min: 0,
    acquire: 30000,
    idle: 10000
  }
});
```

#### 2. Caching Implementation
```javascript
const redis = require('redis');
const client = redis.createClient();

// Cache user data
app.get('/api/v1/users/:id', async (req, res) => {
  const cached = await client.get(`user:${req.params.id}`);
  if (cached) return res.json(JSON.parse(cached));
  
  const user = await User.findByPk(req.params.id);
  await client.setEx(`user:${req.params.id}`, 3600, JSON.stringify(user));
  res.json(user);
});
```

#### 3. Load Balancing (Nginx)
```nginx
upstream backend {
    server api1.example.com:5000;
    server api2.example.com:5000;
    server api3.example.com:5000;
}

server {
    listen 80;
    location /api {
        proxy_pass http://backend;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

#### 4. Horizontal Scaling with Kubernetes
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: api-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: api
  template:
    metadata:
      labels:
        app: api
    spec:
      containers:
      - name: api
        image: your-api:latest
        ports:
        - containerPort: 5000
        env:
        - name: NODE_ENV
          value: "production"
```

### Monitoring & Observability

#### Health Check Endpoint
```javascript
// Already implemented
app.get('/health', (req, res) => {
  res.status(200).json({
    status: 'UP',
    timestamp: new Date(),
    uptime: process.uptime()
  });
});
```

#### Prometheus Metrics
```javascript
const prometheus = require('prom-client');
const httpRequestDuration = new prometheus.Histogram({
  name: 'http_request_duration_seconds',
  help: 'Duration of HTTP requests in seconds',
  labelNames: ['method', 'route', 'status_code']
});

// Middleware to track metrics
app.use((req, res, next) => {
  const start = Date.now();
  res.on('finish', () => {
    const duration = (Date.now() - start) / 1000;
    httpRequestDuration.labels(req.method, req.route.path, res.statusCode).observe(duration);
  });
  next();
});
```

---

## 🏗️ Architecture

### High-Level Architecture
```
┌─────────────────────────────────────────────────────────────────┐
│                         CLIENT LAYER                            │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  React Frontend (Port 3000)                              │   │
│  │  - Authentication UI                                     │   │
│  │  - Task Management Dashboard                             │   │
│  │  - Responsive Design                                     │   │
│  └──────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
                              │
                              │ HTTP/HTTPS
                              │ (JWT Token in Header)
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                      APPLICATION LAYER                          │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  Express.js Backend (Port 5000)                          │   │
│  │                                                          │   │
│  │  Middleware Stack:                                      │   │
│  │  • CORS                                                 │   │
│  │  • Helmet (Security Headers)                            │   │
│  │  • Rate Limiting                                        │   │
│  │  • JWT Authentication                                   │   │
│  │  • Input Validation                                     │   │
│  │  • Error Handler                                        │   │
│  │                                                          │   │
│  │  API Routes (Versioned: v1)                             │   │
│  │  • /api/v1/auth/* (Register, Login, Profile)           │   │
│  │  • /api/v1/tasks/* (CRUD, Stats, Filtering)            │   │
│  │                                                          │   │
│  │  Controllers → Business Logic                           │   │
│  │  Models → Database Entities                             │   │
│  └──────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
                              │
                              │ SQL Queries
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                       DATABASE LAYER                            │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  SQLite Database                                         │   │
│  │  ┌────────────────┐    ┌──────────────────────┐         │   │
│  │  │ users table    │    │ tasks table          │         │   │
│  │  │ • id (PK)      │───▶│ • userId (FK)        │         │   │
│  │  │ • username     │    │ • title, description │         │   │
│  │  │ • email        │    │ • status, priority   │         │   │
│  │  │ • password     │    │ • dueDate            │         │   │
│  │  │ • role         │    │                      │         │   │
│  │  └────────────────┘    └──────────────────────┘         │   │
│  │          One-to-Many Relationship                        │   │
│  └──────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
```

### Request Flow
```
1. User action in UI (e.g., Create Task)
   ↓
2. React sends API request (Axios)
   ↓
3. Express receives request
   ↓
4. Middleware chain:
   - CORS check
   - Rate limiting
   - JWT verification
   - Input validation
   ↓
5. Controller processes business logic
   ↓
6. Model interacts with database
   ↓
7. Response formatted and sent
   ↓
8. React updates UI
```

---

## 🐛 Troubleshooting

### Common Issues

#### Backend Won't Start

**Error: Port 5000 already in use**
```powershell
# Find process using port 5000
netstat -ano | findstr :5000

# Kill the process
taskkill /PID <PID> /F

# Or change port in .env
PORT=5001
```

**Error: Database connection failed**
- SQLite database is auto-created
- Check file permissions in project directory
- Ensure `database.sqlite` file can be created

#### Frontend Issues

**Error: Cannot connect to backend**
- Verify backend is running on port 5000
- Check `proxy` field in `frontend/package.json`: `"proxy": "http://localhost:5000"`
- Restart frontend after adding proxy: `npm start`

**Error: CORS policy blocked**
- Verify `CORS_ORIGIN` in backend `.env` is set to `http://localhost:3000`
- Restart backend after changing .env

**Error: npm install fails**
```powershell
# Clear npm cache
npm cache clean --force

# Delete node_modules and package-lock.json
Remove-Item -Recurse -Force node_modules
Remove-Item package-lock.json

# Reinstall
npm install
```

#### Authentication Issues

**Error: Token expired**
- JWT tokens expire after 7 days
- User needs to login again
- Token is automatically removed from localStorage

**Error: Invalid token**
- Ensure JWT_SECRET is same across server restarts
- Don't change JWT_SECRET in production (users will be logged out)
- Check token format: `Bearer <token>`

#### Database Issues

**Error: Validation error**
- Check password meets requirements (6+ chars, uppercase, lowercase, number)
- Ensure username is alphanumeric
- Verify email format is valid

**Error: Unique constraint violation**
- Username or email already exists
- Try different credentials

### Debug Mode

**Enable verbose logging:**

Backend:
```javascript
// In server.js
app.use((req, res, next) => {
  console.log(`${req.method} ${req.path}`, req.body);
  next();
});
```

Frontend:
```javascript
// In api.js
api.interceptors.request.use(config => {
  console.log('API Request:', config);
  return config;
});
```

---

## 🧪 Testing

### Testing the Application

#### 1. Using the Frontend UI

1. Open http://localhost:3000
2. Click "Register here"
3. Create account:
   - Username: `testuser`
   - Email: `test@example.com`
   - Password: `Test1234` (meets requirements)
4. Login with credentials
5. Create a task:
   - Title: "Complete project"
   - Description: "Finish REST API"
   - Priority: High
   - Status: In Progress
6. Test filtering by status/priority
7. Edit task and mark as completed
8. Delete task

#### 2. Using Swagger UI

1. Navigate to http://localhost:5000/api-docs
2. Test `/api/v1/auth/register`:
   - Click "Try it out"
   - Edit request body
   - Click "Execute"
   - Copy the JWT token from response
3. Authorize:
   - Click "Authorize" button (top right)
   - Enter: `Bearer <paste_token_here>`
   - Click "Authorize"
4. Test all endpoints with different scenarios

#### 3. Using cURL (PowerShell)

**Register:**
```powershell
$body = @{
    username = "testuser"
    email = "test@example.com"
    password = "Test123456"
} | ConvertTo-Json

$response = Invoke-RestMethod -Uri "http://localhost:5000/api/v1/auth/register" `
    -Method POST `
    -Body $body `
    -ContentType "application/json"

$token = $response.data.token
```

**Create Task:**
```powershell
$headers = @{ Authorization = "Bearer $token" }
$body = @{
    title = "Test Task"
    description = "Testing API"
    priority = "high"
    status = "pending"
} | ConvertTo-Json

Invoke-RestMethod -Uri "http://localhost:5000/api/v1/tasks" `
    -Method POST `
    -Headers $headers `
    -Body $body `
    -ContentType "application/json"
```

**Get All Tasks:**
```powershell
Invoke-RestMethod -Uri "http://localhost:5000/api/v1/tasks" `
    -Method GET `
    -Headers $headers
```

#### 4. Using Postman

1. Import `Postman_Collection.json`
2. Create environment variable:
   - Key: `token`
   - Value: (leave empty, will be set automatically)
3. Run "Register" request
4. Run "Login" request (token will be saved automatically)
5. Test all other endpoints

### Test Scenarios

#### Happy Path
- ✅ Register new user
- ✅ Login successfully
- ✅ Create task
- ✅ Get all tasks
- ✅ Update task
- ✅ Delete task
- ✅ Get statistics

#### Error Scenarios
- ❌ Register with existing email (should fail)
- ❌ Login with wrong password (should fail)
- ❌ Create task without token (should fail)
- ❌ Access task of another user (should fail)
- ❌ Invalid input validation (should fail)

#### Edge Cases
- Test with very long task titles
- Test with special characters
- Test pagination with many tasks
- Test filtering with no results
- Test with expired tokens

---

## 📝 API Response Format

All API responses follow this structure:

**Success Response:**
```json
{
  "success": true,
  "data": { ... },
  "count": 10,      // For list endpoints
  "total": 100,     // For paginated endpoints
  "totalPages": 10, // For paginated endpoints
  "currentPage": 1  // For paginated endpoints
}
```

**Error Response:**
```json
{
  "success": false,
  "message": "Error message",
  "errors": [        // Validation errors (optional)
    {
      "field": "email",
      "message": "Invalid email format"
    }
  ]
}
```

---

## 🎓 Learning Resources

### Documentation Included
- Complete API documentation (Swagger)
- Code comments and JSDoc
- Environment configuration examples
- Docker deployment guide

### Technologies Used
- [Express.js Documentation](https://expressjs.com/)
- [React Documentation](https://react.dev/)
- [Sequelize ORM](https://sequelize.org/)
- [JWT Authentication](https://jwt.io/)
- [Docker Documentation](https://docs.docker.com/)

---

## 🚀 Next Steps

### Phase 1: Enhancements
- [ ] Email verification for new users
- [ ] Password reset functionality
- [ ] User profile pictures
- [ ] Task comments
- [ ] Task attachments
- [ ] Task assignments to multiple users
- [ ] Task labels/tags

### Phase 2: Advanced Features
- [ ] Real-time updates (WebSocket/Socket.io)
- [ ] Push notifications
- [ ] Email notifications
- [ ] Task reminders
- [ ] Recurring tasks
- [ ] Export tasks (CSV/PDF)
- [ ] Dark mode
- [ ] Mobile app (React Native)

### Phase 3: Production
- [ ] Switch to PostgreSQL
- [ ] Implement Redis caching
- [ ] Set up CI/CD pipeline (GitHub Actions)
- [ ] Deploy to cloud (AWS/Azure/GCP)
- [ ] Set up monitoring (Prometheus/Grafana)
- [ ] Implement logging (Winston/ELK)
- [ ] Add automated tests (Jest/Mocha)
- [ ] Performance optimization
- [ ] Security audit
- [ ] Load testing

---

## ✅ Feature Checklist

### Backend ✅
- [x] User registration with validation
- [x] User login with JWT
- [x] Password hashing with bcrypt
- [x] Role-based access control
- [x] Protected routes middleware
- [x] Task CRUD operations
- [x] Task filtering (status, priority)
- [x] Task search
- [x] Task pagination
- [x] Task statistics
- [x] Input validation
- [x] Error handling
- [x] Rate limiting
- [x] API versioning
- [x] Swagger documentation
- [x] Health check endpoint
- [x] CORS configuration
- [x] Security headers

### Frontend ✅
- [x] Registration page
- [x] Login page
- [x] Dashboard layout
- [x] Task list view
- [x] Create task modal
- [x] Edit task functionality
- [x] Delete task functionality
- [x] Task filtering UI
- [x] Search functionality
- [x] Statistics cards
- [x] Protected routes
- [x] Auth context
- [x] Toast notifications
- [x] Responsive design
- [x] Form validation
- [x] Error handling

### DevOps ✅
- [x] Docker configuration
- [x] Docker Compose setup
- [x] Environment variables
- [x] Production-ready structure
- [x] Health checks
- [x] Logging setup

---

## 📞 Support & Contribution

### Getting Help
1. Check this README for comprehensive documentation
2. Review Swagger documentation at http://localhost:5000/api-docs
3. Check troubleshooting section above
4. Review code comments in the source files

### Contributing
1. Fork the repository
2. Create feature branch: `git checkout -b feature/AmazingFeature`
3. Commit changes: `git commit -m 'Add AmazingFeature'`
4. Push to branch: `git push origin feature/AmazingFeature`
5. Open a Pull Request

---

## 📄 License

MIT License - feel free to use this project for learning or production purposes.

---

## 👤 Author

**Adithya**

Built with ❤️ using Node.js, Express, React, and SQLite.

---

## 🎉 Congratulations!

You now have a **production-ready**, **scalable** REST API with:
- ✅ Complete authentication system
- ✅ Role-based authorization
- ✅ Full CRUD operations
- ✅ Modern React frontend
- ✅ Comprehensive documentation
- ✅ Docker deployment
- ✅ Security best practices
- ✅ Scalability roadmap

**Ready to deploy and scale!** 🚀

---

*Last Updated: November 29, 2025*

