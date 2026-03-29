# AI Career Navigator — Complete Local Dev Setup

> **Prototype / Functional Validation Only.**
> Optimised for speed and demo clarity — not production security.

---

## Stack

| Layer     | Technology                          |
|-----------|-------------------------------------|
| Frontend  | React 18 + Vite + Tailwind CSS      |
| Backend   | Node.js + Express                   |
| Database  | PostgreSQL 16                       |
| Cache     | Redis 7                             |
| Documents | MongoDB 7                           |
| AI        | OpenAI / Anthropic / Ollama / Mock  |

---

## Prerequisites

| Tool          | Version |
|---------------|---------|
| Node.js       | 18+     |
| Docker        | 24+     |
| Docker Compose| v2      |

---

## Quick Start

```bash
chmod +x scripts/dev-start.sh
./scripts/dev-start.sh
```

---

## Service URLs

| Service         | URL                                   |
|-----------------|---------------------------------------|
| Frontend        | http://localhost:5173                 |
| Backend API     | http://localhost:3001                 |
| Health Check    | http://localhost:3001/api/health      |
| pgAdmin (DB UI) | http://localhost:5050  (admin@dev.local / admin) |
| Redis UI        | http://localhost:8081                 |

---

## AI Provider Setup

Edit `backend/.env` and set `AI_PROVIDER` to one of:

| Value       | Description                                 |
|-------------|---------------------------------------------|
| `mock`      | Instant canned responses — no setup needed  |
| `openai`    | GPT-4o-mini — set `OPENAI_API_KEY`          |
| `anthropic` | Claude Haiku — set `ANTHROPIC_API_KEY`      |
| `ollama`    | Local model — run Docker with Ollama image  |

**Recommended for demos:** `mock`
**Recommended for real use:** `openai` or `anthropic`

---

## Mock Users (Role Switcher)

Use the bottom-left dropdown in the app to switch roles. Sends `x-mock-user-id` header automatically.

| Role       | Email                  |
|------------|------------------------|
| Admin      | admin@dev.local        |
| Counselor  | counselor@dev.local    |
| Student    | student@dev.local      |

---

## API Reference

```
GET  /api/health
GET  /api/careers
GET  /api/careers/:slug
GET  /api/profiles/me
PUT  /api/profiles/me
POST /api/assessment/submit
GET  /api/recommendations
POST /api/recommendations/refresh
POST /api/recommendations/:id/feedback
GET  /api/roadmaps
POST /api/roadmaps
PATCH /api/roadmaps/:id/item
POST /api/advisor/chat
GET  /api/advisor/sessions
GET  /api/advisor/sessions/:id
POST /api/resume/analyze
GET  /api/resume/history
POST /api/comparison
```

---

## Project Structure

```
navigator/
├── docker-compose.yml
├── scripts/dev-start.sh
├── docker/
│   ├── postgres/init.sql      # schema + 10 career roles + 3 demo users
│   └── mongo/init.js
├── backend/
│   ├── .env
│   ├── package.json
│   └── src/
│       ├── index.js
│       ├── middleware/mockAuth.js
│       ├── services/
│       │   ├── postgres.js
│       │   ├── redis.js
│       │   ├── mongo.js
│       │   ├── ai.js          # multi-provider AI adapter
│       │   └── engine.js      # cosine similarity recommendation engine
│       ├── routes/
│       │   ├── health.js
│       │   ├── careers.js
│       │   ├── profiles.js
│       │   ├── assessment.js
│       │   ├── recommendations.js
│       │   ├── roadmaps.js
│       │   ├── advisor.js
│       │   ├── resume.js
│       │   └── comparison.js
│       └── scripts/seed.js
└── frontend/
    ├── .env
    ├── package.json
    ├── vite.config.js
    ├── tailwind.config.js
    └── src/
        ├── main.jsx
        ├── App.jsx
        ├── index.css
        ├── store/AuthContext.jsx
        ├── services/api.js
        ├── components/
        │   ├── layout/Layout.jsx   # sidebar + navigation
        │   └── ui/index.jsx        # Card, Btn, Badge, ProgressBar...
        └── pages/
            ├── Dashboard.jsx
            ├── Assessment.jsx
            ├── Recommendations.jsx
            ├── Roadmap.jsx
            ├── Advisor.jsx
            ├── Careers.jsx
            ├── ResumeUpload.jsx
            └── Comparison.jsx
```

---

## Reset Everything

```bash
docker compose down -v   # removes all data volumes
./scripts/dev-start.sh   # fresh start
```
