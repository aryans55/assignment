# Ethara Website Assignment

<div align="center">
  <img src="https://via.placeholder.com/150" alt="Ethara Logo" width="150" height="150">
  <h3>Next-Generation Event & Booking Platform</h3>
  <p>A comprehensive full-stack solution built to handle events, ticketing, and user management.</p>
</div>

---

## 📖 Table of Contents
1. [Overview](#-overview)
2. [Key Features](#-key-features)
3. [Architecture](#-architecture)
4. [Tech Stack](#-tech-stack)
5. [Folder Structure](#-folder-structure)
6. [Prerequisites](#-prerequisites)
7. [Installation & Setup](#-installation--setup)
8. [Environment Variables](#-environment-variables)
9. [Available Scripts](#-available-scripts)
10. [API Documentation](#-api-documentation)
11. [Testing](#-testing)
12. [Deployment](#-deployment)
13. [Contributing](#-contributing)
14. [Troubleshooting](#-troubleshooting)
15. [License](#-license)

---

## 🌟 Overview
The **Ethara Website Assignment** is a robust, scalable, and responsive web application designed for seamless event management and ticketing. It offers a rich user interface crafted for optimal user experience, backed by a high-performance RESTful API that handles complex business logic, user authentication, and secure transactions.

Whether you're an admin managing events or a user purchasing tickets, this application provides all the tools you need in a modern, secure environment.

---

## ✨ Key Features

### 👤 User Features
- **Secure Authentication:** Registration, login, and password recovery using JWT-based authentication.
- **Dynamic Dashboard:** Personalized user dashboard to track upcoming events and past bookings.
- **Real-Time Booking:** Instant ticket generation with QR code integration.
- **Responsive Design:** A mobile-first approach ensuring the UI looks flawless on desktops, tablets, and smartphones.
- **Dark/Light Mode:** Integrated theme switching for accessibility.

### 🛡️ Admin Features
- **Role-Based Access Control (RBAC):** Strict permissions distinguishing between standard users, event organizers, and super admins.
- **Event Management:** Create, edit, publish, and delete events. Upload promotional banners via Cloudinary.
- **Analytics:** Visual charts mapping ticket sales and user demographics.
- **User Management:** Ability to ban, suspend, or elevate user privileges.

---

## 🏛️ Architecture
This project strictly follows the **Client-Server Architecture**.
- **Frontend (Client):** A Single Page Application (SPA) providing an interactive user interface, state management, and client-side routing.
- **Backend (Server):** A stateless REST API handling requests, business logic, validation, and database operations.
- **Database:** A NoSQL approach ensuring high flexibility and horizontal scalability for event data.

---

## 🛠️ Tech Stack

### Frontend
- **Framework:** React.js (Vite)
- **State Management:** Redux Toolkit / React Context
- **Styling:** Tailwind CSS / Styled Components
- **Routing:** React Router DOM
- **Data Fetching:** Axios / React Query

### Backend
- **Runtime:** Node.js
- **Framework:** Express.js
- **Database:** MongoDB (via Mongoose ODM)
- **Authentication:** JSON Web Tokens (JWT) & bcrypt.js
- **File Storage:** AWS S3 / Cloudinary (for images)

---

## 📂 Folder Structure

This repository is structured as a **Monorepo**, cleanly separating the client-side and server-side codebases.

```text
etharaWebsit-main/
├── frontend/                  # React Frontend Application
│   ├── public/                # Static assets (favicons, images)
│   ├── src/
│   │   ├── components/        # Reusable UI components (Buttons, Modals)
│   │   ├── pages/             # Page components (Home, Login, Dashboard)
│   │   ├── services/          # API integration and Axios instances
│   │   ├── styles/            # Global CSS / Tailwind configurations
│   │   ├── utils/             # Helper functions and constants
│   │   ├── App.js             # Root component and Routes
│   │   └── index.js           # Entry point
│   └── package.json           # Frontend dependencies
│
├── backend/                   # Node.js/Express Backend API
│   ├── src/
│   │   ├── config/            # Database and environment configurations
│   │   ├── controllers/       # Route handlers and business logic
│   │   ├── middleware/        # Custom middlewares (Auth, Error Handling)
│   │   ├── models/            # Mongoose schemas and database models
│   │   ├── routes/            # Express route definitions
│   │   ├── utils/             # Utility classes (AppError, logger)
│   │   └── server.js          # Main application entry point
│   └── package.json           # Backend dependencies
│
└── README.md                  # Project documentation (You are here)
```

---

## 📋 Prerequisites
Before you begin, ensure you have the following installed on your local machine:
- [Node.js](https://nodejs.org/en/) (v16.x or higher)
- [npm](https://www.npmjs.com/) (v8.x or higher) or [Yarn](https://yarnpkg.com/)
- [MongoDB](https://www.mongodb.com/) (Local instance or MongoDB Atlas cluster)
- [Git](https://git-scm.com/)

---

## 🚀 Installation & Setup

Follow these steps to get your development environment up and running.

### 1. Clone the Repository
```bash
git clone https://github.com/aryans55/assignment.git
cd etharaWebsit-main
```

### 2. Setup the Backend
Open a new terminal window and navigate to the backend directory:
```bash
cd backend
npm install
```
Configure your environment variables (see next section), then start the server:
```bash
npm run dev
```
The backend server should now be running on `http://localhost:5000`.

### 3. Setup the Frontend
Open a new terminal window and navigate to the frontend directory:
```bash
cd frontend
npm install
```
Start the React development server:
```bash
npm start
```
The frontend application should now be running on `http://localhost:3000`.

---

## 🔐 Environment Variables

For the application to function correctly, you must set up the necessary environment variables. 
Create a `.env` file in **both** the `frontend` and `backend` directories.

### Backend `.env`
```env
PORT=5000
NODE_ENV=development
MONGO_URI=mongodb+srv://<username>:<password>@cluster.mongodb.net/ethara?retryWrites=true&w=majority
JWT_SECRET=your_super_secret_jwt_key_here
JWT_EXPIRES_IN=30d
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret
```

### Frontend `.env`
```env
REACT_APP_API_URL=http://localhost:5000/api/v1
REACT_APP_ENVIRONMENT=development
```

---

## 📜 Available Scripts

### Backend Scripts (`/backend`)
- `npm start`: Starts the application in production mode.
- `npm run dev`: Starts the application in development mode using Nodemon (auto-restarts on file changes).
- `npm run seed`: Populates the database with sample dummy data for testing.
- `npm run lint`: Runs ESLint to check for code formatting issues.

### Frontend Scripts (`/frontend`)
- `npm start`: Runs the app in development mode.
- `npm run build`: Builds the app for production to the `build` folder.
- `npm test`: Launches the test runner in interactive watch mode.
- `npm run eject`: Ejects the Create React App configuration for custom tweaking.

---

## 🔌 API Documentation

The backend exposes a comprehensive RESTful API. Below are some of the primary endpoints.

### Authentication Endpoints
| Method | Endpoint | Description | Access |
|---|---|---|---|
| POST | `/api/v1/auth/register` | Register a new user | Public |
| POST | `/api/v1/auth/login` | Authenticate user & get token | Public |
| GET | `/api/v1/auth/me` | Get current logged-in user | Private |
| POST | `/api/v1/auth/forgotpassword`| Send password reset email | Public |

### Event Endpoints
| Method | Endpoint | Description | Access |
|---|---|---|---|
| GET | `/api/v1/events` | Get all events (with filtering) | Public |
| GET | `/api/v1/events/:id` | Get single event details | Public |
| POST | `/api/v1/events` | Create a new event | Admin |
| PUT | `/api/v1/events/:id` | Update an existing event | Admin |
| DELETE| `/api/v1/events/:id` | Delete an event | Admin |

### User Endpoints
| Method | Endpoint | Description | Access |
|---|---|---|---|
| GET | `/api/v1/users` | Get all users | Admin |
| GET | `/api/v1/users/:id` | Get specific user | Admin |
| PUT | `/api/v1/users/:id` | Update user roles | Admin |
| DELETE| `/api/v1/users/:id` | Remove a user account | Admin |

*(Detailed API documentation, including request payloads and response schemas, will be provided via Swagger/Postman collection in the future).*

---

## 🧪 Testing

We value code reliability. This project uses the following testing frameworks:
- **Backend:** Jest & Supertest (Integration & Unit testing)
- **Frontend:** React Testing Library & Jest (Component testing)

To run the test suites:
```bash
# In the backend directory
npm test

# In the frontend directory
npm test
```

---

## ☁️ Deployment

### Backend Deployment (Render / Heroku)
1. Connect your GitHub repository to Render.
2. Set the build command to `npm install`.
3. Set the start command to `npm start`.
4. Inject all environment variables in the Render dashboard.

### Frontend Deployment (Vercel / Netlify)
1. Import the repository into Vercel.
2. Set the root directory to `frontend/`.
3. Vercel will automatically detect Create React App / Vite and configure build settings.
4. Add the `REACT_APP_API_URL` pointing to your deployed backend.

---

## 🤝 Contributing

Contributions are what make the open-source community such an amazing place to learn, inspire, and create. Any contributions you make are **greatly appreciated**.

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

Please ensure your code follows the established formatting rules. We use Prettier and ESLint to maintain code quality.

---

## 🐛 Troubleshooting

- **MongoDB Connection Error:** Ensure your IP address is whitelisted in MongoDB Atlas. Check your `MONGO_URI` in the `.env` file.
- **CORS Issues:** If the frontend cannot communicate with the backend, verify that your backend `app.use(cors())` configuration allows the frontend origin.
- **Node Sass/Bcrypt Bindings:** If you encounter native compilation errors, try deleting `node_modules` and `package-lock.json`, then run `npm cache clean --force` followed by `npm install`.

---

## 📄 License

Distributed under the **MIT License**. See `LICENSE` for more information.

---
<div align="center">
  <p>Made with ❤️ for the Ethara Assignment.</p>
</div>
