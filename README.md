# ResearchMind

ResearchMind is a multi-agent AI research assistant that turns a topic into a structured research report and a critical review. It uses LangChain and Groq for orchestration and generation, Tavily for web search, Beautiful Soup for page extraction, and Streamlit for its web interface.

## How it works

The pipeline has four focused stages:

1. **Search agent** finds recent, relevant sources with Tavily.
2. **Reader agent** selects and scrapes a useful source for deeper context.
3. **Writer chain** produces a structured report from the gathered research.
4. **Critic chain** scores the report and identifies strengths and improvements.

The Streamlit app shows each stage, exposes the raw research outputs, renders the final report, and lets you download it as Markdown.

## Requirements

- Python 3.11 or later
- A [Groq API key](https://console.groq.com/keys)
- A [Tavily API key](https://app.tavily.com/)

## Setup

Create and activate a virtual environment:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

Install the dependencies:

```bash
pip install -r requirements.txt
```

Create a `.env` file in the project root with your credentials:

```env
GROQ_API_KEY=your_groq_api_key
TAVILY_API_KEY=your_tavily_api_key
```

Never commit `.env`; it is already excluded through `.gitignore`.

## Run the web app

```bash
streamlit run app.py
```

Open the local URL printed by Streamlit, enter a research topic, and select **Run Research Pipeline**. The final report can be downloaded from the results section.

## Run from the terminal

For an interactive command-line version:

```bash
python3 pipeline.py
```

Enter a topic when prompted. The terminal prints the search output, scraped content, final report, and critic feedback.

## Project structure

```text
.
├── app.py          # Streamlit interface and visual pipeline flow
├── agents.py       # Search/reader agents plus writer and critic chains
├── tools.py        # Tavily search and URL-scraping tools
├── pipeline.py     # Interactive command-line pipeline
├── requirements.txt
└── .env            # Local API keys; do not commit
```

## Configuration

The Groq model is configured in `agents.py` as `openai/gpt-oss-120b` with a temperature of `0`. Change that value if your Groq account uses a different supported model or if you want a different balance of creativity and consistency.

## Notes

- Scraped pages are limited to 3,000 characters to keep prompts manageable.
- Web search returns up to five results per query.
- Generated reports should be reviewed and source-checked before being used for high-stakes, academic, medical, legal, or financial decisions.
