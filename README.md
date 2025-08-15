# Custom GPT Bot

A **private AI chatbot** built with **FastAPI**, **Streamlit**, and **Ollama/Groq/OpenAI (optional)** for intelligent conversations, powered by **llama-index** and **TinyDB** (easily swappable with MySQL/PostgreSQL).  

---

## Features
- **Private Chat** with locally hosted or cloud-based LLMs.
- **Multiple Providers**: Ollama (local), Groq, OpenAI.
- **Conversation History** stored in TinyDB.
- **FastAPI Backend** with REST APIs.
- **Streamlit Frontend** for chat interface.
- **Extensible Architecture** for integrating new models.

---

## Tech Stack
From `tech_stack.txt`:
```
- Python
- Ollama (Groq & OpenAI - optional)
- llama-index
- FastAPI
- Streamlit
- Tinydb (can be replaced with MySQL, Postgres, etc.)
```

---

## Project Structure
```
private-chatgpt-app/
├── .venv/                  # Virtual environment
├── backend/
│   ├── api/
│   │   ├── chat.py
│   │   ├── conversation.py
│   │   ├── db_services.py
│   │   ├── provider_models.py
│   │   └── title.py
│   ├── config/
│   ├── db/
│   │   ├── __init__.py
│   │   └── chat_dao.py
│   ├── llm/
│   ├── services/
│   │   ├── __init__.py
│   │   └── main.py
│   └── data/
│       ├── chat.db
│       └── placeholder.txt
├── frontend/
│   └── .env
├── .gitignore
├── env_template.txt
└── README.md
```

---

## Installation & Setup

### Clone the Repository
```bash
git clone https://github.com/<your-username>/private-chatgpt-app.git
cd private-chatgpt-app
```

### Create & Activate Virtual Environment
```bash
python3 -m venv .venv
source .venv/bin/activate    # Mac/Linux
# OR
.venv\Scripts\activate       # Windows
```

### Install Dependencies
```bash
pip install -r requirements.txt
```

---

## Environment Variables
Copy the template and fill in your API keys:
```bash
cp env_template.txt .env
```
Edit `.env` and add:
```
OPENAI_API_KEY=your_openai_key
GROQ_API_KEY=your_groq_key
OLLAMA_API_URL=http://localhost:11434
```

---

## Running the Application

### Backend (FastAPI)
```bash
cd backend
uvicorn services.main:app --reload --host 0.0.0.0 --port 8000
```
Runs on: `http://127.0.0.1:8000`

### Frontend (Streamlit)
```bash
cd frontend
streamlit run app.py --server.port 8501
```
Runs on: `http://localhost:8501`

---

## Database
- Default: **TinyDB** (lightweight JSON-based DB)
- Replaceable with **MySQL** / **PostgreSQL** by editing `backend/db/chat_dao.py`.

---

## 📌 API Endpoints

| Method | Endpoint              | Description |
|--------|----------------------|-------------|
| POST   | `/chat`               | Send a message to the bot |
| GET    | `/conversation/{id}`  | Retrieve conversation history |
| POST   | `/title`              | Generate a title for conversation |
| GET    | `/models`             | List available LLM models |

---

##  Example API Usage

### cURL
```bash
curl -X POST "http://127.0.0.1:8000/chat"      -H "Content-Type: application/json"      -d '{"message": "Hello, GPT!"}'
```

### Python Client
```python
import requests

response = requests.post(
    "http://127.0.0.1:8000/chat",
    json={"message": "Hello, GPT!"}
)
print(response.json())
```
