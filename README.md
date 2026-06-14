# ExamShield 🛡️

> Secure online examination platform with real-time webcam proctoring, automated evaluation, and detailed analytics.

**Live Demo:** https://exam-platform-phi-coral.vercel.app  
**Backend API:** https://exam-platform-server-m38q.onrender.com

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | React.js + Vite |
| Backend | Node.js + Express |
| Database | PostgreSQL (Supabase) |
| Real-time | Socket.IO + WebRTC |
| Auth | JWT (JSON Web Tokens) |
| Deployment | Vercel (Frontend) + Render (Backend) |

---

## Features

### ✅ Working Features

**Authentication**
- Role-based login — Admin (Teacher) and Candidate (Student)
- JWT-based secure authentication
- Register and login with name, email, password

**Admin Panel**
- Create and manage exams (title, duration, passing criteria)
- Question bank — add MCQ questions with 4 options and correct answer
- Assign questions to exams
- View all exams and manage them

**Candidate Panel**
- View available exams
- Take timed exams with countdown timer
- Auto-submit when time runs out
- Tab-switch violation detection — logs every time candidate switches tab
- Webcam snapshot captured every 30 seconds and logged as violation record

**Exam Flow**
- MCQ-based questions
- Answers recorded in real-time
- Automated evaluation on submission
- Instant result — Score (%), correct count, Pass/Fail status

**Proctoring Dashboard (Admin)**
- Live candidate list visible when candidates join exam room
- Socket.IO based real-time candidate tracking
- Violation logs stored in database (tab switches + webcam snapshots)

**Database**
- 8 tables: users, exams, questions, exam_questions, attempts, answers, results, violations
- All data stored on Supabase PostgreSQL (Mumbai region)

---

### ⚠️ Known Limitations

**WebRTC Live Video Feed**
- Candidate card shows "Connecting..." on proctor dashboard
- WebRTC peer-to-peer video requires a TURN server for production environments
- TURN servers are paid services (e.g., Twilio, Metered.ca)
- Locally (same network), WebRTC works without TURN server
- Current setup uses Google's free STUN server (`stun:stun.l.google.com:19302`) which only works for direct peer connections, not across NAT/firewalls in production

**Render Free Tier**
- Backend spins down after inactivity — first request may take 30-50 seconds
- This also affects Socket.IO WebSocket stability

---

## Project Structure

```
exam-platform/
├── client/                  # React + Vite Frontend
│   ├── src/
│   │   ├── components/
│   │   │   ├── admin/
│   │   │   │   ├── CreateExam.jsx
│   │   │   │   ├── QuestionBank.jsx
│   │   │   │   └── ProctorDashboard.jsx
│   │   │   ├── auth/
│   │   │   │   ├── Login.jsx
│   │   │   │   └── Register.jsx
│   │   │   └── shared/
│   │   │       ├── Navbar.jsx
│   │   │       └── ProtectedRoute.jsx
│   │   ├── pages/
│   │   │   ├── AdminDashboard.jsx
│   │   │   ├── CandidateDashboard.jsx
│   │   │   └── ExamPage.jsx
│   │   ├── context/
│   │   └── App.jsx
│   └── index.html
│
└── server/                  # Node.js + Express Backend
    ├── controllers/
    │   ├── auth.controller.js
    │   ├── exam.controller.js
    │   └── result.controller.js
    ├── middleware/
    │   └── auth.js
    ├── routes/
    ├── db.js
    └── index.js
```

---

## Environment Variables

**Backend (`server/.env`)**
```
PORT=10000
DATABASE_URL=your_supabase_connection_string
JWT_SECRET=your_jwt_secret
CLIENT_URL=https://exam-platform-phi-coral.vercel.app
```

**Frontend (`client/.env`)**
```
VITE_API_URL=https://exam-platform-server-m38q.onrender.com
```

---

## Database Schema

| Table | Description |
|-------|-------------|
| users | Admin and Candidate accounts |
| exams | Exam details — title, duration, passing % |
| questions | Question bank with options and correct answer |
| exam_questions | Maps questions to exams |
| attempts | Candidate exam attempt records |
| answers | Candidate answers per attempt |
| results | Final score, percentage, pass/fail |
| violations | Tab switches and webcam snapshots |

---

## How to Run Locally

```bash
# Clone the repo
git clone https://github.com/ayushi-0820/exam-platform.git
cd exam-platform

# Backend
cd server
npm install
# Create .env file with your variables
node index.js

# Frontend (new terminal)
cd client
npm install
npm run dev
```

---

## Deployment

| Service | Platform | URL |
|---------|----------|-----|
| Frontend | Vercel | https://exam-platform-phi-coral.vercel.app |
| Backend | Render | https://exam-platform-server-m38q.onrender.com |
| Database | Supabase | PostgreSQL — ap-south-1 (Mumbai) |

---

## Future Improvements

- TURN server integration for WebRTC live video in production
- Invite code / exam code system for controlled access
- Email notifications for exam results
- Mobile responsive UI
- Question import via CSV
- Result analytics with charts

---

## Developer

**Ayushi Kumari**  
GitHub: [@ayushi-0820](https://github.com/ayushi-0820)  
LinkedIn: [linkedin.com/in/ayushi0806](https://linkedin.com/in/ayushi0806)

*Built as part of internship at Codec Technologies*
