<div align="center">
</div>

# Run and deploy your AI Studio app

This contains everything you need to run your app locally.

View your app in AI Studio: https://ai.studio/apps/ef152a86-144b-42b7-bc68-133c253c7391

## Run Locally

**Prerequisites:**  Node.js


1. Install dependencies:
   `npm install`
2. Set the `GEMINI_API_KEY` in [.env.local](.env.local) to your Gemini API key
3. Run the app:
   `npm run dev`
   # 📸 FaceAttend AI — Smart Facial Recognition Attendance System

[![React](https://img.shields.io/badge/Frontend-React%20%7C%20TypeScript%20%7C%20Tailwind-61DAFB?logo=react&logoColor=black)](https://react.dev/)
[![Firebase](https://img.shields.io/badge/Database-Firebase%20Firestore%20%26%20Auth-FFCA28?logo=firebase&logoColor=black)](https://firebase.google.com/)
[![Google GenAI](https://img.shields.io/badge/AI%20Engine-Gemini%20Vision%20API-4285F4?logo=google&logoColor=white)](https://ai.google.dev/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

An intelligent, cloud-backed facial recognition attendance web application designed for universities, schools, and training institutes. **FaceAttend AI** eliminates roll-calls and proxy attendance by using **Google Gemini Vision multimodal AI** to identify multiple students simultaneously from a single classroom webcam feed or group photo upload.

---

## 🌟 Key Features

- **🎯 Multi-Face AI Recognition:**
  - Identifies multiple students in a single classroom frame with structured JSON schema outputs.
  - Compares live classroom captures against enrolled student reference images in real time (>85% confidence matching).
  - Works with live webcam auto-scanning (every 3 seconds) or manual high-res image uploads.

- **👥 Student Management (Full CRUD):**
  - Register new students with details (Roll Number, Department, Academic Year, Section, Email).
  - In-app face capture using webcam or photo upload with automated center-crop normalization.
  - Edit student details and delete records with safe confirmation dialogs.

- **🏫 Class-Level Filtering & RBAC:**
  - Filter by **Department**, **Year**, and **Section** (e.g., *Computer Science • Year III • Section A*).
  - Isolate attendance logs and statistics so teachers only see relevant students.
  - Role-based permissions for Admins, Teachers/Staff, and Students.
  - Emergency **Demo Mode** for offline evaluation and project review presentations.

- **📊 Dynamic Analytics & Reporting:**
  - Real-time attendance percentage, total present, and total absent counters.
  - Visual charts: Weekly attendance trends, hourly check-in distribution, and top performer metrics.
  - Attendance history table with date picker and search filters.
  - One-click export for attendance reports (CSV / PDF format).

---

## 🛠️ Tech Stack

| Layer | Technologies |
| :--- | :--- |
| **Frontend** | React 19, TypeScript, Tailwind CSS, Lucide Icons, Chart.js / Recharts |
| **Build Tool** | Vite |
| **Backend & Routing** | Express.js (Node.js full-stack mount) |
| **AI / Computer Vision** | Google Gemini Multimodal Vision API (`@google/genai`) |
| **Authentication** | Firebase Authentication (Email/Password & Social OAuth) |
| **Database** | Google Cloud Firestore (Real-time NoSQL) |

---

## 🏗️ Architecture & Workflow

```text
[ 1. Student Enrollment ]
  Teacher selects Class (Dept / Year / Sec)
  └──> Uploads / Captures Student Portrait (Base64 normalized)
       └──> Saved to Firestore (/students)

[ 2. Live Scanning & AI Inference ]
  Teacher launches Live Attendance or Uploads Classroom Photo
  └──> Client prepares multimodal payload:
         • Classroom Frame (JPEG)
         • Reference faces of all class students
         • Strict JSON match instruction prompt
  └──> Sent to Gemini Vision API (Multimodal)
  └──> AI returns array of matched student IDs: ["std_01", "std_04", ...]

[ 3. Attendance Recording ]
  System matches IDs -> Marks "PRESENT" in Firestore (/attendance)
  └──> Live UI and Analytics update instantly
  └──> Teacher can click "Mark Remaining as Absent" to close session
