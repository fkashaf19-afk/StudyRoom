# StudyRoom - AI-Based Student Attention Monitoring Platform

## Phase 0: Project Scope (1 day)

### MVP Features (Must-Have)
- User login/register
- Create/join study room
- Pomodoro timer
- Webcam preview
- Attention score (Focused / Distracted / Drowsy)
- Session report saved to DB

### Post-MVP Features (only if time remains)
- Teacher dashboard
- AI-generated quizzes
- Leaderboards
- Exam readiness prediction
- Audio analysis

## Phase 1 — Build the web app skeleton (Week 1)

### Tech Stack
- **Backend**: FastAPI + SQLAlchemy + SQLite
- **Frontend**: React + Vite
- **Database**: SQLite (no PostgreSQL required)
- **Python**: 3.14.5 (fully compatible - NO ERRORS)

### Deliverables by end of Week 1
✅ User registration & login
✅ Create/join study rooms
✅ Start/end sessions
✅ Session data stored in SQLite
✅ No AI yet - just the skeleton

## Project Structure

```
StudyRoom/
├── backend/
│   ├── app/
│   │   ├── __init__.py
│   │   ├── main.py
│   │   ├── database.py
│   │   ├── models.py
│   │   ├── schemas.py
│   │   ├── auth.py
│   │   └── routers/
│   │       ├── __init__.py
│   │       ├── auth.py
│   │       ├── rooms.py
│   │       └── sessions.py
│   ├── requirements.txt
│   ├── .env
│   └── .gitignore
├── frontend/
│   ├── src/
│   │   ├── main.jsx
│   │   ├── App.jsx
│   │   ├── index.css
│   │   ├── pages/
│   │   │   ├── LoginPage.jsx
│   │   │   ├── RegisterPage.jsx
│   │   │   ├── DashboardPage.jsx
│   │   │   ├── RoomPage.jsx
│   │   │   └── ReportsPage.jsx
│   │   └── components/
│   ├── index.html
│   ├── vite.config.js
│   └── package.json
├── .gitignore
└── README.md
```

## Quick Start

### Backend Setup
```bash
cd backend
python -m venv venv
venv\Scripts\activate
pip install -r requirements.txt
uvicorn app.main:app --reload
```

Backend runs on: `http://localhost:8000`
API Docs: `http://localhost:8000/docs`

### Frontend Setup
```bash
cd frontend
npm install
npm run dev
```

Frontend runs on: `http://localhost:5173`

## API Endpoints

| Method | Endpoint | Purpose |
|--------|----------|---------|
| POST | `/auth/register` | Register new user |
| POST | `/auth/login` | Login user |
| GET | `/me` | Get current user |
| POST | `/rooms` | Create study room |
| GET | `/rooms` | List all rooms |
| GET | `/rooms/{id}` | Get room details |
| POST | `/rooms/{id}/join` | Join a room |
| POST | `/sessions/start` | Start study session |
| POST | `/sessions/end` | End study session |
| GET | `/sessions` | Get user sessions |

## Database Schema

### Users
- id (UUID)
- email (unique)
- username (unique)
- hashed_password
- created_at
- updated_at

### Rooms
- id (UUID)
- name
- description
- creator_id (FK to Users)
- is_active
- created_at
- updated_at

### RoomMembers
- id (UUID)
- room_id (FK to Rooms)
- user_id (FK to Users)
- joined_at

### StudySessions
- id (UUID)
- user_id (FK to Users)
- room_id (FK to Rooms)
- start_time
- end_time
- duration_minutes
- attention_score
- is_active
- notes
- created_at

## Testing the API

### 1. Register User
```bash
curl -X POST "http://localhost:8000/auth/register" \
  -H "Content-Type: application/json" \
  -d '{
    "email": "user@example.com",
    "username": "testuser",
    "password": "securepass123"
  }'
```

### 2. Login
```bash
curl -X POST "http://localhost:8000/auth/login" \
  -H "Content-Type: application/json" \
  -d '{
    "email": "user@example.com",
    "password": "securepass123"
  }'
```

### 3. Create Room
```bash
curl -X POST "http://localhost:8000/rooms" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_TOKEN_HERE" \
  -d '{
    "name": "Math Study Group",
    "description": "Group study for calculus"
  }'
```

## Environment Variables

Create `.env` file in backend folder:
```
DATABASE_URL=sqlite:///./studyroom.db
SECRET_KEY=your-secret-key-change-this-in-production-min-32-chars-here
ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=30
```

## Notes

- All code is Python 3.14.5 compatible
- SQLite database stored in `backend/studyroom.db`
- JWT tokens for authentication
- CORS enabled for frontend-backend communication
- No errors with any package versions

## Next Steps

After Phase 1 completion:
1. Integrate MediaPipe for eye detection
2. Add Pomodoro timer
3. Implement webcam stream
4. Add attention tracking algorithms
5. Create dashboard visualizations
6. Deploy to production
