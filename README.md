# PMS — Project Management System

A full-stack project and team management app: projects, tasks, teams, real-time chat, presence tracking and analytics dashboards.

## Tech stack

| Layer | Technologies |
|---|---|
| Frontend | React 19, React Router 7, Recharts, Socket.IO client, Google OAuth (`@react-oauth/google`), Create React App |
| Backend | Python, Flask, Flask-SocketIO, Flask-CORS |
| Database | MongoDB (PyMongo) |
| Auth | JWT (PyJWT), bcrypt password hashing, Google Sign-In |

## Features

- **Auth** — email/password registration & login, Google Sign-In, JWT sessions, role-based users
- **Projects** — create, update and list projects
- **Tasks** — create/assign tasks, status workflow, threaded task comments
- **Teams** — create teams, assign/remove users, working-status tracking
- **Real-time** — Socket.IO private messaging, chat history, online / break / offline presence
- **Dashboards** — project status, resource utilisation and weekly working-hours charts

## Project structure

```
Backend/          Flask API + Socket.IO server
  app/
    __init__.py   app factory, Mongo & CORS setup
    auth.py       /api/auth   — register, login, google-login
    projects.py   /api/project — projects, tasks, comments
    users.py      /api/user   — users, teams, working hours
    charts.py     /api/chart  — dashboard analytics
    events.py     Socket.IO events (chat, presence)
    utils.py      JWT helpers
  run.py          entry point (port 9005)
Frontend/         React client
  src/Pages       Dashboard, Projects, Tasks, Teams, Messages, Auth
  src/Component   Cards, grids, charts, chatbot, nav
  src/Hooks       data hooks (projects, organisation)
  src/Context     AuthContext
```

## Getting started

### Prerequisites
Python 3.10+, Node.js 18+, and a MongoDB instance.

### Backend
```bash
cd Backend
python -m venv venv && source venv/bin/activate   # Windows: venv\Scripts\activate
pip install -r requirements.txt
cp .env.example .env    # fill in SECRET_KEY, MONGO_URI, GOOGLE_CLIENT_ID
python run.py           # http://localhost:9005
```

### Frontend
```bash
cd Frontend
npm install
cp .env.example .env    # set REACT_APP_BASE_URL and REACT_APP_GOOGLE_CLIENT_ID
npm start               # http://localhost:3000
```

> The Socket.IO client connects to `REACT_APP_BASE_URL` with the trailing `/api` removed (e.g. `http://localhost:9005`).

## Environment variables

| File | Variable | Purpose |
|---|---|---|
| `Backend/.env` | `SECRET_KEY` | JWT signing key |
| | `MONGO_URI` | MongoDB connection string |
| | `GOOGLE_CLIENT_ID` | Verifies Google ID tokens |
| `Frontend/.env` | `REACT_APP_BASE_URL` | API base URL |
| | `REACT_APP_GOOGLE_CLIENT_ID` | Google Sign-In client ID |

## License

[MIT](LICENSE) © 2026 Anand Baid
