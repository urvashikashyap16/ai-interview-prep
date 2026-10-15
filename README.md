<div align="center">

# 🎯 AI Interview Prep

**Practice technical interviews with AI-generated questions and instant, scored feedback.**

![React Native](https://img.shields.io/badge/React_Native-Expo-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![Node.js](https://img.shields.io/badge/Node.js-Express-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)
![Groq](https://img.shields.io/badge/Groq-LLaMA_3.3_70B-F55036?style=for-the-badge)
![AsyncStorage](https://img.shields.io/badge/Storage-AsyncStorage-7F00FF?style=for-the-badge)

</div>

---

## ✨ What it does

Pick a role or topic and a difficulty, answer 10 questions written on the spot by an LLM, and get a score, strengths and improvement tips for every answer.

- **AI-generated questions** for any role or topic, with quick picks for React, Python, Data Structures, DBMS, Operating Systems and Computer Networks
- **Three difficulty levels**: Easy, Medium, Hard
- **Per-answer evaluation**: a score, written feedback, strengths and what to improve
- **Read-aloud questions** with text-to-speech
- **Session history** saved on the device with AsyncStorage, so no login or database is needed
- **Offline fallback**: a built-in question bank takes over (with a warning banner) if the AI API is unreachable
- **Cross-platform**: one codebase for Android, iOS and the web

---

## 🧱 Architecture

```
┌──────────────────────┐   POST /generate-questions   ┌──────────────────────┐     ┌──────────────┐
│  React Native (Expo) │ ───────────────────────────▶ │  Node.js + Express   │ ──▶ │   Groq API   │
│  Home → Question →   │   POST /evaluate-answer      │  REST backend        │     │ LLaMA 3.3 70B│
│  Feedback → History  │ ◀─────────────────────────── │  (structured JSON)   │ ◀── │              │
└──────────────────────┘                              └──────────────────────┘     └──────────────┘
        │
        └── AsyncStorage (local session history)
```

The backend asks the model for strict JSON so the app can render questions and scores reliably. Evaluation calls are spaced out to stay within the free-tier rate limits, and the app falls back to local questions if a call fails.

---

## 📁 Project structure

```
ai-interview-prep/
├── App.js                   ← Navigation stack (Home, Question, Feedback, History)
├── theme.js                 ← Shared colours and styles
├── screens/
│   ├── HomeScreen.js        ← Role + difficulty picker
│   ├── QuestionScreen.js    ← Answer questions, text-to-speech
│   ├── FeedbackScreen.js    ← Scores and feedback per answer
│   └── HistoryScreen.js     ← Past sessions
├── assets/
└── InterviewPrepBackend/
    ├── server.js            ← Express API + Groq calls
    └── .env.example
```

---

## 🚀 Run it locally

**Prerequisites:** Node.js 18+ and a free Groq API key from [console.groq.com](https://console.groq.com).

**1. Start the backend**

```bash
cd InterviewPrepBackend
npm install
cp .env.example .env        # then paste your GROQ_API_KEY into .env
npm run dev                 # runs on http://localhost:5000
```

**2. Start the app** (in a new terminal, from the project root)

```bash
npm install
npm run web                 # or: npm start, then press a for Android / i for iOS
```

---

## 🔌 API

| Method | Endpoint | Body | Returns |
|---|---|---|---|
| POST | `/generate-questions` | `{ role, difficulty, count }` | List of questions |
| POST | `/evaluate-answer` | `{ question, answer, role, difficulty }` | Score, feedback, strengths, improvements |
| GET | `/` | none | Health check |

---

## 🛣️ Roadmap

- Voice answers with speech-to-text
- Progress charts across sessions
- Cloud sync and user accounts

---

<div align="center">Built by <a href="https://github.com/urvashikashyap16">Urvashi Kashyap</a></div>
