# Multi-Agent Research System

A production-style multi-agent research pipeline built with **LangGraph**, **OpenAI GPT-4o**, and **Tavily Search**.

This system takes a research goal, decomposes it into tasks, executes them using parallel AI agents, and generates a fully cited `.docx` research report.

---

## 🚀 Features

- Multi-agent orchestration using LangGraph
- Parallel task execution with ThreadPoolExecutor
- Human-in-the-loop review step (optional)
- Iterative research refinement loop
- Automatic citation generation
- Export to `.docx` format
- REST API using FastAPI

---

## 🧠 System Flow
User Input → Plan → Human Review → Execute → Evaluate → Synthesize → Cite → Export

---

## 🏗️ Project Structure
├── main.py
├── config/
│ └── config.py
├── src/
│ ├── app/graph/
│ ├── utils/tools/
├── data/
├── output/ # (ignored in git)
├── agents.md
├── graph_design.md
├── README.md

---

## ⚙️ Setup

### 1. Clone the repo

```bash
git clone https://github.com/YOUR_USERNAME/YOUR_REPO.git
cd YOUR_REPO

2. Create environment
python -m venv venv
source venv/bin/activate   # Mac/Linux
venv\Scripts\activate      # Windows

3. Install dependencies
pip install -r requirements.txt (or use uv sync if using uv)

4. Set API keys (IMPORTANT)
Create a .env file in root:
OPENAI_API_KEY=your_openai_key
TAVILY_API_KEY=your_tavily_key
Do NOT store API keys in config.py and Do NOT push .env to GitHub

5.Run the server
uvicorn main:app --reload --port 8000
Open API docs: http://localhost:8000/docs

API Usage:
Start a research session
curl -X POST http://localhost:8000/research \
-H "Content-Type: application/json" \
-d '{
  "research_goal": "Latest advancements in LLMs",
  "user_documents": []
}'
Check status
GET /research/{session_id}
Submit review
POST /research/{session_id}/review
Actions:
  approve
  modify
  reject

Output:
Generated reports are saved in:
output/

Example Use Case
Input:
"What are the latest advancements in LLMs?"

Output:

Structured research plan
Multi-agent execution
Final .docx report with citations