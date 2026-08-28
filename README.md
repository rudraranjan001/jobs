# 💼 JobHunt - Full-Stack Job Portal Application

A modern, full-stack Job Portal platform built with the **MERN stack** (MongoDB, Express.js, React, Node.js), **Tailwind CSS**, and **Redux Toolkit**. It connects recruiters and job seekers seamlessly with role-based features, real-time application tracking, resume/avatar uploads via Cloudinary, and an intuitive UI.

---

## 📑 Table of Contents

- [Features](#-features)
  - [For Job Seekers (Candidates)](#for-job-seekers-candidates)
  - [For Recruiters (Admins)](#for-recruiters-admins)
- [Tech Stack](#-tech-stack)
- [Project Architecture](#-project-architecture)
- [Getting Started](#-getting-started)
  - [Prerequisites](#prerequisites)
  - [1. Clone the Repository](#1-clone-the-repository)
  - [2. Backend Setup](#2-backend-setup)
  - [3. Frontend Setup](#3-frontend-setup)
- [Environment Variables](#-environment-variables)
- [API Endpoints Overview](#-api-endpoints-overview)
- [Folder Structure](#-folder-structure)
- [Deployment](#-deployment)
- [Contributing](#-contributing)
- [License](#-license)

---

## ✨ Features

### For Job Seekers (Candidates)
- 🔐 **Authentication & Authorization**: Secure signup and login with JWT stored in HTTP-only cookies and bcrypt password hashing.
- 🔍 **Explore & Search Jobs**: Search and filter jobs by keywords, locations, categories, and salary ranges.
- 📄 **Interactive Job Details**: Detailed view of job descriptions, responsibilities, requirements, and company profiles.
- ⚡ **One-Click Application**: Easily apply for open positions and prevent duplicate applications.
- 👤 **Profile & Resume Management**: Update bio, contact details, skills, profile picture, and upload/update resume PDFs.
- 📊 **Application History**: Track applied jobs and monitor recruitment status in real-time (`Pending`, `Accepted`, `Rejected`).

### For Recruiters (Admins)
- 🏢 **Company Registration & Management**: Create and configure company details, logos, descriptions, and official websites.
- 📝 **Post & Manage Jobs**: Create job listings with salary, experience level, position count, job type, requirements, and location.
- 👥 **Applicant Tracking System (ATS)**: View all applicants for posted positions along with their profiles and uploaded resumes.
- 🔄 **Application Status Updates**: Accept or reject candidate applications with instantaneous updates.
- 🛡️ **Protected Admin Routes**: Dedicated recruiter dashboard guarded by role verification.

---

## 🛠️ Tech Stack

### Frontend
- **Framework**: [React 18](https://react.dev/) + [Vite](https://vitejs.dev/)
- **State Management**: [Redux Toolkit](https://redux-toolkit.js.org/) + [Redux Persist](https://github.com/rt2zz/redux-persist)
- **Styling**: [Tailwind CSS](https://tailwindcss.com/) + [Radix UI](https://www.radix-ui.com/) (shadcn/ui style components)
- **Animations & Icons**: [Framer Motion](https://www.framer.com/motion/) + [Lucide React](https://lucide.dev/)
- **Routing**: [React Router DOM v6](https://reactrouter.com/)
- **Notifications**: [Sonner](https://sonner.emilkowal.ski/)
- **HTTP Client**: [Axios](https://axios-http.com/)

### Backend
- **Runtime**: [Node.js](https://nodejs.org/) (ES Modules)
- **Framework**: [Express.js](https://expressjs.com/)
- **Database**: [MongoDB](https://www.mongodb.com/) with [Mongoose ODM](https://mongoosejs.com/)
- **Authentication**: [JSON Web Tokens (JWT)](https://jwt.io/) + [Cookie-Parser](https://www.npmjs.com/package/cookie-parser) + [bcryptjs](https://www.npmjs.com/package/bcryptjs)
- **File Uploads & Media Storage**: [Multer](https://github.com/expressjs/multer) + [Cloudinary](https://cloudinary.com/) + [DataURI](https://www.npmjs.com/package/datauri)

---



## 🚀 Getting Started

### Prerequisites
Make sure you have the following installed on your machine:
- [Node.js](https://nodejs.org/) (v16.x or higher recommended)
- [npm](https://www.npmjs.com/) or [yarn](https://yarnpkg.com/)
- A free [MongoDB Atlas](https://www.mongodb.com/atlas) cluster or local MongoDB instance
- A free [Cloudinary](https://cloudinary.com/) account for image and PDF storage

---

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/jobportal.git
cd jobportal
```

---

### 2. Backend Setup

1. Navigate to the backend directory:
   ```bash
   cd backend
   ```

2. Install backend dependencies:
   ```bash
   npm install
   ```

3. Create a `.env` file in the `backend/` root:
   ```env
   MONGO_URI=mongodb+srv://<username>:<password>@cluster0.xxxxx.mongodb.net/jobportal?retryWrites=true&w=majority
   SECRET_KEY=your_super_secret_jwt_key
   CLOUD_NAME=your_cloudinary_cloud_name
   API_KEY=your_cloudinary_api_key
   API_SECRET=your_cloudinary_api_secret
   PORT=8000
   FRONTEND_URL=http://localhost:5173
   ```

4. Start the backend development server:
   ```bash
   npm run dev
   ```
   *The backend server will run on `http://localhost:8000`.*

---

### 3. Frontend Setup

1. Open a new terminal and navigate to the frontend directory:
   ```bash
   cd frontend
   ```

2. Install frontend dependencies:
   ```bash
   npm install
   ```

3. (Optional) Create a `.env` file in the `frontend/` root if pointing to a remote backend:
   ```env
   VITE_BACKEND_URL=http://localhost:8000
   ```

4. Start the Vite development server:
   ```bash
   npm run dev
   ```
   *The frontend client will be accessible at `http://localhost:5173`.*

---

## 🔑 Environment Variables

### Backend (`backend/.env`)

| Variable | Description | Example |
| :--- | :--- | :--- |
| `MONGO_URI` | MongoDB Atlas / Local Connection URI | `mongodb+srv://...` |
| `SECRET_KEY` | Secret token used to sign & verify JWTs | `random_secret_string_123` |
| `CLOUD_NAME` | Cloudinary cloud name | `my_cloud` |
| `API_KEY` | Cloudinary API Key | `1234567890` |
| `API_SECRET` | Cloudinary API Secret | `abcdef12345` |
| `PORT` | Port number for Express server | `8000` |
| `FRONTEND_URL`| Allowed frontend origin for CORS | `http://localhost:5173` |

### Frontend (`frontend/.env`)

| Variable | Description | Default |
| :--- | :--- | :--- |
| `VITE_BACKEND_URL` | Base URL of the backend API | `http://localhost:8000` |

---

## 📡 API Endpoints Overview

### User Routes (`/api/v1/user`)
- `POST /register` - Register a new user (`student` or `recruiter`) with profile picture.
- `POST /login` - User login & issue JWT in cookie.
- `GET /logout` - Clear authentication cookie.
- `POST /profile/update` - Update candidate profile details, bio, skills, and resume.

### Job Routes (`/api/v1/job`)
- `POST /post` - Post a new job *(Recruiter only)*.
- `GET /get` - Get all posted jobs (with search/keyword support).
- `GET /getadminjobs` - Get jobs created by the logged-in recruiter.
- `GET /get/:id` - Get specific job details by ID.

### Company Routes (`/api/v1/company`)
- `POST /register` - Register a new company.
- `GET /get` - Get all companies registered by the logged-in recruiter.
- `GET /get/:id` - Get company details by ID.
- `PUT /update/:id` - Update company information and logo.

### Application Routes (`/api/v1/application`)
- `GET /apply/:id` - Apply for a job by job ID.
- `GET /get` - Get all jobs applied to by the logged-in user.
- `GET /:id/applicants` - Get all applicants for a specific job *(Recruiter only)*.
- `POST /status/:id/update` - Update applicant status (`accepted` / `rejected`).

---

## 📂 Folder Structure

```
jobportal/
├── backend/
│   ├── controllers/          # Business logic (user, company, job, application)
│   ├── middlewares/          # JWT auth & Multer file upload middlewares
│   ├── models/               # Mongoose schemas (User, Company, Job, Application)
│   ├── routes/               # API route definitions
│   ├── utils/                # DB connection & Cloudinary setup
│   ├── .env.example          # Environment variables template
│   ├── index.js              # Express app entry point
│   └── package.json          # Backend dependencies and scripts
│
├── frontend/
│   ├── public/               # Public assets
│   ├── src/
│   │   ├── assets/           # Static images and logos
│   │   ├── components/       # UI components (auth, admin, shared, home, etc.)
│   │   ├── hooks/            # Custom React hooks (job fetchers, etc.)
│   │   ├── redux/            # Redux Toolkit slices and persistent store
│   │   ├── utils/            # Axios API constants and utilities
│   │   ├── App.jsx           # Main route configurations
│   │   ├── main.jsx          # Root React entry point
│   │   └── index.css         # Tailwind & theme stylesheets
│   ├── package.json          # Frontend dependencies and scripts
│   ├── tailwind.config.js    # Tailwind CSS configuration
│   └── vite.config.js        # Vite configuration
│
└── README.md                 # Project documentation
```



## 🤝 Contributing

Contributions, issues, and feature requests are welcome!
1. Fork the project.
2. Create your feature branch (`git checkout -b feature/AmazingFeature`).
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`).
4. Push to the branch (`git push origin feature/AmazingFeature`).
5. Open a Pull Request.

---

## 📄 License

This project is licensed under the [ISC License](file:///d:/FULL%20STACK/project/jobportal/backend/package.json#L13).
