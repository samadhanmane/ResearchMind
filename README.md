# ResearchMind — Multi-Agent AI Research System

ResearchMind is a lightweight multi-agent research pipeline built with LangChain and Streamlit. Four specialized agents (search, reader, writer, critic) collaborate to gather recent web information, scrape deep content, draft a structured research report, and provide a constructive critique.

Stack
- Language(s): Python 3.10+
- Framework / runtime: Streamlit (UI) + LangChain agents
- Notable libraries: langchain, langchain-mistralai, tavily-python, beautifulsoup4

What this repository does
ResearchMind accepts a topic, runs a web search (via Tavily), scrapes top sources, drafts a detailed report using a LLM (Mistral/compatible through LangChain), and produces a scored critique. It ships both a Streamlit UI (`app.py`) and a programmatic/CLI pipeline (`pipeline.py`).

Repository layout
```
app.py           # Streamlit UI: visual pipeline and results display
agent.py         # Agent & chain construction (search/reader/writer/critic)
tools.py         # Tools used by agents: web_search (Tavily), scrape_url (requests + BeautifulSoup)
pipeline.py      # Procedural runner for the full research pipeline (CLI-friendly)
requirements.txt # Python dependencies
README.md        # This file
.gitignore
```

How it fits together
- app.py is the Streamlit entry point used for interactive sessions. It calls the same agents and chains built in `agent.py`.
- `agent.py` composes two agents (search + reader) using LangChain's `create_agent`, and two chains (writer + critic) implemented with chat prompts + LLM.
- `tools.py` exposes the `web_search` and `scrape_url` tools that agents use during the pipeline. `web_search` relies on the Tavily API.
- `pipeline.py` provides a non-interactive runner to produce the same outputs from the terminal.

Quickstart (local)
1. Clone and create a virtual environment

```bash
git clone https://github.com/samadhanmane/MultiAgentAI_ResearchSystem.git
cd MultiAgentAI_ResearchSystem
python -m venv .venv
source .venv/bin/activate  # or .\.venv\Scripts\activate on Windows
pip install -r requirements.txt
```

2. Add credentials
Create a `.env` file in the repo root with at least the Tavily API key. Example:

```
TAVILY_API_KEY=your_tavily_api_key_here
# plus any LLM provider keys required by your LangChain integration, e.g.:
# MISTRALAI_API_KEY=...
# OPENAI_API_KEY=...
```

3. Run the Streamlit app

```bash
streamlit run app.py
```

Or run the CLI pipeline

```bash
python pipeline.py
# then enter a research topic when prompted
```

Environment variables and configuration
- TAVILY_API_KEY: required for `tools.web_search` (Tavily client)
- LLM credentials: the app uses LangChain + ChatMistralAI; configure whichever provider keys your LangChain/Mistral adapter expects (environment variables depend on the adapter you use).

Files of interest
- `app.py`: UI, pipeline orchestration in the browser
- `agent.py`: prompt templates and agent/chain definitions
- `tools.py`: web search and scraping helpers
- `pipeline.py`: scriptable runner (prints progress to stdout)
- `requirements.txt`: dependency hints used by the project

Notes & caveats
- Scraping: `scrape_url` uses requests + BeautifulSoup and returns a text slice (first ~3000 chars). It intentionally removes some tags (script, style, nav, footer), but results may still contain noise — adjust as needed.
- Safety & rate limits: be mindful of provider rate limits (Tavily and the LLM provider). Add retries or backoff if you scale usage.
- Models: the repo references `mistral-small-2506` via `langchain_mistralai.ChatMistralAI`. If you use a different LLM, update the model initialization in `agent.py`.

Development & contribution
- Open an issue or a PR if you'd like to add features, e.g., multi-URL scraping, caching search results, or richer prompt templates.

License
- No license file provided. Add a LICENSE if you intend to publish this project.

Acknowledgements
- Built with LangChain, Tavily, BeautifulSoup and Streamlit.
