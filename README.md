# 🧠 QuizMind AI - AI-Powered Quiz Generator Web Application

An end-to-end full-stack AI Quiz Generation web application built for internship project presentation. Built with **React**, **Tailwind CSS**, **Node.js/Express**, and **MongoDB**, featuring Google Gemini AI integration with a built-in intelligent offline mock engine.

---

## ✨ Key Features

1. **Modern & Responsive UI**:
   - Built with **React + Vite** and styled with **Tailwind CSS**.
   - Sleek glassmorphism visual design, responsive on mobile, tablet, and desktop.
   - Smooth **Dark / Light mode** toggle with persistent user preference.

2. **AI-Powered Quiz Generation**:
   - Customizable Parameters:
     - **Topic / Subject**: Any custom topic (e.g., JavaScript, React, Machine Learning, World History, Quantum Physics).
     - **Number of Questions**: 5, 10, 15, or 20 questions.
     - **Difficulty Level**: Easy, Medium, or Hard.
     - **Question Format**: Multiple Choice (4 choices) or True/False.
   - Powered by Google Gemini AI API with dynamic prompt engineering.
   - **Built-in Mock AI Fallback**: If no API key is provided, the application automatically activates a realistic Mock AI generator so the project runs seamlessly offline.

3. **Interactive Quiz Experience**:
   - Live timer stopwatch & question progress bar.
   - Question pill navigation to quickly jump between questions.
   - Clean option selection with instant visual feedback and clear answer option.
   - Submission confirmation modal.

4. **Instant Evaluation & Detailed Explanations**:
   - Score calculation, percentage, and confetti celebration for passing scores (≥60%).
   - Metrics breakdown: Total questions, correct count, incorrect count, time spent.
   - **Step-by-step Question Review**: Compares user's selected answer with the correct answer and provides an **AI explanation** for every question.
   - Shareable score summary generator.

5. **User Dashboard & Analytics**:
   - Performance overview: Total quizzes taken, average score percentage, highest score, top practiced topic.
   - Complete quiz attempt history with search & filter functionality.
   - Retake previous quizzes or review detailed explanations at any time.

6. **Authentication & Security**:
   - User registration and login with bcrypt password hashing and JWT tokens.
   - One-click **Guest / Demo Login** for instant demonstration during evaluation.
   - Secure server-side AI API key handling (`.env`), never exposed to frontend code.

7. **Database Storage with Resilient Fallback**:
   - MongoDB schemas for Users, Quizzes, and Attempts using Mongoose.
   - Memory fallback layer that ensures full functionality even if local MongoDB service is offline.

---

## 🛠️ Technology Stack

- **Frontend**: React 18, Vite, Tailwind CSS, Lucide React Icons, React Router v6, Canvas Confetti
- **Backend**: Node.js, Express.js, CORS, Dotenv, JSON Web Tokens (JWT), BcryptJS
- **Database**: MongoDB & Mongoose (with automated in-memory storage fallback)
- **AI Integration**: Google Gemini API (`gemini-1.5-flash`) + Built-in Mock AI Engine

---

## 📁 Project Structure

