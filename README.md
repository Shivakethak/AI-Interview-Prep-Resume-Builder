# 🎯 InterviewPrep AI - Smart Interview Preparation & Resume Builder

[![React 19](https://img.shields.io/badge/React-19.0-61DAFB?style=for-the-badge&logo=react)](https://react.dev/)
[![Node.js](https://img.shields.io/badge/Node.js-v18+-339933?style=for-the-badge&logo=node.js)](https://nodejs.org/)
[![Express](https://img.shields.io/badge/Express-5.0-000000?style=for-the-badge&logo=express)](https://expressjs.com/)
[![MongoDB](https://img.shields.io/badge/MongoDB-Mongoose-47A248?style=for-the-badge&logo=mongodb)](https://www.mongodb.com/)
[![Google Gemini](https://img.shields.io/badge/Google%20Gemini-AI-8E75B2?style=for-the-badge&logo=google)](https://deepmind.google/technologies/gemini/)
[![Vite](https://img.shields.io/badge/Vite-7.3-646CFF?style=for-the-badge&logo=vite)](https://vitejs.dev/)

An intelligent full-stack AI platform built to analyze candidate profiles against specific job descriptions, calculate match scores, identify severity-graded skill gaps, generate tailored interview Q&A guides with personalized preparation roadmaps, and automatically construct ATS-friendly downloadable PDF resumes.

---

## ✨ Key Features

- **📄 AI Profile & Resume Parsing**: Ingests candidate PDF resumes and self-descriptions alongside targeted Job Descriptions using server-side PDF parsing (`pdf-parse`).
- **📊 Role Match Score & Gap Analysis**: Computes an accurate match score (0–100%) and categorizes missing skills by severity (*Low, Medium, High*).
- **💡 Tailored Technical & Behavioral Q&A**: Generates role-specific technical and behavioral questions along with the interviewer's intent and strategic guidelines on how to answer.
- **📅 Day-by-Day Preparation Roadmap**: Provides a structured, customized study plan broken down by day, focus areas, and actionable tasks.
- **📄 ATS-Compliant PDF Resume Builder**: Uses Google Gemini AI to craft job-optimized HTML resume templates and **Puppeteer** to dynamically stream downloadable A4 PDFs.
- **🔒 Secure Authentication & Data Persistence**: Implements JWT authentication with HTTP-only cookies, password hashing with `bcryptjs`, token blacklisting, and user dashboard history in MongoDB.

---

## 🛠️ Tech Stack

### **Frontend**
- **Framework**: React 19 + Vite
- **Routing**: React Router v7
- **Styling**: Sass / SCSS
- **State & HTTP**: React Context API, Axios

### **Backend**
- **Runtime**: Node.js & Express 5
- **Database**: MongoDB with Mongoose ORM
- **Authentication**: JWT (JSON Web Tokens), `bcryptjs`, Cookie Parser
- **File Upload**: Multer (In-memory storage, 3MB limit)
- **PDF Generation & Parsing**: Puppeteer, `pdf-parse`

### **AI & Data Validation**
- **LLM**: Google Gemini API (`@google/genai` / `gemini-3-flash-preview`)
- **Schema Validation**: Zod + `zod-to-json-schema` (Ensures 100% structured JSON responses without free-text LLM variance)

---

## 📁 Project Structure

```text
interview-ai-yt-main/
├── Backend/
│   ├── server.js                   # Application entry point
│   ├── src/
│   │   ├── app.js                  # Express app setup & middleware
│   │   ├── config/
│   │   │   └── database.js         # MongoDB connection config
│   │   ├── controllers/
│   │   │   ├── auth.controller.js  # Register, Login, Logout, Profile
│   │   │   └── interview.controller.js # Report & PDF resume controllers
│   │   ├── middlewares/
│   │   │   ├── auth.middleware.js  # JWT authentication & route protection
│   │   │   └── file.middleware.js  # Multer configuration for PDF uploads
│   │   ├── models/
│   │   │   ├── user.model.js       # User schema
│   │   │   ├── blacklist.model.js  # Invalidated tokens schema
│   │   │   └── interviewReport.model.js # Interview report & analysis schema
│   │   ├── routes/
│   │   │   ├── auth.routes.js      # Auth API endpoints
│   │   │   └── interview.routes.js # Interview & Resume API endpoints
│   │   └── services/
│   │       └── ai.service.js       # Gemini AI integration & Puppeteer PDF generator
│   └── package.json
│
└── Frontend/
    ├── index.html
    ├── vite.config.js
    ├── src/
    │   ├── App.jsx
    │   ├── app.routes.jsx          # Route definitions
    │   ├── main.jsx                # App bootstrap
    │   └── features/
    │       ├── auth/               # Login & Register components, hooks, context
    │       └── interview/          # Home, Interview Report dashboard, PDF generator
    └── package.json
```

---

## 🚀 Getting Started

### **Prerequisites**
- **Node.js** (v18 or higher)
- **MongoDB** (Local instance or MongoDB Atlas cluster)
- **Google Gemini API Key** (Obtain from [Google AI Studio](https://aistudio.google.com/))

---

### **1. Backend Setup**

1. Navigate to the `Backend` directory:
   ```bash
   cd Backend
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Create a `.env` file in the `Backend` root directory and configure the environment variables:
   ```env
   PORT=3000
   MONGODB_URI=mongodb://localhost:27017/interview_ai
   JWT_SECRET=your_super_secret_jwt_key
   GOOGLE_GENAI_API_KEY=your_google_gemini_api_key
   ```

4. Start the backend development server:
   ```bash
   npm run dev
   ```
   The backend server will run on `http://localhost:3000`.

---

### **2. Frontend Setup**

1. Navigate to the `Frontend` directory:
   ```bash
   cd Frontend
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Start the frontend Vite development server:
   ```bash
   npm run dev
   ```
   Open `http://localhost:5173` in your browser.

---

## 🔌 API Reference

### **Authentication Endpoints (`/api/auth`)**
| Method | Endpoint | Description | Auth Required |
| :--- | :--- | :--- | :--- |
| `POST` | `/api/auth/register` | Register a new user account | ❌ No |
| `POST` | `/api/auth/login` | Login user & issue HTTP-only cookie JWT | ❌ No |
| `POST` | `/api/auth/logout` | Logout user & invalidate token | 🔒 Yes |
| `GET` | `/api/auth/profile` | Fetch authenticated user profile | 🔒 Yes |

### **Interview & Resume Endpoints (`/api/interview`)**
| Method | Endpoint | Description | Auth Required |
| :--- | :--- | :--- | :--- |
| `POST` | `/api/interview/` | Upload resume PDF, self-description & JD to generate AI report | 🔒 Yes |
| `GET` | `/api/interview/` | Fetch all historical interview reports of logged-in user | 🔒 Yes |
| `GET` | `/api/interview/report/:interviewId` | Get detailed interview report by ID | 🔒 Yes |
| `POST` | `/api/interview/resume/pdf/:interviewReportId` | Generate & download job-tailored ATS PDF resume | 🔒 Yes |

---

## 🛡️ License

Distributed under the ISC License. See `LICENSE` for more details.
