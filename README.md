# SQL AI Chatbot — LangChain + SQLite

Talk to your database in plain English.
No SQL knowledge required.

## Example Questions You Can Ask
- "How many employees joined last month?"
- "What is the total revenue this quarter?"
- "Show me all tasks due this week"

## How It Works
1. Connect to any SQLite database
2. Ask question in plain English
3. LangChain converts to SQL automatically
4. Query runs and returns the answer

## Tech Stack
- LangChain
- SQLite
- OpenAI GPT
- Python

## Setup
pip install -r requirements.txt
Add OPENAI_API_KEY in .env
python sql_chatbot.py
