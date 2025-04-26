🎯 Goal
Create a platform where instructors can host live classes, interact with students, auto-record & transcribe sessions, and generate AI-driven summaries or notes — all in one place.

🧩 Core Features
User Roles: Instructor & Student

Live Classes: Integrated via Zoom SDK

Session Recordings: Auto-record via Zoom API

Transcription: Use Google Speech-to-Text (STT) for audio transcripts

AI Summarization: Use OpenAI to generate study notes from transcripts

Dashboard: For scheduling, joining classes, accessing recordings & summaries

Payments: Instructors can charge students via Stripe

Auth: Google Sign-In or SSO

Notifications: Email or push when summary is ready (using task queue or serverless)

🏗️ Tech Stack
Frontend: React or Next.js

Backend: FastAPI or Node.js (Express)

Database: PostgreSQL (for users, classes, recordings, etc.)

AI: OpenAI API (summaries), Google STT (transcripts)

Payments: Stripe

Auth: OAuth2 (Google Sign-In), Firebase (optional for magic links)

Queue/Async: Celery (Python) or BullMQ (Node.js)

Deployment: GCP (Cloud Run / App Engine), Docker, GitHub Actions

🔄 Flow Breakdown
➤ Instructor creates a class
Class details stored in PostgreSQL

Zoom meeting link generated using Zoom API

➤ Students join via dashboard
Authenticated with Google or magic link

Frontend uses Zoom Web SDK to embed the live session

➤ Class ends
Zoom recording becomes available

Async job fetches the recording → sends audio to Google STT → stores transcript

➤ Transcript sent to OpenAI
Async job sends transcript to GPT → returns summarized notes

Notes saved and displayed on instructor and student dashboards

➤ Optional
Stripe: Students pay to access premium classes

Serverless function: Notifies user when notes are ready

🧠 AI Notes Sample Prompt
plaintext
Copy
Edit
You're a smart teaching assistant. Summarize this class transcript in bullet points with key takeaways, important concepts, and potential quiz questions.
📁 Folder Structure (Backend)
Copy
Edit
/backend
  ├── app/
  │   ├── api/
  │   ├── services/       # Zoom, OpenAI, STT
  │   ├── models/
  │   ├── tasks/          # Async job handlers
  ├── main.py
  ├── requirements.txt
🧪 MVP in 4 Milestones
User auth + dashboard UI

Zoom integration + class scheduling

Recording + transcript + AI summaries

Stripe integration + notifications

