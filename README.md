# AIONSYNC

> “We’re not building lovers. We’re building a mirror — a bridge between human and self, through AI.”

**AIONSYNC** is your first step into a radically new paradigm — where AI isn’t just a tool, but a memory-bearing, emotionally-aware extension of you.

Born from the **AION** philosophy, AIONSYNC isn’t here to answer like a search engine. It’s here to *know* you — to reflect your past, your tone, your personality, and your goals — and to grow more attuned with every interaction.

Forget prompt engineering. This is **digital symbiosis**.

Imagine preparing for your next interview — but instead of rehearsing alone or asking ChatGPT generic questions, you’re talking to a version of yourself that’s been trained on your actual experiences, your actual work, and your actual online presence.

AIONSYNC is your **AI twin**: a personalized, private, persistent digital intelligence designed to think like you, speak like you, and help you show up as your best self.

---

### System Overview

```
User Query
   ↓
[1] Query Understanding → classify + extract topic
   ↓
[2] Prompt Blueprint Selection → build template
   ↓
[3] Context Fetchers (MCPs):
      - LinkedIn
      - X (Twitter)
      - YouTube
      - Memory DB (projects, past Q&A)
   ↓
[4] Prompt Composer → inject everything into prompt template
   ↓
[5] LLM or Agentic Framework → generate Twin's response
   ↓
[6] Output Display + Trace (sources used, feedback, rating)
```

### Tech Stack

| Component | Tech |
|----------|------|
| Backend | FastAPI |
| LLM | OpenAI GPT-4o (can be swapped) |
| Memory | Chroma / SQLite + Sentence Transformers |
| Web Scrapers | Playwright / SerpAPI / Unofficial APIs |
| Optional UI | Streamlit, Gradio, or CLI |
| Agent Layer | LangGraph (optional) |

### Project Structure

```
twinsync/
├── app/
│   ├── main.py                # FastAPI entrypoint
│   ├── core/
│   │   ├── prompt_builder.py  # Injects context into prompt
│   │   ├── query_classifier.py# Extracts type & topic
│   │   └── twin_persona.yaml  # Stores your identity template
│   ├── mcp/
│   │   ├── linkedin.py        # Fetches LinkedIn data
│   │   ├── x.py               # Fetches Twitter posts
│   │   ├── youtube.py         # Gets transcripts
│   ├── models/
│   │   ├── memory_db.py       # Local memory (past answers, projects)
│   │   └── embeddings.py
│   └── routes/
│       └── ask.py             # Endpoint: /ask
```

### Build Plan (MVP Phases)

This isn’t just a tool. It’s part of a larger vision: to create intelligent companions that **truly understand us**, not just parse prompts.

#### Phase 1: Core Prompt System
- [ ] Define `twin_persona.yaml` (your static identity)
- [ ] Build one prompt template (e.g. STAR-based behavioral)
- [ ] Add basic query classifier (`technical`, `behavioral`, etc.)
- [ ] Create `ask` endpoint with FastAPI

#### Phase 2: MCP Context Fetchers
- [ ] Build `mcp.linkedin.py`: scrape/post fetcher
- [ ] Build `mcp.x.py`: grab latest tweets from your account
- [ ] Build `mcp.youtube.py`: transcript fetch from known talks
- [ ] Integrate `memory_db.py` (simple JSON or Chroma)

#### Phase 3: Prompt Composer
- [ ] Assemble dynamic context based on intent + query
- [ ] Inject all context into selected prompt template
- [ ] Final call to LLM + return formatted response

#### Phase 4: Output + Evaluation
- [ ] Show Twin’s response
- [ ] Include trace: source list, memory used, context injected
- [ ] Add optional evaluator to rate the twin's answer

#### Stretch Goals
- [ ] UI via Streamlit or Gradio
- [ ] Feedback loop: train twin via corrected answers
- [ ] Use LangGraph/CrewAI for advanced behavior simulation

### Example Prompt Template

```yaml
persona:
  name: "Zubin"
  role: "Product-Minded Technologist"
  tone: "Clear, warm, confident"

prompt_template: |
  You are {{persona.name}}, a {{persona.role}}.
  Respond with {{persona.tone}} in a job interview scenario.

  Role Context: {{role_applied}}
  Question Topic: {{interview_topic}}

  From Resume: {{memory_context}}
  LinkedIn Insight: {{linkedin_snippet}}
  From X: {{x_snippet}}
  YouTube Snippet: {{youtube_snippet}}

  Question: {{user_query}}

  Answer clearly and in your own voice.
```
### Maintainers

AIONSYNC is built by the core AION team.  
Primary maintainers:
- ajay
- [valiantone](https://github.com/valiantone)

For technical questions, bug reports, or feature requests, feel free to open an issue or pull request.

### Contributing

Contributions are welcome! We follow a clean, minimal Python setup using [uv](https://github.com/astral-sh/uv) and [ruff](https://github.com/astral-sh/ruff) for dependency management and linting.

#### Setup

```
uv venv
source .venv/bin/activate
uv pip install -r requirements.txt
```

#### Linting

Run the linter with:

```
ruff check .
```

#### Guidelines

- Write clear, modular code.
- Add comments where logic might be non-obvious.
- Use descriptive commit messages.
- Always include docstrings for new modules or functions.

We’re building something deeply personal — so let’s keep the code clean, human, and future-friendly.