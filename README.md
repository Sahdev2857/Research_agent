# Research Agent

A research agent that runs locally on [Ollama](https://ollama.ai). Give it a topic or question and it searches the web, reads relevant pages, saves everything it finds with source links, and writes a final summary. Afterwards you can ask it questions about its findings.

## How it works

1. You enter a research query.
2. The LLM creates 5 prioritized focus areas.
3. For each area it searches the web, picks relevant pages, scrapes them, and saves the content with source URLs to a text file.
4. It generates new focus areas from what it found and repeats.
5. When you quit, it reviews all collected content and writes a summary.
6. Conversation mode lets you ask follow-up questions about the findings.

## Installation (macOS / Linux)

```sh
git clone <your-repo-url>
cd Research_agent
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

Install Ollama from https://ollama.ai and pull a model, for example `phi3:3.8b-mini-128k-instruct`. A model with a large context window is recommended.

## Configuration

Open `llm_config.py` and set your model name in the Ollama section:

```python
LLM_CONFIG_OLLAMA = {
    "llm_type": "ollama",
    "base_url": "http://localhost:11434",
    "model_name": "your-model-name",   # change this
    "n_ctx": 55000,                    # context size
}
```

## Usage

```sh
ollama serve          # in one terminal
python Web-LLM.py     # in another
```

Type `@` followed by your query, then press `CTRL+D` to submit. Example: `@What are the latest trends in AI agents?`

Commands during research (type the letter, then `CTRL+D`):

| Key | Action |
|-----|--------|
| `s` | Show status |
| `f` | Show current focus |
| `p` | Pause and assess progress (then `c` to continue or `q` to quit) |
| `q` | Quit research and generate the summary |

After the summary, use conversation mode to ask questions. The full research session (content, source URLs, focus areas, summary) is saved as a text file in the program folder.
