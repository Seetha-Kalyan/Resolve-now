# ResolveNow — Online Complaint Registration and Management System

## 📋 Table of Contents
1. [Project Overview](#project-overview)
2. [Features](#features)
3. [Tech Stack](#tech-stack)
4. [Project Structure](#project-structure)
5. [Prerequisites](#prerequisites)
6. [Installation & Setup](#installation--setup)
7. [Configuration](#configuration)
8. [API Documentation](#api-documentation)
9. [Database Models](#database-models)
10. [Frontend Components](#frontend-components)
11. [Authentication & Authorization](#authentication--authorization)
12. [Real-time Features](#real-time-features)
13. [Development Guide](#development-guide)
14. [Deployment Notes](#deployment-notes)

---

## Project Overview

**ResolveNow** is a full-stack web application designed to streamline complaint registration, tracking, and management. It enables users to submit complaints, track their status in real-time, and communicate with support agents through an integrated messaging system.

The application follows a modern full-stack architecture with:
- **Backend**: Express.js server with MongoDB database
- **Frontend**: React application with Vite bundler
- **Real-time Communication**: Socket.io for live chat and notifications

### Key Purpose
- Allow users to register and submit complaints
- Provide complaint tracking and status updates
- Enable real-time communication between users and support agents
- Manage complaint lifecycle from submission to resolution

---

## Features

### User Features
- ✅ **User Registration & Login** - Secure authentication with JWT tokens
- ✅ **Submit Complaints** - Create new complaints with title, description, and images
- ✅ **Track Complaints** - View personal complaint history and current status
- ✅ **Real-time Chat** - Live messaging with assigned support agents
- ✅ **Status Tracking** - Monitor complaint progress through different states

### Agent Features
- ✅ **View All Complaints** - Dashboard to see all submitted complaints
- ✅ **Assign Complaints** - Assign complaints to themselves or other agents
- ✅ **Update Status** - Change complaint status (open → in_progress → resolved → closed)
- ✅ **Communicate** - Real-time chat with users regarding their complaints

### Admin Features
- ✅ **System Management** - Manage users and complaints system-wide
- ✅ **Role Management** - Assign roles to users (user, agent, admin)

---

## Tech Stack

### Backend
| Technology | Version | Purpose |
|-----------|---------|---------|
| **Express.js** | 4.18.2 | Web framework |
| **Node.js** | 18+ | Runtime environment |
| **MongoDB** | Latest | Database |
| **Mongoose** | 7.0.0 | ODM for MongoDB |
| **Socket.io** | 4.7.0 | Real-time communication |
| **JWT (jsonwebtoken)** | 9.0.0 | Authentication tokens |
| **bcryptjs** | 2.4.3 | Password hashing |
| **CORS** | 2.8.5 | Cross-origin requests |
| **Multer** | 1.4.5 | File upload handling |
| **Dotenv** | 16.0.0 | Environment variables |
| **Nodemon** | 2.0.22 | Development auto-reload |

### Frontend
| Technology | Version | Purpose |
|-----------|---------|---------|
| **React** | 18.2.0 | UI library |
| **Vite** | 5.0.0 | Build tool & dev server |
| **React Router** | 6.14.1 | Client-side routing |
| **Axios** | 1.13.5 | HTTP client |
| **Socket.io Client** | 4.7.0 | Real-time communication |
| **Bootstrap** | 5.3.0 | CSS framework |

---

## Project Structure

```
apsche project/
├── README.md
├── DOCUMENTATION.md
│
├── backend/                    # Express.js server
│   ├── server.js              # Main server file
│   ├── package.json           # Dependencies
│   ├── config/
│   │   └── db.js              # MongoDB connection
│   ├── models/                # Database schemas
│   │   ├── User.js            # User model
│   │   └── Complaint.js       # Complaint model with messages
│   ├── controllers/           # Business logic
│   │   ├── authController.js  # Auth endpoints
│   │   └── complaintController.js  # Complaint endpoints
│   ├── middleware/
│   │   └── auth.js            # JWT verification middleware
│   └── routes/                # API endpoints
│       ├── auth.js            # Auth routes
│       └── complaints.js      # Complaint routes
│
└── frontend/                  # React application
    ├── index.html             # HTML entry point
    ├── package.json           # Dependencies
    ├── src/
    │   ├── main.jsx           # React DOM render
    │   ├── App.jsx            # Main app component
    │   ├── api.js             # Axios API client
    │   ├── styles.css         # Global styles
    │   └── pages/             # Page components
    │       ├── Login.jsx      # Login page
    │       ├── Register.jsx   # Registration page
    │       ├── Dashboard.jsx  # Main dashboard
    │       ├── SubmitComplaint.jsx  # Complaint form
    │       ├── MyComplaints.jsx     # User's complaints list
    │       └── Chat.jsx       # Real-time chat interface
```

---

## Prerequisites

Before you start, ensure you have installed:
- **Node.js** (version 18 or higher) - [Download](https://nodejs.org/)
- **MongoDB** - Either:
  - Local installation ([Download](https://www.mongodb.com/try/download/community))
  - MongoDB Atlas (cloud) - [Sign up](https://www.mongodb.com/cloud/atlas)
- **npm** (comes with Node.js)

### Verify Installation
```bash
node --version    # Should be v18+
npm --version     # Should be 8+
mongo --version   # If using local MongoDB
```

---

## Installation & Setup

### Step 1: Clone/Open Project
Navigate to your project directory:
```bash
cd "c:\Users\Seethapavankalyan\OneDrive\Documents\apsche project"
```

### Step 2: Backend Setup

#### Install Dependencies
```bash
cd backend
npm install
```

#### Create Environment File
Create a `.env` file in the `backend/` directory:
```env
PORT=5000
MONGO_URI=mongodb://localhost:27017/resolvenow
JWT_SECRET=your_secret_key_here_change_in_production
NODE_ENV=development
```

**Note**: 
- `MONGO_URI`: Connection string to MongoDB (local or Atlas)
- `JWT_SECRET`: Generate a strong secret for token signing
- Change `JWT_SECRET` in production!

#### Start Backend Server
```bash
# Development (with auto-reload)
npm run dev

# Production
npm start
```

Server will run on `http://localhost:5000`

### Step 3: Frontend Setup

#### Install Dependencies
```bash
cd frontend
npm install
```

#### Start Development Server
```bash
npm run dev
```

Frontend will run on `http://localhost:5173` (or next available port)

### Step 4: Access Application
Open your browser and go to `http://localhost:5173`

---

## Configuration

### Backend Configuration

#### MongoDB Connection (config/db.js)
The database module handles connection pooling and error handling.

#### Environment Variables (.env)
| Variable | Description | Example |
|----------|-------------|---------|
| `PORT` | Server port | 5000 |
| `MONGO_URI` | MongoDB connection string | mongodb://localhost:27017/resolvenow |
| `JWT_SECRET` | Secret key for JWT signing | your-secret-key |
| `NODE_ENV` | Environment mode | development/production |

### Frontend Configuration

#### API Base URL (src/api.js)
By default, the frontend expects the backend at `http://localhost:5000`.

To change the API URL:
```javascript
// In src/api.js or environment config
const API_BASE_URL = process.env.REACT_APP_API_URL || 'http://localhost:5000';
```

---

## API Documentation

### Authentication Endpoints

#### Register User
```http
POST /api/auth/register
Content-Type: application/json

{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "password123"
}
```

**Response** (201):
```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "user": {
    "id": "64a5f8b2c1d2e3f4g5h6i7j8",
    "name": "John Doe",
    "email": "john@example.com",
    "role": "user"
  }
}
```

#### Login User
```http
POST /api/auth/login
Content-Type: application/json

{
  "email": "john@example.com",
  "password": "password123"
}
```

**Response** (200):
```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "user": {
    "id": "64a5f8b2c1d2e3f4g5h6i7j8",
    "name": "John Doe",
    "email": "john@example.com",
    "role": "user"
  }
}
```

#### Get Current User
```http
GET /api/auth/me
Authorization: Bearer {token}
```

**Response** (200):
```json
{
  "id": "64a5f8b2c1d2e3f4g5h6i7j8",
  "name": "John Doe",
  "email": "john@example.com",
  "role": "user"
}
```

---

### Complaint Endpoints

#### Create Complaint
```http
POST /api/complaints
Authorization: Bearer {token}
Content-Type: application/json

{
  "title": "Water supply issue in building",
  "description": "No water in the building since morning",
  "images": ["base64-encoded-image-1", "base64-encoded-image-2"]
}
```

**Response** (200):
```json
{
  "_id": "64a5f8b2c1d2e3f4g5h6i7j8",
  "title": "Water supply issue in building",
  "description": "No water in the building since morning",
  "images": ["base64-encoded-image-1", "base64-encoded-image-2"],
  "status": "open",
  "user": "64a5f8b2c1d2e3f4g5h6i7j8",
  "assignedTo": null,
  "messages": [],
  "createdAt": "2025-03-08T10:30:00Z"
}
```

#### Get My Complaints
```http
GET /api/complaints/mine
Authorization: Bearer {token}
```

**Response** (200):
```json
[
  {
    "_id": "64a5f8b2c1d2e3f4g5h6i7j8",
    "title": "Water supply issue",
    "description": "No water in the building",
    "status": "open",
    "user": "64a5f8b2c1d2e3f4g5h6i7j8",
    "assignedTo": {
      "_id": "64a5f8b2c1d2e3f4g5h6i7j9",
      "name": "Agent Smith",
      "email": "agent@example.com"
    },
    "createdAt": "2025-03-08T10:30:00Z"
  }
]
```

#### Get All Complaints (Admin/Agent)
```http
GET /api/complaints
Authorization: Bearer {token}
```

**Response** (200): Array of all complaints

#### Assign Complaint
```http
PUT /api/complaints/:id/assign
Authorization: Bearer {token}
Content-Type: application/json

{
  "agentId": "64a5f8b2c1d2e3f4g5h6i7j9"
}
```

**Response** (200): Updated complaint with status "in_progress"

#### Update Complaint Status
```http
PUT /api/complaints/:id/status
Authorization: Bearer {token}
Content-Type: application/json

{
  "status": "resolved"
}
```

**Status Values**: `open`, `in_progress`, `resolved`, `closed`

**Response** (200): Updated complaint

#### Add Message to Complaint
```http
POST /api/complaints/:id/message
Authorization: Bearer {token}
Content-Type: application/json

{
  "text": "We are working on fixing the water supply issue"
}
```

**Response** (200): Updated complaint with new message

---

## Database Models

### User Schema

```javascript
{
  name: String (required),
  email: String (required, unique),
  password: String (hashed, required),
  role: String (enum: ['user', 'agent', 'admin'], default: 'user'),
  createdAt: Date (default: current date)
}
```

**Indexes**: `email` (unique)

### Complaint Schema

```javascript
{
  title: String (required),
  description: String,
  images: [String],  // Base64 encoded or URLs
  status: String (enum: ['open', 'in_progress', 'resolved', 'closed'], default: 'open'),
  user: ObjectId (ref: User),  // Who filed the complaint
  assignedTo: ObjectId (ref: User),  // Assigned agent/admin
  messages: [MessageSchema],  // Chat messages
  createdAt: Date (default: current date)
}
```

### Message Schema (Embedded in Complaint)

```javascript
{
  sender: ObjectId (ref: User),
  text: String,
  createdAt: Date (default: current date)
}
```

---

## Frontend Components

### Page Components

#### Login.jsx
- User login form
- Email and password fields
- JWT token storage
- Redirect to dashboard on success
- Error handling and validation

#### Register.jsx
- User registration form
- Name, email, password fields
- Password confirmation
- Automatic login after registration
- Email validation

#### Dashboard.jsx
- Main application hub
- Navigation to other pages
- User profile information
- Quick complaint stats (if implemented)

#### SubmitComplaint.jsx
- Complaint creation form
- Title and description fields
- Image upload functionality
- Form validation
- Success/error notifications

#### MyComplaints.jsx
- List of user's complaints
- Complaint cards showing:
  - Title and description
  - Current status (color-coded)
  - Assigned agent name
  - Creation date
- Filter/search functionality (optional)
- Link to individual complaint details

#### Chat.jsx
- Real-time messaging interface
- Show complaint details
- Message history
- Live message updates via Socket.io
- Message input field

### Utility Files

#### api.js (API Client)
- Axios instance configured with base URL
- Pre-configured headers with JWT token
- API method definitions for:
  - Authentication
  - Complaint CRUD operations
  - Message operations

---

## Authentication & Authorization

### JWT Token Flow

1. **Registration/Login**: User sends credentials → Server validates → Creates JWT token
2. **Token Storage**: Frontend stores token in localStorage
3. **API Requests**: Every request includes `Authorization: Bearer {token}` header
4. **Token Verification**: Middleware (`auth.js`) validates token on protected routes
5. **Token Expiry**: Tokens expire in 7 days

### Middleware (middleware/auth.js)
```javascript
- Verifies JWT token from request headers
- Extracts user information from token
- Attaches user to request object
- Rejects invalid/expired tokens
```

### Role-Based Access Control

| Role | Permissions |
|------|-------------|
| **user** | Submit complaints, view own complaints, chat with agents |
| **agent** | View all complaints, assign to self, update status, chat with users |
| **admin** | Full system access, manage users, manage all complaints |

---

## Real-time Features

### Socket.io Implementation

#### Client-Server Events

**Client → Server**:
```javascript
socket.emit('joinRoom', { complaintId });  // Join complaint chat room
socket.emit('message', { complaintId, message });  // Send message
```

**Server → Client**:
```javascript
socket.on('message', (message));  // Receive new message
socket.on('statusUpdate', (status));  // Receive status update
```

#### Features
- Real-time chat for each complaint
- Automatic room joining by complaint ID
- Message broadcasting to all connected users in a complaint room
- Connection/disconnection logging

### Socket Connection
```javascript
// Frontend
const socket = io('http://localhost:5000');

// Backend
const io = new Server(server, { cors: { origin: '*' } });
```

---

## Development Guide

### Running All Services

#### Terminal 1 - Backend
```bash
cd backend
npm run dev
```

#### Terminal 2 - Frontend
```bash
cd frontend
npm run dev
```

#### Terminal 3 - MongoDB (if local)
```bash
mongod
```

### Common Development Tasks

#### Add a New API Endpoint

1. **Create Controller** (`backend/controllers/`):
```javascript
exports.newFunction = async (req, res) => {
  try {
    // Implementation
    res.json({ success: true });
  } catch (err) {
    res.status(500).send('Server error');
  }
};
```

2. **Add Route** (`backend/routes/`):
```javascript
router.get('/endpoint', auth, newFunction);
```

3. **Update Frontend** (`frontend/src/api.js`):
```javascript
export const newApiCall = (data) => {
  return api.get('/endpoint', { params: data });
};
```

#### Add a New Frontend Component

1. Create file in `frontend/src/pages/ComponentName.jsx`
2. Import in `App.jsx` and add to router:
```javascript
import ComponentName from './pages/ComponentName';

<Route path="/component" element={<ComponentName />} />
```

#### Database Query Debugging

Use MongoDB Compass or CLI:
```bash
# MongoDB Shell
mongosh
use resolvenow
db.users.find()
db.complaints.find()
```

---

## Deployment Notes

### ⚠️ Before Production Deployment

1. **Security Hardening**
   - [ ] Change `JWT_SECRET` to a strong, random key
   - [ ] Implement input validation and sanitization
   - [ ] Add rate limiting to API endpoints
   - [ ] Enable HTTPS only
   - [ ] Set secure CORS origins (not `*`)

2. **Data Protection**
   - [ ] Hash all passwords (already implemented)
   - [ ] Validate and sanitize all inputs
   - [ ] Implement encryption for sensitive data
   - [ ] Set up database backups

3. **Error Handling**
   - [ ] Remove console.log statements
   - [ ] Implement proper error logging
   - [ ] Create user-friendly error messages
   - [ ] Hide stack traces from clients

4. **Performance**
   - [ ] Add database indexes for frequent queries
   - [ ] Implement caching strategies
   - [ ] Optimize image handling (compression, CDN)
   - [ ] Set up monitoring and logging

5. **File Upload Handling**
   - [ ] Implement file size limits
   - [ ] Validate file types
   - [ ] Scan files for malware
   - [ ] Use secure storage (AWS S3, etc.)

### Deployment Platforms

**Backend**:
- Heroku
- AWS EC2 / ECS
- DigitalOcean
- Railway
- Render

**Frontend**:
- Vercel
- Netlify
- AWS S3 + CloudFront
- DigitalOcean

**Database**:
- MongoDB Atlas (recommended)
- AWS DocumentDB
- Self-hosted MongoDB

### Environment Variables for Production
```env
PORT=5000
MONGO_URI=mongodb+srv://user:password@cluster.mongodb.net/resolvenow
JWT_SECRET=your_strong_secret_key_here
NODE_ENV=production
```

---

## Troubleshooting

### MongoDB Connection Issues
- **Error**: `Error connecting to MongoDB`
- **Solution**: 
  - Ensure MongoDB is running
  - Check `MONGO_URI` in `.env`
  - Verify network connection if using MongoDB Atlas

### CORS Errors
- **Error**: `Access to XMLHttpRequest blocked by CORS`
- **Solution**:
  - Check backend CORS configuration
  - Ensure frontend URL matches allowed origins
  - Verify API_BASE_URL in frontend config

### Token Expiry
- **Error**: `Token expired`
- **Solution**:
  - Clear localStorage
  - Re-login to get new token
  - Implement token refresh mechanism

### Socket.io Connection Issues
- **Error**: `Socket connection refused`
- **Solution**:
  - Ensure both frontend and backend running
  - Check Socket.io configuration and CORS
  - Verify correct server URL in frontend

---

## Future Enhancements

- [ ] Email notifications for complaint updates
- [ ] File upload with storage (AWS S3, Cloudinary)
- [ ] Advanced complaint filtering and search
- [ ] Analytics dashboard
- [ ] Complaint prioritization system
- [ ] SLA (Service Level Agreement) tracking
- [ ] Mobile app version
- [ ] Two-factor authentication
- [ ] Complaint rating and feedback system
- [ ] Multi-language support

---

## Contributing

To contribute to this project:
1. Create a new branch
2. Make your changes
3. Test thoroughly
4. Submit a pull request with description

---

## Support & Documentation

For additional help:
- Review code comments
- Check official documentation for dependencies
- Use browser DevTools for frontend debugging
- Use MongoDB Compass for database inspection

---

## Changelog

### Version 1.0.0 (Initial Release)
- User authentication and authorization
- Complaint registration and tracking
- Real-time chat with Socket.io
- Role-based access control
- Responsive UI with Bootstrap

---

**Last Updated**: March 8, 2025
**Project Version**: 1.0.0
**Status**: Active Development
