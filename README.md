# 💬 ChatSphere - Real-Time Chat Application

> A modern, full-stack real-time messaging application built with Node.js, React, Socket.io, and MongoDB

[![License: ISC](https://img.shields.io/badge/License-ISC-blue.svg)](https://opensource.org/licenses/ISC)
[![Node.js](https://img.shields.io/badge/Node.js-20.x-green.svg)](https://nodejs.org/)
[![React](https://img.shields.io/badge/React-18.x-61dafb.svg)](https://reactjs.org/)
[![MongoDB](https://img.shields.io/badge/MongoDB-6.x-47a248.svg)](https://www.mongodb.com/)

---

## 📋 Table of Contents

- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Prerequisites](#-prerequisites)
- [Installation](#-installation)
- [Configuration](#-configuration)
- [Running the Application](#-running-the-application)
- [API Endpoints](#-api-endpoints)
- [WebSocket Events](#-websocket-events)
- [Project Architecture](#-project-architecture)
- [Key Features Explained](#-key-features-explained)
- [Contributing](#-contributing)
- [License](#-license)

---

## ✨ Features

### Core Features
- ✅ **Real-Time Messaging** - Instant message delivery using Socket.io
- ✅ **User Authentication** - Secure JWT-based authentication with password hashing
- ✅ **Conversation Management** - Create, list, and manage conversations
- ✅ **User Profiles** - Register, login, and manage user profiles
- ✅ **Online Status** - Real-time user online/offline status
- ✅ **Message History** - Persistent message storage with MongoDB
- ✅ **Responsive Design** - Beautiful UI with Tailwind CSS & DaisyUI
- ✅ **Cookie-Based Sessions** - Secure session management

### Technical Highlights
- 🔐 Password encryption with bcryptjs
- 📡 WebSocket communication for real-time updates
- 🗄️ NoSQL database (MongoDB with Mongoose ODM)
- ⚡ Fast build with Vite
- 🎨 Modern UI with Tailwind CSS
- 📦 State management with Zustand
- 🔔 Toast notifications with react-toastify

---

## 🛠 Tech Stack

### Backend
| Technology | Version | Purpose |
|-----------|---------|---------|
| **Express.js** | 4.18.3 | Web framework |
| **Node.js** | 20.x | Runtime environment |
| **MongoDB** | 6.4.0 | Database |
| **Mongoose** | 8.2.0 | ODM for MongoDB |
| **Socket.io** | 4.7.4 | Real-time communication |
| **JWT** | 9.0.2 | Authentication |
| **bcryptjs** | 2.4.3 | Password hashing |
| **Nodemon** | 3.1.0 | Development auto-reload |

### Frontend
| Technology | Version | Purpose |
|-----------|---------|---------|
| **React** | 18.2.0 | UI library |
| **Vite** | 5.1.4 | Build tool |
| **Tailwind CSS** | 3.4.1 | Styling |
| **DaisyUI** | 4.7.2 | Component library |
| **Socket.io Client** | 4.7.4 | WebSocket client |
| **React Router** | 6.22.2 | Routing |
| **Zustand** | 4.5.2 | State management |
| **Axios** | 1.6.7 | HTTP client |

---

## 📁 Project Structure

```
chatsphere/
├── backend/
│   ├── index.js                          # Main server entry point
│   ├── DB/
│   │   └── dbConnect.js                  # MongoDB connection setup
│   ├── middleware/
│   │   └── isLogin.js                    # Authentication middleware
│   ├── Models/
│   │   ├── userModels.js                 # User schema
│   │   ├── messageSchema.js              # Message schema
│   │   └── conversationModels.js         # Conversation schema
│   ├── rout/
│   │   ├── authUser.js                   # Auth routes (register, login)
│   │   ├── messageRout.js                # Message routes
│   │   └── userRout.js                   # User routes
│   ├── routControlers/
│   │   ├── userhandlerControler.js       # Auth logic
│   │   ├── messageroutControler.js       # Message logic
│   │   └── userroutControler.js          # User logic
│   ├── Socket/
│   │   └── socket.js                     # Socket.io configuration
│   └── utils/
│       └── jwtwebToken.js                # JWT token generation
│
├── frontend/
│   ├── src/
│   │   ├── App.jsx                       # Main app component
│   │   ├── main.jsx                      # React entry point
│   │   ├── index.css                     # Global styles
│   │   ├── context/
│   │   │   ├── AuthContext.jsx           # Authentication context
│   │   │   └── SocketContext.jsx         # Socket.io context
│   │   ├── home/
│   │   │   ├── Home.jsx                  # Main chat page
│   │   │   └── components/
│   │   │       ├── Sidebar.jsx           # Conversation sidebar
│   │   │       └── MessageContainer.jsx  # Message display area
│   │   ├── login/
│   │   │   └── Login.jsx                 # Login page
│   │   ├── register/
│   │   │   └── Register.jsx              # Registration page
│   │   ├── utils/
│   │   │   └── VerifyUser.jsx            # User verification utility
│   │   ├── Zustans/
│   │   │   └── useConversation.js        # Conversation state store
│   │   └── assets/
│   │       └── sound/                    # Notification sounds
│   ├── vite.config.js                    # Vite configuration
│   ├── tailwind.config.js                # Tailwind CSS config
│   ├── postcss.config.js                 # PostCSS config
│   └── package.json
│
├── package.json                          # Root package.json
└── README.md                             # This file
```

---

## 📦 Prerequisites

Before you begin, ensure you have the following installed:

- **Node.js** (v16.0.0 or higher) - [Download](https://nodejs.org/)
- **npm** (v8.0.0 or higher) - comes with Node.js
- **MongoDB** (v5.0 or higher) - [Download](https://www.mongodb.com/try/download/community) or use [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
- **Git** - [Download](https://git-scm.com/)

---

## 🚀 Installation

### 1. Clone the Repository
```bash
git clone https://github.com/yourusername/chatsphere.git
cd chatsphere
```

### 2. Install Backend Dependencies
```bash
npm install
```

### 3. Install Frontend Dependencies
```bash
npm install --prefix frontend
```

### 4. Install All at Once
```bash
npm run build
```

---

## ⚙️ Configuration

### 1. Create `.env` File in Root Directory

Create a `.env` file in the root directory with the following variables:

```env
# Server Configuration
PORT=3000
NODE_ENV=development

# Database Configuration
MONGODB_URI=mongodb://localhost:27017/chatsphere
# OR for MongoDB Atlas:
# MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/chatsphere?retryWrites=true&w=majority

# JWT Configuration
JWT_SECRET=your_jwt_secret_key_here_min_32_characters
JWT_EXPIRY=7d

# CORS Configuration (if needed)
CORS_ORIGIN=http://localhost:5173
```

### 2. MongoDB Setup

**Local MongoDB:**
```bash
# Windows (if installed)
mongod

# Linux/Mac
mongod
```

**MongoDB Atlas Cloud:**
1. Go to [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
2. Create a free account
3. Create a cluster
4. Get your connection string
5. Add it to your `.env` file

---

## ▶️ Running the Application

### Development Mode

**Terminal 1 - Start Backend Server:**
```bash
npm run dev
```
The backend will run on `http://localhost:3000`

**Terminal 2 - Start Frontend Development Server:**
```bash
npm run dev --prefix frontend
```
The frontend will run on `http://localhost:5173`

### Production Mode

**Build Frontend:**
```bash
npm run build --prefix frontend
```

**Start Server:**
```bash
npm start
```
Access the application at `http://localhost:3000`

---

## 📡 API Endpoints

### Authentication Routes (`/api/auth`)

| Method | Endpoint | Description | Auth |
|--------|----------|-------------|------|
| POST | `/register` | Register new user | ❌ |
| POST | `/login` | Login user | ❌ |
| POST | `/logout` | Logout user | ✅ |

**Register Request:**
```json
{
  "email": "user@example.com",
  "password": "securePassword123",
  "username": "username"
}
```

**Login Request:**
```json
{
  "email": "user@example.com",
  "password": "securePassword123"
}
```

### User Routes (`/api/user`)

| Method | Endpoint | Description | Auth |
|--------|----------|-------------|------|
| GET | `/` | Get all users | ✅ |
| GET | `/profile` | Get current user profile | ✅ |
| GET | `/:id` | Get user by ID | ✅ |

### Message Routes (`/api/message`)

| Method | Endpoint | Description | Auth |
|--------|----------|-------------|------|
| POST | `/send/:id` | Send message to user | ✅ |
| GET | `/conversations` | Get user conversations | ✅ |
| GET | `/:conversationId` | Get messages in conversation | ✅ |

---

## 🔌 WebSocket Events

### Client to Server Events

| Event | Payload | Description |
|-------|---------|-------------|
| `join` | `{ userId }` | User joins socket connection |
| `send_message` | `{ conversationId, message }` | Send real-time message |
| `typing` | `{ conversationId, userId }` | User is typing |
| `stop_typing` | `{ conversationId, userId }` | User stopped typing |

### Server to Client Events

| Event | Payload | Description |
|-------|---------|-------------|
| `receive_message` | `{ message }` | New message received |
| `user_online` | `{ userId }` | User came online |
| `user_offline` | `{ userId }` | User went offline |
| `user_typing` | `{ userId }` | User is typing |
| `user_stop_typing` | `{ userId }` | User stopped typing |

---

## 🏗️ Project Architecture

### Data Flow

```
┌─────────────────────────────────────────────────────────────────┐
│                       FRONTEND (React + Vite)                   │
│                                                                  │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐          │
│  │   Login/Reg  │  │ Home/Chat UI │  │ Sidebar      │          │
│  │   Components │  │              │  │              │          │
│  └──────────────┘  └──────────────┘  └──────────────┘          │
│         │                │                    │                 │
│         └────────────────┼────────────────────┘                 │
│                          │                                      │
│         ┌────────────────┴────────────────┐                    │
│         │   Context API & Zustand Store   │                    │
│         │   (Auth & Conversation State)   │                    │
│         └────────────────┬────────────────┘                    │
└─────────────────────────┼──────────────────────────────────────┘
                          │
                ┌─────────┴──────────┐
                │                    │
         ┌──────▼──────┐      ┌──────▼──────┐
         │ REST API    │      │ WebSocket   │
         │ (Axios)     │      │ (Socket.io) │
         └──────┬──────┘      └──────┬──────┘
                │                    │
└─────────────────┼────────────────────────────────────────────────┘
                  │
┌─────────────────▼────────────────────────────────────────────────┐
│              BACKEND (Express.js + Node.js)                      │
│                                                                  │
│  ┌──────────────────┐  ┌─────────────────────────────────────┐ │
│  │   API Routes     │  │   WebSocket Handler                 │ │
│  │  - Auth Router   │  │  - Real-time messaging              │ │
│  │  - User Router   │  │  - Online status                    │ │
│  │  - Message Router│  │  - Typing indicators                │ │
│  └──────────────────┘  └─────────────────────────────────────┘ │
│         │                             │                         │
│         └──────────────┬──────────────┘                         │
│                        │                                        │
│        ┌───────────────▼───────────────┐                       │
│        │   Controllers & Logic         │                       │
│        │  - Auth Controller            │                       │
│        │  - Message Controller         │                       │
│        │  - User Controller            │                       │
│        └───────────────┬───────────────┘                       │
│                        │                                        │
│        ┌───────────────▼───────────────┐                       │
│        │   Data Models (Mongoose)      │                       │
│        │  - User Schema                │                       │
│        │  - Message Schema             │                       │
│        │  - Conversation Schema        │                       │
│        └───────────────┬───────────────┘                       │
└─────────────────────────┼──────────────────────────────────────┘
                          │
┌─────────────────────────▼──────────────────────────────────────┐
│              DATABASE (MongoDB)                                │
│                                                                │
│  ┌────────────┐  ┌──────────────┐  ┌──────────────────┐       │
│  │   Users    │  │   Messages   │  │  Conversations   │       │
│  │  Collection│  │  Collection  │  │  Collection      │       │
│  └────────────┘  └──────────────┘  └──────────────────┘       │
└────────────────────────────────────────────────────────────────┘
```

### Authentication Flow

```
User Input (Email/Password)
       │
       ▼
Frontend: Login Component
       │
       ▼
POST /api/auth/login
       │
       ▼
Backend: Auth Controller
       │
       ├─▶ Validate input
       ├─▶ Find user in DB
       ├─▶ Compare password (bcryptjs)
       │
       ▼
Generate JWT Token
       │
       ▼
Set HttpOnly Cookie
       │
       ▼
Response to Frontend
       │
       ▼
Save Auth State (Context/Zustand)
       │
       ▼
Redirect to Home
```

---

## 🎯 Key Features Explained

### 1. Real-Time Messaging
- Uses Socket.io for WebSocket connections
- Messages are stored in MongoDB for history
- Users receive instant notifications of new messages

### 2. Authentication & Security
- Passwords are hashed using bcryptjs
- JWT tokens for session management
- HttpOnly cookies for additional security
- Middleware to verify user authentication

### 3. Conversation Management
- Each conversation links two users
- Messages are grouped by conversations
- Users can see all their conversations and start new ones

### 4. Online Status
- Socket.io tracks user connections
- Real-time online/offline status updates
- Broadcasting user status to all connected clients

### 5. State Management
- **Frontend**: Zustand for lightweight conversation state
- **Context API**: For authentication and socket connection
- **Backend**: Session management with JWT

---

## 🤝 Contributing

Contributions are welcome! Here's how you can help:

1. **Fork the repository**
   ```bash
   git clone https://github.com/yourusername/chatsphere.git
   ```

2. **Create a feature branch**
   ```bash
   git checkout -b feature/AmazingFeature
   ```

3. **Commit your changes**
   ```bash
   git commit -m 'Add some AmazingFeature'
   ```

4. **Push to the branch**
   ```bash
   git push origin feature/AmazingFeature
   ```

5. **Open a Pull Request**

### Development Guidelines
- Follow existing code style
- Add comments for complex logic
- Test your changes before submitting
- Update documentation as needed

---

## 🔮 Future Enhancements

- [ ] Group conversations
- [ ] File sharing and media uploads
- [ ] Message search functionality
- [ ] User presence indicators (typing, online, away)
- [ ] Message reactions and emojis
- [ ] Voice and video calling
- [ ] Dark mode support
- [ ] User blocking functionality
- [ ] Message encryption
- [ ] Push notifications

---



## 🙏 Acknowledgments

- Express.js community
- Socket.io documentation
- MongoDB documentation
- React documentation
- Tailwind CSS and DaisyUI
- All contributors and testers

---




