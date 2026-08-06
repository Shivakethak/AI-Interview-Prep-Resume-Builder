# 🎯 AI-Powered Interview Preparation & Resume Builder Platform

An end-to-end, full-stack career acceleration platform built with **React 19, Node.js, Express, MongoDB, and Google Gemini AI**. 

The platform evaluates candidate profiles against specific Job Descriptions (JDs), calculates match scores, surfaces severity-graded skill gaps, delivers tailored technical & behavioral interview preparation plans, and automatically builds downloadable, ATS-optimized PDF resumes using **Puppeteer**.

---

## ✨ Features

- **📄 Resume & Job Match Analysis**: Parses candidate resumes (PDF format) and evaluates fit against any targeted Job Description.
- **📊 AI Match Score & Skill Gap Analysis**: Uses Google Gemini AI with Zod structured JSON schemas to compute a 0-100% match score and highlight skill gaps by severity (*Low, Medium, High*).
- **💡 Targeted Interview Questions & Answers**: Generates role-specific technical and behavioral questions, complete with the interviewer's intention and strategic answer guidance.
- **📅 Day-by-Day Preparation Roadmap**: Creates a structured daily preparation timeline to help candidates systematically bridge identified skill gaps before interview day.
- **📝 ATS-Optimized Resume Generator**: Crafts a customized HTML resume tailored for the job role and dynamically converts it into a downloadable A4 PDF via Puppeteer.
- **🔐 Secure User Authentication**: Full user login/registration system powered by **JWT (HTTP-only cookies)**, **bcrypt password hashing**, and token blacklisting.
- **📂 In-Memory PDF Upload Pipeline**: Uses **Multer** (in-memory storage) and `pdf-parse` for fast, secure resume text extraction without saving files to disk.

---

## 🛠️ Tech Stack

### **Frontend**
- **Framework**: React 19 + Vite
- **Routing**: React Router v7
- **Styling**: SCSS / Sass
- **HTTP Client**: Axios (with credentials for HTTP-only cookies)
- **State Management**: React Context API

### **Backend**
- **Runtime & Framework**: Node.js, Express.js 5
- **Database**: MongoDB (Mongoose ORM)
- **Authentication**: JSON Web Tokens (JWT), Cookie-Parser, bcryptjs
- **AI Integration**: `@google/genai` (Google Gemini API) with `zod` and `zod-to-json-schema`
- **Document Processing**: `pdf-parse` (resume parsing), `multer` (file upload), `puppeteer` (PDF generation)

---

## 📁 Project Structure

```text
interview-ai-yt-main/
├── Backend/
│   ├── server.js              # Server entry point
│   └── src/
│       ├── app.js             # Express app setup & CORS configuration
│       ├── config/            # Database connection setup
│       ├── controllers/       # Auth & Interview route controllers
│       ├── middlewares/       # Auth & Multer file upload middlewares
│       ├── models/            # User, Blacklist, and InterviewReport Mongoose schemas
│       ├── routes/            # Express API routes
│       └── services/          # Gemini AI API & Puppeteer PDF services
│
└── Frontend/
    ├── index.html             # Main HTML file
    ├── vite.config.js         # Vite configuration
    └── src/
        ├── App.jsx            # Main app router component
        ├── app.routes.jsx     # Route definitions
        └── features/          # Modular feature components (auth & interview)
```

---

## 🚀 Getting Started

### Prerequisites

Ensure you have the following installed:
- [Node.js](https://nodejs.org/) (v18 or higher)
- [MongoDB](https://www.mongodb.com/) (Local instance or MongoDB Atlas URI)
- [Google Gemini API Key](https://aistudio.google.com/)

---

### 1. Backend Setup

1. Navigate to the `Backend` directory:
   ```bash
   cd Backend
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Create a `.env` file in the `Backend` directory with the following environment variables:
   ```env
   PORT=3000
   MONGO_URI=mongodb://localhost:27017/interview-ai
   JWT_SECRET=your_super_secret_jwt_key
   GOOGLE_GENAI_API_KEY=your_google_gemini_api_key
   ```

4. Start the backend development server:
   ```bash
   npm run dev
   ```
   *Server will run at `http://localhost:3000`*

---

### 2. Frontend Setup

1. Navigate to the `Frontend` directory:
   ```bash
   cd Frontend
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Start the Vite development server:
   ```bash
   npm run dev
   ```
   *Frontend will run at `http://localhost:5173`*

---

## 🔌 API Endpoints Summary

### **Authentication Routes** (`/api/auth`)
| Method | Endpoint | Description | Access |
|---|---|---|---|
| `POST` | `/register` | Register a new user | Public |
| `POST` | `/login` | User login (returns HTTP-only JWT cookie) | Public |
| `GET` | `/logout` | Logout user & blacklist JWT token | Public |
| `GET` | `/get-me` | Get current logged-in user profile | Private |

### **Interview & Resume Routes** (`/api/interview`)
| Method | Endpoint | Description | Access |
|---|---|---|---|
| `POST` | `/` | Upload resume PDF + Job Description to generate AI Report | Private |
| `GET` | `/` | Get all interview reports of logged-in user | Private |
| `GET` | `/report/:interviewId` | Get detailed interview report by ID | Private |
| `POST` | `/resume/pdf/:interviewReportId` | Generate & download job-tailored ATS PDF Resume | Private |

---

## 🛡️ License

This project is open-source and available under the [ISC License](LICENSE).
