# SQL AI Chatbot — LangChain + SQLite

Talk to any SQLite database in plain English. Ask business questions, get answers — no SQL knowledge needed.

## How it works

```
User types question in plain English
     ↓
LangChain SQLDatabaseChain
     ↓
GPT-4o converts question to SQL query
     ↓
Query runs against SQLite database
     ↓
Result converted back to natural language
     ↓
Answer returned to user
```

## Example questions

```
"How many tasks are due this week?"
"Show me all employees in the engineering department"
"What is the total count of completed tasks?"
"Which employee has the most open tasks?"
```

## Files

| File | What it does |
|------|-------------|
| `sql_chatbot.py` | Main chatbot script |
| `my_tasks.db` | Sample SQLite database (tasks) |
| `employee_records.csv` | Sample data for testing |
| `requirements.txt` | Dependencies |

## Tech stack

- LangChain (SQLDatabaseChain)
- OpenAI GPT-4o (natural language to SQL)
- SQLite (database)
- Python

## Setup

```bash
pip install -r requirements.txt
```

Create `.env`:
```
OPENAI_API_KEY=your_key
```

```bash
python sql_chatbot.py
```

Point it at any SQLite database by changing the `db_path` variable in `sql_chatbot.py`.

## Related projects

- [RAG PDF Chatbot](https://github.com/Saiajaykumar12/langchain-rag-pdf-chatbot) — same natural language interface for documents
- [LangGraph Agentic RAG](https://github.com/Saiajaykumar12/langgraph-agentic-rag) — adds autonomous reasoning on top
