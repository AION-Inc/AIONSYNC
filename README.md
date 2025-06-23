# TwiNSYNC

> A context-aware digital twin system for personalized interview preparation.

TwiNSYNC is a context-enhanced digital twin system that simulates how *you* would answer interview questions — using your experience, tone, and content pulled in real time from multiple sources. It's powered by Model Context Protocol (MCP) principles to dynamically fetch and inject relevant context into every response.

### What is TwiNSYNC?

TwiNSYNC assists in interview preparation by creating an intelligent representation of yourself. It functions as a digital model that understands your experience, communicates in your voice, and reflects your tone and style.

This system learns from your previous work, writing, and projects. When presented with a question, it generates answers that align with how *you* would respond — clear, confident, and personalized.

It integrates real-time information (such as your LinkedIn posts or YouTube presentations) with your resume and history to help you respond to challenging questions naturally and authentically, effectively coaching you through the interview process.

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

### Credits & Naming

Project Name: **TwiNSYNC™**  
> A context-aware MCP system that keeps your digital twin in sync with everything *you* are.

### Next Step

To start the server:
```bash
uvicorn app.main:app --reload
```

To test with a mock question:
```bash
curl -X POST http://localhost:8000/ask -d '{"query": "Tell me about a time you led a design team."}'
```
