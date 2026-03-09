# RAG-based-Company-Knowledge-Assistant
This project implements a Retrieval-Augmented Generation (RAG) system that allows users to query and retrieve information from company documents using LLMs and vector search.
🧠 Company Knowledge Assistant
A Retrieval-Augmented Generation (RAG) system that enables intelligent Q&A over company documents. Built with modern AI stack to provide accurate, source-grounded answers from your knowledge base.

✨ Features
📚 Multi-format Document Support: PDF, Markdown, Word documents, and plain text
🔍 Semantic Search: Vector embeddings with HNSW indexing for fast retrieval
🎯 Intelligent Reranking: Cohere reranking for improved relevance
💾 Semantic Caching: Redis-based caching to reduce API calls for similar questions
🌐 Web Interface: Clean, interactive UI for asking questions
📊 RAG Evaluation: Built-in Ragas metrics for system assessment
🗂️ Category Organization: Documents organized by type (FAQs, guides, policies, etc.)
🛠️ Tech Stack
🐍 Python + FastAPI: High-performance async API framework
🔗 LangChain: Orchestration framework for LLM applications
🤖 OpenAI API: GPT-4o-mini for generation, embeddings for vector search
🐘 PostgreSQL + pgvector: Vector database with HNSW indexing
📦 Redis: Semantic caching layer
🐳 Docker Compose: Container orchestration
🎯 Cohere Rerank: Advanced reranking for retrieval quality
📈 Ragas: RAG evaluation framework
🏗️ Pipeline
Data Indexing
Load Documents

Recursively scans data/ directory
Supports: .pdf, .md, .docx, .doc, .txt
Chunk Documents

Splits documents into chunks with RecursiveCharacterTextSplitter
Preserves metadata (category, source)
Embed & Store

OpenAI embeddings for vector representation
Stores in PostgreSQL with pgvector
Builds HNSW index for fast similarity search
Retrieval & Generation
Vector Retrieval

Retrieves top-k documents (default: 5) based on cosine similarity
Optional category filtering
Reranking

Cohere rerank-multilingual-v3.0 narrows to top 3 most relevant chunks
Redis Semantic Cache Check

Skips LLM call if cached answer exists for similar questions
Answer Generation

GPT-4o-mini generates answer grounded in retrieved context
Returns answer, sources, and contexts
🚀 Getting Started
Prerequisites
Docker
API Keys: OpenAI, Cohere (optional), LangSmith (optional)
Setup
Clone the repository

git clone <repo-url>
cd rag-company-knowledge-assistant
Configure environment variables

Create a .env file:

# Database
DATABASE_URL=postgresql+asyncpg://postgres:postgres@postgres:5432/postgres

# OpenAI
OPENAI_API_KEY=your_openai_key

# LangSmith (optional, for tracing)
LANGSMITH_TRACING_V2=true
LANGSMITH_PROJECT=cka
LANGSMITH_API_KEY=your_langsmith_key

# Data & Configuration
DATA_DIR=data
RETRIEVAL_K=5

# Redis
REDIS_URL=redis://cka-redis:6379/0

# Cohere (optional, for reranking)
CO_API_KEY=your_cohere_key
Start services

docker compose up
Access the application

Web UI: http://localhost:8000
Ingest your documents

Place documents in data/ directory (organized by category)
Click "Ingest Data" in the web UI, or POST to /ingest
Cleanup
To stop services and remove volumes:

docker compose down -v
🔧 API Endpoints
GET / - Web UI
POST /ingest - Trigger document ingestion
GET /ingest/status - Check ingestion status
POST /ask - Ask a question
{
  "question": "How many PTO days are full-time employees entitled to in a calendar year?"
}
🧪 Evaluation
Run RAG evaluation using Ragas metrics:

python app/eval_ragas.py
Metrics evaluated:

Faithfulness: Answer grounded in context
Answer Relevancy: Relevance of answer to question
Context Precision: Precision of retrieved contexts
Context Recall: Recall of relevant information
📝 License
See LICENSE file for details.