```
ai-quiz-generator/
├── package.json              # Root orchestrator scripts
├── README.md                 # Project documentation
├── server/                   # Backend API (Node.js & Express)
│   ├── package.json
│   ├── .env.example
│   ├── .env
│   ├── server.js             # Express app entry point
│   ├── config/
│   │   └── db.js             # Database connection & fallback
│   ├── models/
│   │   ├── User.js           # Mongoose User model
│   │   ├── Quiz.js           # Mongoose Quiz model
│   │   ├── Attempt.js        # Mongoose Attempt model
│   │   └── storage.js        # Hybrid storage layer (MongoDB + Memory)
│   ├── routes/
│   │   ├── authRoutes.js     # Register, Login, Me endpoints
│   │   ├── quizRoutes.js     # Generate, List, Get Quiz endpoints
│   │   └── attemptRoutes.js  # Submit, Grade, History endpoints
│   ├── middleware/
│   │   └── auth.js           # JWT authentication middleware
│   └── services/
│       ├── aiService.js       # Google Gemini AI integration
│       └── mockQuizService.js # High-quality offline Mock AI generator
└── client/                   # Frontend SPA (React + Tailwind CSS)
    ├── package.json
    ├── vite.config.js
    ├── tailwind.config.js
    ├── postcss.config.js
    ├── index.html
    └── src/
        ├── App.jsx           # Main router
        ├── main.jsx          # Root render
        ├── index.css         # Tailwind & custom CSS
        ├── context/
        │   ├── AuthContext.jsx   # Auth state & user session
        │   └── ThemeContext.jsx  # Dark/Light mode state
        ├── services/
        │   └── api.js        # Centralized API service client
        ├── components/
        │   ├── Navbar.jsx    # Top navigation & theme toggle
        │   └── Footer.jsx    # Footer
        └── pages/
            ├── Home.jsx         # Landing page & quick starter pills
            ├── GenerateQuiz.jsx # Quiz configuration form
            ├── TakeQuiz.jsx     # Live quiz taking interface
            ├── QuizResult.jsx   # Results, score, explanations & review
            ├── Dashboard.jsx    # User statistics & attempt history
            ├── Login.jsx        # Login page with demo guest pass
            └── Register.jsx     # User registration
```

---

## 🚀 Getting Started

### 1. Prerequisites
Ensure you have **Node.js** (v18 or higher) installed on your system.
*(Optional)* **MongoDB** installed locally or MongoDB Atlas connection URI.

### 2. Install Dependencies

You can install dependencies for both frontend and backend using the root command or individually:

```bash
# Option A: Install root and both subprojects
npm run install:all

# Option B: Or install individually
cd server
npm install
cd ../client
npm install
```

---

### 3. Environment Configuration

Backend configuration file is located at `server/.env`:

```env
PORT=5000
MONGODB_URI=mongodb://127.0.0.1:27017/ai-quiz-generator
JWT_SECRET=supersecretjwtkey_aiquiz_internship_2026_dev

# (Optional) Google Gemini API Key
# If left blank, the application will seamlessly use the Built-in Mock AI Engine!
GEMINI_API_KEY=
```

---

### 4. Running the Application

You can start both backend and frontend together or in separate terminals:

#### Method A: Run Both Together (Recommended)
From the root project directory:
```bash
npm run dev
```

#### Method B: Run In Separate Terminals

**Terminal 1 (Backend Server):**
```bash
cd server
npm start
```
*Backend runs on `http://localhost:5000`*

**Terminal 2 (Frontend Client):**
```bash
cd client
npm run dev
```
*Frontend runs on `http://localhost:3000` (or `http://localhost:5173`)*

---

## 🌐 API Endpoints Reference

| Method | Endpoint | Description | Auth |
|---|---|---|---|
| `POST` | `/api/auth/register` | Register new user | Public |
| `POST` | `/api/auth/login` | Login user & get JWT token | Public |
| `GET` | `/api/auth/me` | Get current user profile | Required |
| `POST` | `/api/quiz/generate` | Generate AI quiz (Topic, Diff, Type, Qty) | Optional |
| `GET` | `/api/quiz/:id` | Fetch specific quiz by ID | Public |
| `POST` | `/api/attempts/submit` | Submit answers & get instant grading + reasoning | Optional |
| `GET` | `/api/attempts/user` | Get quiz attempt history & aggregated analytics | Optional |
| `DELETE`| `/api/attempts/:id` | Delete attempt from history | Optional |

---

## 🎓 Demo / Evaluation Tips

- **Quick Topic Testing**: Click any popular topic pill on the Home page (e.g., *JavaScript*, *React*, *Machine Learning*) to auto-fill the generator.
- **Offline Mock Demonstration**: Leave `GEMINI_API_KEY` empty in `server/.env` to showcase the intelligent Mock AI generation logic.
- **Instant Guest Login**: On the Login screen, click **"Continue as Guest Demo User"** to immediately test user-specific dashboard features without manual registration.
