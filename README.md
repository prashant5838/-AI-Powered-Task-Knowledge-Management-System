# -AI-Powered-Task-Knowledge-Management-System
AI-powered Task &amp; Knowledge Management System — FastAPI + MySQL backend with JWT auth &amp; RBAC, React frontend, and a from-scratch semantic search engine (TF-IDF embeddings + FAISS/cosine similarity) for document search and task management.
# AI-Powered Task & Knowledge Management System

A full-stack MVP where an **Admin** builds a searchable knowledge base by 
uploading documents and assigns tasks to users, while **Users** leverage 
AI-powered semantic search to find answers and complete their assigned work.

Built with a FastAPI + MySQL backend (JWT authentication, role-based access 
control, and a fully relational schema) and a React frontend. The core AI 
feature — semantic search — is implemented from scratch: documents are 
chunked, converted into TF-IDF embeddings, indexed in FAISS (with an 
automatic numpy cosine-similarity fallback), and queried via vector 
similarity rather than simple keyword matching or an external LLM API call.

**Key features:**
- JWT authentication with Admin/User role-based access control
- Relational MySQL schema (users, roles, documents, tasks, activity_logs, 
  document_chunks, search_queries) with proper foreign keys
- Document upload with automatic chunking and embedding
- Semantic search built on TF-IDF vectorization + FAISS/cosine similarity
- Task creation, assignment, and status tracking with dynamic filtering
- Full activity audit log (logins, uploads, searches, task updates)
- Basic analytics dashboard (task counts, most-searched queries)
