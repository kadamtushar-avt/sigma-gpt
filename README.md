# SigmaGPT

SigmaGPT is a small MERN-style chat application that integrates OpenAI's Chat API to provide assistant replies and stores conversation threads in MongoDB.

## Overview
- Backend: Express server exposing REST endpoints for chat and thread management; saves conversation threads in MongoDB.
- Frontend: React (Vite) single-page app that provides a chat UI, thread list, and message rendering (supports markdown/code highlighting).

## Tech stack
- Node.js + Express
- MongoDB + Mongoose
- OpenAI Chat API (via fetch in backend)
- React + Vite on the frontend

## Project structure (important files)
- Backend: [Backend/server.js](Backend/server.js#L1) — Express app; [Backend/routes/chat.js](Backend/routes/chat.js#L1) — API routes; [Backend/utils/openai.js](Backend/utils/openai.js#L1) — OpenAI call helper
- Frontend: [Frontend/src/App.jsx](Frontend/src/App.jsx#L1) — main app; [Frontend/src/Chat.jsx](Frontend/src/Chat.jsx#L1) — chat UI; [Frontend/src/MyContext.jsx](Frontend/src/MyContext.jsx#L1)

## Environment variables
- `OPENAI_API_KEY` — required to call OpenAI API
- `MONGODB_URI` — MongoDB connection string

Set these in a `.env` file in the `Backend/` folder (or export them in your environment). The backend reads them via `dotenv`.

## Run locally

1. Backend

```bash
cd Backend
npm install
# create .env with OPENAI_API_KEY and MONGODB_URI
npm run dev # or `node server.js` (package.json includes dependencies; use nodemon if installed)
```

The backend listens on port `8080` by default (see `Backend/server.js`). API routes are mounted under `/api`.

2. Frontend

```bash
cd Frontend
npm install
npm run dev
```

The frontend uses Vite (default dev port 5173). It communicates with the backend API (e.g., `/api/chat`). If frontend and backend run on different origins, CORS is enabled in the backend.

## API (high level)
- `POST /api/chat` — body: `{ threadId, message }` — creates/updates a thread, calls OpenAI, saves assistant reply, returns `{ reply }`.
- `GET /api/thread` — returns threads (sorted by `updatedAt`).
- `GET /api/thread/:threadId` — returns messages for a thread.
- `DELETE /api/thread/:threadId` — deletes a thread.

## Notes
- The OpenAI request is implemented in `Backend/utils/openai.js` using the Chat Completions endpoint with model `gpt-4o-mini`.
- Ensure your `OPENAI_API_KEY` has permission and usage limits set appropriately.

If you want, I can also: add a sample `.env.example`, update package.json scripts to clarify dev vs start, or run the app locally to verify. Which would you like next?
