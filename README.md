# Team Task Manager (Ertha1 - Assignment)

<div align="center">
  <h3>A premium, full-stack web application for project and task management with role-based access control.</h3>
  <p>Streamline your workflow, manage team collaboration, and track project progress in real-time.</p>
</div>

---

## 📑 Table of Contents
1. [Overview](#-overview)
2. [Key Features](#-key-features)
3. [Architecture & Tech Stack](#-architecture--tech-stack)
4. [Folder Structure](#-folder-structure)
5. [Prerequisites](#-prerequisites)
6. [Setup Instructions](#-setup-instructions)
7. [Demo Credentials](#-demo-credentials)
8. [API Documentation](#-api-documentation)
9. [Database Schema](#-database-schema)
10. [Deployment (Railway)](#-deployment-railway)
11. [Contributing](#-contributing)
12. [License](#-license)

---

## 🌟 Overview
Team Task Manager is an intuitive and robust application designed to help teams coordinate efficiently. 
With strict Role-Based Access Control (RBAC), admins can oversee projects and assign tasks, while team members can focus on execution. 
The application provides real-time dashboard analytics, seamless authentication, and a highly responsive user interface.

---

## ✨ Key Features

### 🔐 Authentication & Security
- **Secure Authentication**: Robust signup and login using JWT (JSON Web Tokens).
- **Data Protection**: Passwords are securely hashed using bcrypt before being stored in the database.
- **Input Validation**: All incoming API requests are validated using Zod to prevent malicious data entry.

### 🛡️ Role-Based Access Control
- **Admin Role**: 
  - Complete oversight over the platform.
  - Create, edit, and archive projects.
  - Assign specific tasks to team members.
  - Manage team directory and user roles.
- **Member Role**:
  - View individually assigned projects and tasks.
  - Update task progress and status (e.g., To-Do, In Progress, Completed).

### 📊 Project & Task Management
- **Project Workspaces**: Group related tasks under specific projects for better organization.
- **Granular Task Control**: Set task priorities (Low, Medium, High), assign due dates, and filter dynamically.
- **Status Tracking**: Keep the whole team updated with real-time status updates on deliverables.

### 📈 Real-Time Dashboard
- **Analytics**: Get instant statistics on active projects, completed tasks, and pending deliverables.
- **Overdue Tracking**: Automatically flags overdue items to ensure deadlines are met.
- **Premium UI/UX**: Built with a clean, modern aesthetic utilizing Tailwind CSS and smooth animations powered by Framer Motion.

---

## 🛠️ Architecture & Tech Stack

This project uses the MERN stack (MongoDB, Express, React, Node) with modern enhancements.

### Frontend (Client)
- **Framework**: React (Bootstrapped with Vite for instant server start and lightning-fast HMR)
- **Styling**: Tailwind CSS for utility-first responsive design.
- **Animations**: Framer Motion for premium, fluid UI transitions.
- **Routing**: React Router DOM.
- **HTTP Client**: Axios for seamless API communication.
- **Icons**: Lucide Icons for crisp, scalable vector graphics.

### Backend (Server)
- **Runtime**: Node.js
- **Framework**: Express.js
- **Database**: MongoDB with Mongoose ODM for structured data modeling.
- **Security**: JWT for stateless session management.
- **Validation**: Zod for strict type and schema validation.

---

## 📂 Folder Structure

```text
root/
├── client/                     # React Frontend
│   ├── public/                 # Static assets
│   ├── src/
│   │   ├── components/         # Reusable UI & Layout (Buttons, Cards, Navbar)
│   │   ├── pages/              # View components (Dashboard, Login, Projects)
│   │   ├── context/            # Global Auth state management
│   │   ├── services/           # Axios interceptors and API communication
│   │   ├── utils/              # Helper functions (date formatting, etc.)
│   │   ├── App.jsx             # Main application router
│   │   └── main.jsx            # React entry point
│   ├── package.json
│   └── vite.config.js
│
├── server/                     # Express Backend
│   ├── src/
│   │   ├── config/             # DB connection and env variables
│   │   ├── models/             # Mongoose schemas (User, Project, Task)
│   │   ├── controllers/        # Business logic for endpoints
│   │   ├── routes/             # API route definitions
│   │   ├── middleware/         # Auth verification & Error handling
│   │   ├── validations/        # Zod validation schemas
│   │   └── index.js            # Server entry point
│   └── package.json
│
└── README.md                   # Project documentation
```

---

## 📋 Prerequisites
- **Node.js** (v16.0.0 or higher)
- **npm** or **yarn**
- **MongoDB** (Local instance or MongoDB Atlas URL)

---

## 🚀 Setup Instructions

### 1. Backend Setup
Navigate to the server directory and install dependencies:
```bash
cd server
npm install
```

Create a `.env` file in the `server` directory (you can copy `.env.example` if available) and add the following variables:
```env
PORT=5000
MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_super_secret_jwt_key
CLIENT_URL=http://localhost:5173
```

Seed the database with initial demo data (users, projects):
```bash
npm run seed
```

Start the backend development server:
```bash
npm run dev
```
*The server will typically run on http://localhost:5000.*

### 2. Frontend Setup
Open a new terminal, navigate to the client directory, and install dependencies:
```bash
cd client
npm install
```

Start the Vite development server:
```bash
npm run dev
```
*The frontend will be available at http://localhost:5173.*

---

## 🔑 Demo Credentials

You can use the following credentials to test the application after running the seed script:

- **Admin Account**: 
  - Email: `admin@test.com` 
  - Password: `Admin@123`
- **Member Account**: 
  - Email: `member@test.com` 
  - Password: `Member@123`

---

## 🔌 API Endpoints Summary

Below is a quick reference for the primary REST API endpoints available in the backend.

### Authentication (`/api/auth`)
| Method | Endpoint | Description | Access |
|---|---|---|---|
| POST | `/signup` | Register a new user | Public |
| POST | `/login` | Authenticate user & get token | Public |
| GET | `/me` | Get current authenticated user profile | Private |

### Projects (`/api/projects`)
| Method | Endpoint | Description | Access |
|---|---|---|---|
| GET | `/` | Fetch all projects | Private (Admin/Member) |
| POST | `/` | Create a new project | Admin |
| PUT | `/:id` | Update project details | Admin |

### Tasks (`/api/tasks`)
| Method | Endpoint | Description | Access |
|---|---|---|---|
| GET | `/` | Fetch all tasks | Private |
| POST | `/` | Create and assign a new task | Admin |
| PATCH | `/:id/status`| Update the status of a specific task | Private |

### Dashboard (`/api/dashboard`)
| Method | Endpoint | Description | Access |
|---|---|---|---|
| GET | `/stats` | Fetch real-time dashboard statistics | Private |

---

## 🗄️ Database Schema (Overview)

- **User Model**: Stores `name`, `email`, `password` (hashed), and `role` (Admin/Member).
- **Project Model**: Stores `title`, `description`, `deadline`, and `createdBy` (Admin reference).
- **Task Model**: Stores `title`, `description`, `status` (To-Do, In Progress, Done), `priority` (Low, Medium, High), `project` (Ref), and `assignee` (Ref).

---

## ☁️ Deployment (Railway)

This application is fully prepared and optimized for deployment on **Railway**.

1. Connect your GitHub repository to your Railway account.
2. In the Railway dashboard, create two services (or one monorepo setup depending on your preference):
   - A **Node.js** service for the server.
   - A **Static/Vite** service for the client.
3. Add the required Environment Variables in the Railway dashboard for the backend service:
   - `MONGO_URI`
   - `JWT_SECRET`
   - `CLIENT_URL` (Set this to your newly generated frontend Railway URL)
4. Ensure the root contains both `client` and `server` folders, or deploy them as separate repositories.
5. Deploy both services. Railway will automatically install dependencies and run the build scripts.

---

## 🤝 Contributing
Contributions are always welcome. To contribute:
1. Fork the repository.
2. Create your feature branch (`git checkout -b feature/NewFeature`).
3. Commit your changes (`git commit -m 'Add NewFeature'`).
4. Push to the branch (`git push origin feature/NewFeature`).
5. Open a Pull Request.

---

## 📄 License
This project is licensed under the MIT License.

---
# ertha1
# assignment-

