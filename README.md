# ResearchMind — Multi-Agent AI Research System

ResearchMind is a lightweight **multi-agent AI research system** built with **LangChain, Streamlit, and Mistral**. It uses specialized AI agents to search the web, extract information from reliable sources, generate a structured research report, and critically evaluate the final output.

The system is designed as a modular research pipeline where each agent has a specific responsibility:

**Search → Reader → Writer → Critic**

---

## 🚀 Features

* 🔎 **Web Research** — Search the web for recent and relevant information using Tavily.
* 📄 **Deep Content Extraction** — Scrape and extract useful content from web pages.
* 🤖 **Multi-Agent Architecture** — Separate agents handle searching and reading tasks.
* ✍️ **AI Report Generation** — Generate structured research reports using an LLM.
* 🧐 **AI Critic** — Evaluate the generated report and provide constructive feedback.
* 🖥️ **Streamlit Interface** — Interactive UI for running research tasks.
* 💻 **CLI Pipeline** — Run the complete research workflow directly from the terminal.
* 🧩 **Modular Architecture** — Search, scraping, agents, prompts, and pipeline execution are separated into different modules.
* 🔄 **LLM Flexibility** — Designed around LangChain so the underlying LLM can be changed with minimal modifications.

---

## 🏗️ Architecture

```text
                         ┌─────────────────────┐
                         │      User Topic     │
                         └──────────┬──────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │   Search Agent      │
                         │                     │
                         │  Web Search/Tavily  │
                         └──────────┬──────────┘
                                    │
                              Search Results
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │    Reader Agent     │
                         │                     │
                         │ URL Scraping +      │
                         │ Content Extraction  │
                         └──────────┬──────────┘
                                    │
                              Research Data
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │    Writer Chain     │
                         │                     │
                         │ Structured Report   │
                         └──────────┬──────────┘
                                    │
                              Draft Report
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │    Critic Chain     │
                         │                     │
                         │ Score + Feedback    │
                         └──────────┬──────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │   Final Research    │
                         │      Output         │
                         └─────────────────────┘
```

---

## 🧠 How It Works

ResearchMind processes a research topic through four major stages.

### 1. Search Agent

The Search Agent receives the user's research topic and searches the web for:

* Recent information
* Relevant sources
* Reliable articles
* Supporting evidence
* Multiple perspectives

The agent uses the `web_search` tool powered by Tavily.

### 2. Reader Agent

The Reader Agent takes the URLs discovered during the search stage and extracts useful information from them.

It uses:

* `requests`
* `BeautifulSoup`
* HTML cleaning
* Text extraction

The extracted information is then passed to the writing stage.

### 3. Writer Chain

The Writer Chain receives the collected research information and generates a structured research report.

The generated report can include:

* Introduction
* Key findings
* Important facts
* Analysis
* Supporting evidence
* Conclusion

### 4. Critic Chain

The Critic Chain evaluates the generated report.

It provides:

* Overall score
* Strengths
* Weaknesses
* Missing information
* Accuracy concerns
* Suggestions for improvement

This creates a feedback layer instead of simply returning the first generated answer.

---

## 🛠️ Technology Stack

| Technology     | Purpose                         |
| -------------- | ------------------------------- |
| Python 3.10+   | Core programming language       |
| LangChain      | Agent and LLM orchestration     |
| Mistral        | Language model                  |
| Tavily         | Web search                      |
| BeautifulSoup4 | Web scraping                    |
| Requests       | HTTP requests                   |
| Streamlit      | Web interface                   |
| python-dotenv  | Environment variable management |

---

## 📁 Repository Structure

```text
ResearchMind/
│
├── app.py
├── agent.py
├── tools.py
├── pipeline.py
├── requirements.txt
├── README.md
├── LICENSE
└── .gitignore
```

### `app.py`

Streamlit application and interactive user interface.

### `agent.py`

Contains the construction of:

* Search Agent
* Reader Agent
* Writer Chain
* Critic Chain

### `tools.py`

Contains tools used by the agents:

* `web_search`
* `scrape_url`

### `pipeline.py`

Provides a programmatic/CLI version of the complete research pipeline.

### `requirements.txt`

Contains the Python dependencies required to run the project.

### `LICENSE`

Contains the MIT License for the project.

---

## ⚙️ Installation

### 1. Clone the repository

```bash
git clone https://github.com/samadhanmane/ResearchMind.git
cd ResearchMind
```

### 2. Create a virtual environment

#### Windows

```bash
python -m venv .venv
.venv\Scripts\activate
```

#### Linux/macOS

```bash
python -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

---

## 🔑 Environment Variables

Create a `.env` file in the root directory:

```env
TAVILY_API_KEY=your_tavily_api_key

MISTRALAI_API_KEY=your_mistral_api_key
```

Depending on the LLM provider you configure, additional environment variables may be required.

**Never commit your ****`.env`**** file or API keys to GitHub.**

---

## ▶️ Running the Application

### Streamlit UI

Run:

```bash
streamlit run app.py
```

The Streamlit interface will allow you to enter a research topic and execute the complete pipeline interactively.

### CLI Pipeline

You can also run the pipeline directly:

```bash
python pipeline.py
```

Then enter the research topic when prompted.

---

## 🔬 Example

Input:

```text
Impact of Generative AI on Software Engineering
```

ResearchMind performs:

```text
Topic
  ↓
Web Search
  ↓
Relevant Sources
  ↓
Web Scraping
  ↓
Extracted Research
  ↓
AI Report Generation
  ↓
AI Criticism
  ↓
Final Research Report
```

---

## ⚠️ Limitations

ResearchMind is currently designed as a lightweight research system and has some limitations:

* Web pages may block automated requests.
* Scraped content may contain unwanted text or formatting.
* The current scraper extracts a limited amount of content from each page.
* Search and LLM providers have API rate limits.
* Generated information should be independently verified for critical research.
* Some websites may require JavaScript rendering and therefore cannot be fully scraped using `requests` and BeautifulSoup.

---

## 🤝 Contributing

Contributions are welcome.

If you would like to improve ResearchMind:

1. Fork the repository.
2. Create a new branch.

```bash
git checkout -b feature/your-feature
```

3. Make your changes.
4. Commit your changes.

```bash
git commit -m "Add your feature"
```

5. Push the branch.

```bash
git push origin feature/your-feature
```

6. Open a Pull Request.

---

## 📜 License

ResearchMind is licensed under the **MIT License**.

---

## 🙌 Acknowledgements

ResearchMind is built using:

* LangChain
* Mistral AI
* Tavily
* Streamlit
* BeautifulSoup

---

## 👨‍💻 Author

**Samadhan Mane**

GitHub: `https://github.com/samadhanmane`

---

⭐ If you find ResearchMind useful, consider giving the repository a star!
