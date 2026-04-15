# Chatify — Real-Time Full-Stack Chat Application

![Demo App](/frontend/public/screenshot-for-readme.png)

WEChat is a real-time messaging application I built to practice and demonstrate full-stack product development: authentication, socket communication, media handling, and production-style integrations like email, rate-limiting, and cloud storage.

---

## Why I Built This

I wanted one project that combines:

- secure auth (JWT + protected routes),
- real-time communication (Socket.io),
- practical backend integrations (Resend, Cloudinary, Arcjet),
- and a clean modern frontend (React + Tailwind + Zustand).

The goal was not just “chat messages working”, but building a project with features and constraints similar to real products.

---

## Core Features

- JWT-based signup/login (no external auth provider)
- Real-time 1:1 messaging via Socket.io
- Online/offline user presence indicators
- Image sharing in chat (Cloudinary upload)
- Welcome email on signup (Resend)
- API protection and rate limiting (Arcjet)
- Sound effects for typing/notifications (toggle-able UX)
- Responsive UI with React, Tailwind CSS, DaisyUI
- Zustand-based state management

---

## Tech Stack

### Frontend
- React
- Vite
- Tailwind CSS + DaisyUI
- Zustand
- Axios
- Socket.io client

### Backend
- Node.js
- Express
- MongoDB + Mongoose
- Socket.io
- JWT
- Resend
- Cloudinary
- Arcjet

---

## High-Level Architecture

1. **Client (React)** handles auth state, chat state, and message rendering.
2. **REST API (Express)** manages auth, user, and message-related operations.
3. **Socket Layer** handles real-time message delivery and presence updates.
4. **MongoDB** stores users and messages.
5. **External Services**
   - Resend for transactional email
   - Cloudinary for image storage
   - Arcjet for request protection/rate limiting

---

## Project Structure

```bash
chatify/
  backend/
    src/
      controllers/
      routes/
      models/
      middleware/
      lib/
  frontend/
    src/
      components/
      pages/
      store/
      lib/
```

---

## Environment Variables (`backend/.env`)

Create a `.env` file inside `backend/`:

```bash
PORT=3000
MONGO_URI=your_mongo_uri_here

NODE_ENV=development
JWT_SECRET=your_jwt_secret

RESEND_API_KEY=your_resend_api_key
EMAIL_FROM=your_email_from_address
EMAIL_FROM_NAME=your_email_from_name

CLIENT_URL=http://localhost:5173

CLOUDINARY_CLOUD_NAME=your_cloudinary_cloud_name
CLOUDINARY_API_KEY=your_cloudinary_api_key
CLOUDINARY_API_SECRET=your_cloudinary_api_secret

ARCJET_KEY=your_arcjet_key
ARCJET_ENV=development
```

### Important Notes
- `RESEND_API_KEY` is mandatory if welcome emails are enabled.
- Keep `.env` private and never commit secrets.
- Ensure `CLIENT_URL` matches your frontend dev URL.

---

## How to Run Locally

Use two terminals.

### Terminal 1 — Backend

```bash
cd backend
npm install
npm run dev
```

### Terminal 2 — Frontend

```bash
cd frontend
npm install
npm run dev
```

Frontend default URL: `http://localhost:5173`  
Backend default URL: `http://localhost:3000`

---

## API Overview (Major Routes)

> Exact route prefixes may be defined in `backend/src/server.js` route mounting.

| Area | Purpose |
|------|---------|
| Auth Routes | Signup, login, auth checks, user session flow |
| Message Routes | Send/fetch messages, media message support |
| Socket Events | Real-time incoming message + presence updates |

For route-level details, check:
- `backend/src/routes/auth.route.js`
- `backend/src/routes/message.route.js`

---

## Troubleshooting

### 1) `'vite' is not recognized`
Install frontend dependencies first:

```bash
cd frontend
npm install
npm run dev
```

### 2) `Missing API key. Pass it to the constructor new Resend(...)`
This means `RESEND_API_KEY` is missing or unreadable.

Checklist:
- `.env` exists inside `backend/`
- `RESEND_API_KEY` is present
- backend restarted after `.env` changes

### 3) Backend crashes on startup
Verify all required env vars are set (`MONGO_URI`, `JWT_SECRET`, cloud/email keys if related features are active).

---

## Development Workflow I Follow

- Work on feature/fix branches
- Keep commits focused and small
- Test critical paths locally before pushing
- Open PRs with clear description and screenshots when UI changes are included

---

## What I Learned Building This

- Managing state and sockets together needs careful lifecycle handling.
- Real-time UX is more than message delivery (presence, sounds, loading states).
- External integrations should fail gracefully and not crash unrelated app flows.
- Good README and setup docs save a lot of debugging time.

---

## Known Limitations / Next Improvements

- Add message delivery/read receipts
- Add group chat support
- Improve test coverage (API + component tests)
- Add Docker for one-command local setup
- Add CI checks (lint + tests) on PR

---

## Optional: Push This Clone to Your Own GitHub

If this repo was cloned from someone else and you want your own copy:

```bash
git remote -v
git remote set-url origin https://github.com/<your-username>/<your-repo>.git
git add .
git commit -m "Customize README and project setup"
git push -u origin main
```

(Use `master` if your default branch is `master`.)

---

## Disclaimer

This project is for learning and portfolio demonstration.  
If you fork or reuse it, customize features, naming, and documentation to reflect your own implementation and understanding.
