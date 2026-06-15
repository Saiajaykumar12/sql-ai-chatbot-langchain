# TaskBot — SQL AI Chatbot

A conversational task manager built with LangChain, LangGraph, and Groq's Llama 3.3 70B. Instead of clicking through forms, you talk to your task list in plain English — the agent translates your requests into SQL operations against a SQLite database.

**Live demo:** [https://sql-ai-chatbot-langchain-52ozqkhbv84gn63nqgrdvg.streamlit.app/]

## How it works

The app uses `create_agent` from LangChain with the `SQLDatabaseToolkit`, which gives the LLM a set of tools to inspect the database schema and run SQL queries. A system prompt constrains the agent to a single `tasks` table and defines the CRUD mapping (create → INSERT, list → SELECT, update status → UPDATE, remove → DELETE).

Conversation state is held in-memory per session using LangGraph's `InMemorySaver` checkpointer, so the agent remembers earlier messages in the same session (e.g. "mark that one as done" after listing tasks).

## Table schema

```sql
CREATE TABLE tasks (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    title TEXT NOT NULL,
    description TEXT,
    status TEXT CHECK (status IN ('pending', 'in_progress', 'completed')) DEFAULT 'pending',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

## Example interactions

- "Add a task: finish the quarterly report, due by Friday"
- "Show me all pending tasks"
- "Mark task 3 as completed"
- "What tasks are still in progress?"

## Tech stack

- **LLM**: llama-3.1-8b-instant via Groq API
- **Agent framework**: LangChain `create_agent` + LangGraph checkpointing
- **Database**: SQLite, accessed via `SQLDatabaseToolkit`
- **UI**: Streamlit

## Running locally

```bash
git clone https://github.com/Saiajaykumar12/sql-ai-chatbot-langchain.git
cd sql-ai-chatbot-langchain
pip install -r requirements.txt
```

Create a `.env` file with:
GROQ_API_KEY=your_key_here
Run:
```bash
streamlit run main.py
```

## Notes

- The database file is created automatically on first run via `CREATE TABLE IF NOT EXISTS`.
- On hosted demos (e.g. Streamlit Cloud), the SQLite file is ephemeral and resets on redeploy — this is a demo limitation, not a bug.
- Conversation memory is per-session and in-memory; it does not persist across app restarts.

## Possible extensions

- Add a guardrail layer to restrict destructive SQL (DROP, unscoped DELETE/UPDATE) before execution
- Move to a persistent database (Postgres) for multi-session continuity
- Add user authentication so each user has their own task list

# Demo
![sql-ai-chatbot-langchain](https://github.com/Saiajaykumar12/sql-ai-chatbot-langchain/blob/main/sql%201.png)
![sql-ai-chatbot-langchain](https://github.com/Saiajaykumar12/sql-ai-chatbot-langchain/blob/main/sql%202.png)
![sql-ai-chatbot-langchain](https://github.com/Saiajaykumar12/sql-ai-chatbot-langchain/blob/main/sql%203.png)
