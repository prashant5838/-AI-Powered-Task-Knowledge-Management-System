# AI-Powered Task & Knowledge Management System

## Short Explanation

This is a full-stack MVP where an **Admin** builds a searchable knowledge 
base by uploading documents and assigns tasks to users, while **Users** 
use AI-powered semantic search to find answers and complete their 
assigned tasks.

The system implements JWT authentication with role-based access control 
(Admin/User), a fully relational MySQL schema, and — as the core AI 
feature — a semantic search engine built from scratch. Documents are 
split into chunks, converted into TF-IDF embeddings (using scikit-learn), 
and indexed using FAISS for vector similarity search, with an automatic 
fallback to a numpy-based cosine similarity search if FAISS isn't 
installed. This means search results are based on true semantic/vector 
similarity, not simple keyword matching or a wrapper around an external 
LLM API.

Admins can upload `.txt` documents, create and assign tasks, and view 
analytics (task counts, most searched queries). Users can view their 
assigned tasks, update task status, and semantically search the 
knowledge base. Every key action (login, task update, document upload, 
search) is recorded in an activity log for auditing.

## Tech Stack

**Backend:**
- Python 3
- FastAPI (REST API framework)
- SQLAlchemy (ORM)
- MySQL (relational database)
- JWT (python-jose) for authentication
- Passlib (bcrypt) for password hashing
- scikit-learn (TF-IDF embeddings)
- FAISS / numpy (vector similarity search)

**Frontend:**
- React.js
- React Router (routing)
- Context API (auth state management)
- Fetch API (backend communication)

**Database:**
- MySQL with a normalized relational schema (users, roles, documents, 
  document_chunks, tasks, activity_logs, search_queries) with proper 
  primary/foreign key relationships

## Setup Steps

### 1. Database (MySQL)

Using Docker (recommended):
```bash
docker compose up -d
```
This starts MySQL on `localhost:3306` with database `ai_task_kb`.

Or, if running MySQL manually, create the database:
```sql
CREATE DATABASE ai_task_kb;
```

### 2. Backend Setup

```bash
cd backend
python -m venv venv
source venv/bin/activate      # Windows: venv\Scripts\activate
pip install -r requirements.txt
cp .env.example .env          # update DB credentials if needed
uvicorn app.main:app --reload --port 8000
```

Tables and default roles/admin account are created automatically on 
first run.

Default admin login:
Email: admin@example.com
Password: Admin@123

API docs available at: `http://localhost:8000/docs`

### 3. Frontend Setup

```bash
cd frontend
npm install
cp .env.example .env
npm start
```

App runs at: `http://localhost:3000`

### 4. Usage

1. Log in as admin.
2. Upload `.txt` documents (see `sample_documents/` folder) to build the 
   knowledge base.
3. Create and assign tasks to users.
4. Log in as a user to view tasks, update their status, and use semantic 
   search to query the knowledge base.
5. View analytics from the admin dashboard.
