AI Chatbot using LangGraph and Streamlit

A minimal example chatbot built with LangGraph for managing conversation state and a Streamlit frontend for a simple chat UI. The project demonstrates wiring a GROQ-powered LLM into a state graph and exposing it via a lightweight Streamlit app.

**Repository layout**
- `langgraph_backend.py` - defines the `StateGraph`-based chatbot and the GROQ LLM client.
- `streamlit_frontend.py` - Streamlit chat UI that calls the compiled chatbot.

**Features**
- Uses `langgraph` to model chat state and transitions.
- Calls a GROQ model via `langchain_groq`.
- Simple Streamlit-based chat UI with session-state message history.

Requirements
-----------
- Python 3.10+
- A GROQ API key (set as `GROQ_API_KEY` in environment or a `.env` file)

Install
-------
Create and activate a virtual environment, then install dependencies:

```bash
python -m venv .venv
.\.venv\Scripts\activate
pip install -r requirements.txt
```

Environment
-----------
Create a `.env` file in the project root or export the environment variable directly. Example `.env`:

```
GROQ_API_KEY=your_groq_api_key_here
```

Run
---
Start the Streamlit frontend which imports and uses the backend:

```bash
streamlit run streamlit_frontend.py
```

Open the URL shown by Streamlit (usually `http://localhost:8501`) and type messages into the chat input. The frontend sends a `HumanMessage` to the compiled `chatbot` from `langgraph_backend.py` and displays responses.

Notes
-----
- Conversation history is stored in Streamlit's `st.session_state` for the current session only; it is not persisted to disk in this example.
- The backend (`langgraph_backend.py`) uses `ChatGroq` and expects a valid `GROQ_API_KEY`. If missing or invalid, calls to the LLM will fail.
- This project is a minimal example and may need error handling, persistence, and security improvements for production.

Want improvements?
------------------
- Add persistence for conversation history (database or file-backed checkpointer).
- Add authentication and rate-limiting for multi-user deployments.

License
-------
MIT-style (modify as needed).