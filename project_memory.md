# Project Memory — V University

This file is a **persistent blueprint + guardrail** for the AI University project ("V University"). Its purpose is to:

1. Keep the **goal, architecture, and APIs** in memory for Cursor or any dev tool.
2. Prevent accidental deletion/alteration of working code.
3. Enforce a **backup & rollback strategy** inside the project directory.

---

## 🎯 Goal of V University

Build a **modular, enterprise-grade AI University app** where:

* A user can **prompt any subject + grade level** → app generates a professional-quality course instantly.
* App also provides **pre-generated school-style curricula (by grade)**.
* A **default AI tutor avatar** teaches lessons. Users can **switch avatars** (choose from library, upload image, or use real-looking avatar APIs).
* Lessons include **slides, diagrams, images, animations, interactive widgets, quizzes**.
* Supports **adaptive learning**: mastery tracking, growth charts, certifications.
* Includes **optional classrooms** with multiple students: chat, voice, video, raise-hand, polls, whiteboard.
* Students can graduate virtually with **certificates + transcripts**.
* Entire app is **plug-and-play modular** → new features can be added without rewriting core.

---

## 🏗️ Architecture Principles

* **Modular APIs**: Each feature = isolated service (Auth, Courses, Tutor, Classroom, etc.).
* **Provider Gateway**: Wrap all external APIs behind internal endpoints (e.g., `/api/tutor`), so swapping providers is easy.
* **Open Source First**: Default to open/self-hosted tools (LLaMA, Whisper, Coqui TTS, Wav2Lip, Supabase, LiveKit, Blockcerts).
* **Serverless + Scalable**: Use serverless functions for light tasks, GPU pods (RunPod) for heavy AI jobs.
* **Asynchronous & Cached**: Heavy processes run async with caching to avoid lag.
* **Enterprise Ready**: Multi-tenant, RBAC, secure, observable, with audit logs.

---

## 📦 Core Components & APIs

### Core APIs (owned)

* **Auth & User API** → login, roles (student/teacher/admin/parent).
* **Course API** → prompt-to-course generation, CRUD for courses/lessons.
* **Lesson Content API** → slides, images, interactive widgets (H5P, Lottie).
* **Assessment API** → quizzes, adaptive questions, scoring.
* **Tutor Avatar API** → manage avatar selection, rendering, voice sync.
* **Progress & Transcript API** → mastery, growth charts, certificates.
* **Classroom API** → live rooms, chat, raise hand, video/audio (LiveKit).
* **Notification API** → email, SMS, push reminders.
* **Analytics API** → engagement, dashboards, at-risk detection.
* **Payments API** → subscriptions, bundles, school orgs.

### External / Pluggable APIs

* **LLM (Courses, Q&A)** → LLaMA 3 (RunPod), OpenAI, Gemini, Anthropic.
* **TTS (Tutor voice)** → Coqui TTS, Piper (open source).
* **STT (Student voice)** → Whisper (open source).
* **Avatar / Talking Face** → Wav2Lip, SadTalker, MuseTalk (open source), HeyGen/D-ID (paid fallback).
* **Vector DB** → pgvector (Postgres/Supabase), Qdrant.
* **Realtime** → LiveKit self-host.
* **Interactive Widgets** → H5P, Lottie.
* **Certificates** → Blockcerts.
* **Payments** → Stripe, Razorpay.
* **Search/Recommendation** → OpenSearch, Typesense.

---

## 💾 Database & Hosting

* **Database**: Supabase (Postgres + pgvector + Auth + storage).
* **Frontend Hosting**: Netlify or Vercel (React/Next.js PWA).
* **Backend Hosting**: Netlify/Vercel functions (light), RunPod (AI heavy jobs).
* **Realtime**: LiveKit self-hosted VM/container.
* **Storage**: Supabase storage or S3-compatible bucket (media).

---

## 💸 Cost Strategy

* Supabase free tier → then $25/mo.
* RunPod GPUs → $20–50/mo (on demand).
* Netlify/Vercel frontend → free or <$20.
* LiveKit self-host → $10 VM.
* Payments → Stripe/Razorpay % cut only.
* Total MVP cost: ~$50–100/mo.

---

## 🔄 Backup & Rollback Rules

1. **No file deletions by AI agent** unless explicitly requested by dev.
2. **Working code never overwritten**: mark stable code with comments like `# DO NOT MODIFY BELOW`.
3. **Regular backups**: create `/backups/` folder inside project.

   * Example: `backups/backup-YYYYMMDD-HHMM.zip`
   * Taken before major refactors or new features.
4. **Rollback ready**: Keep last 3 backups in rotation.

---

## 🗂️ Development Workflow

* Monorepo with modular services (packages per API).
* Use pnpm workspaces for clean boundaries.
* Feature flags for experiments.
* Storybook for interactive components.
* CI/CD: GitHub Actions + Netlify/Vercel + RunPod jobs.

---

## 📌 Current Status

* ✅ High-level architecture defined
* ✅ Core + external APIs mapped
* ✅ Hosting & DB strategy chosen (Supabase + RunPod + Netlify/Vercel)
* 🔜 Next step: Flowchart breakdowns per API (Course API, Tutor Avatar API, etc.)
* 🔜 Cursor guardrails: ensure project_memory.md is always referenced before edits.

---

⚡ **Reminder for Cursor / Agents**:
Always consult this file before making changes.
Never delete working code.
Always create a backup in `/backups/` before large modifications.

