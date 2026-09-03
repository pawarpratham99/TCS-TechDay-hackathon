# AI Pulse: Automated Student Newsletter Generator

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![Build Status](https://img.shields.io/badge/build-passing-brightgreen.svg)]()
[![TCS Tech Day](https://img.shields.io/badge/TCS%20Tech%20Day-Fr.%20C.%20Rodrigues%20Institute%20of%20Technology-blueviolet)]()

An AI-powered automated content aggregation, summarization, and curation platform designed for college tech clubs. **AI Pulse** automatically gathers updates from verified public sources, filters out noise and duplicates, generates plain-language student-centric summaries with "Why It Matters" impact notes, and provides an intuitive Human-in-the-Loop review dashboard for newsletter approval.

---

## 📌 Problem Statement

College clubs often need to keep students informed about rapid developments in Artificial Intelligence and Software Engineering. However, finding relevant updates across multiple sources, checking their usefulness, summarizing them, and formatting a student-friendly newsletter requires significant manual effort.

**AI Pulse** solves this by automating:
- Data discovery across tech blogs, research summaries, and RSS feeds.
- Smart filtering & semantic de-duplication.
- Student-tailored summarization and actionable impact notes.
- Editorial review workflows for club coordinators prior to publication.

---

## ✨ Key Features

- **Multi-Source Data Ingestion:** Automatically fetches updates from pre-approved RSS feeds, tech portals, developer blogs, and academic research summaries.
- **De-Duplication & Relevance Scoring:** Uses AI semantic similarity and classification models to filter out duplicates and drop non-tech/irrelevant news.
- **Student-Centric Summarization:** Converts complex technical jargon into concise, 3-sentence plain-language summaries.
- **"Why It Matters" Impact Notes:** Explains direct relevance to software engineering skills, tools, career pathways, or practical learning.
- **Flexible Schedule Support:** Generates newsletters tailored for weekly or monthly consumption formats.
- **Human-in-the-Loop Editorial Dashboard:** Allows club coordinators to edit, reorder, add, or remove updates prior to publishing.
- **Security & Quality Guardrails:** Built-in XSS input sanitization, anti-hallucination prompts, and fallback to cached content during source downtime.

---

## 🏗 System Architecture & Workflow

```
┌─────────────────┐    ┌──────────────────┐    ┌────────────────────┐
│ Approved Feeds  │───>│ Content Ingestion│───>│ De-duplication &   │
│ & RSS Sources   │    │  & HTML Parsing  │    │ Relevance Filter   │
└─────────────────┘    └──────────────────┘    └─────────┬──────────┘
                                                         │
                                                         ▼
┌─────────────────┐    ┌──────────────────┐    ┌────────────────────┐
│ Output Channels │    │ Coordinator UI   │    │ AI Summarizer &    │
│ (Email / Web)   │<───│ Review Dashboard │<───│ "Why It Matters"   │
└─────────────────┘    └──────────────────┘    └────────────────────┘
```

---

## 📡 Predefined Approved Sources

To maintain high data quality and accuracy, AI Pulse aggregates exclusively from verified public engineering feeds:

- **Official Developer Blogs:** OpenAI Blog, Google DeepMind, Hugging Face, GitHub Engineering, AWS ML Blog.
- **Developer Portals:** daily.dev (#ai), Simon Willison’s Weblog, ByteByteGo / The Pragmatic Engineer, MarkTechPost.
- **Academic Research Summaries:** arXiv Computer Science (cs.AI), Berkeley AI Research (BAIR) Blog, MIT Tech Review.
- **Tech & Engineering News:** Hacker News Top Stories, IEEE Spectrum, Ars Technica.

*Note: Unverified social media posts and personal student data are strictly excluded.*

---

## 🚀 Getting Started

### Prerequisites

- **Python 3.10+** or **Node.js 18+**
- **LLM API Key** (OpenAI API / Gemini API / Local Ollama Instance)

### Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/your-username/ai-pulse-newsletter.git
   cd ai-pulse-newsletter
   ```

2. **Create and activate a virtual environment:**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Environment Setup:**
   Create a `.env` file in the root directory:
   ```env
   OPENAI_API_KEY=your_api_key_here
   DATABASE_URL=sqlite:///./ai_pulse.db
   ENVIRONMENT=development
   ```

5. **Run the Application:**
   ```bash
   python main.py
   ```

---

## 🧪 Testing Suite & Test Cases

AI Pulse includes a comprehensive suite of unit and integration tests to verify pipeline accuracy, edge case handling, and editorial workflows.

### Running Tests

```bash
pytest -v
```

### Key Test Scenarios Covered

| Test Case | Type | Description | Expected Outcome |
| :--- | :--- | :--- | :--- |
| **TC-01** | Normal Flow | Ingest 5 highly relevant AI articles. | System ranks all 5 and formats draft newsletter. |
| **TC-02** | Mixed Relevance | Feed containing AI, Gaming, Sports, and Tech items. | Non-tech articles (Gaming/Sports) are filtered out. |
| **TC-03** | De-duplication | Ingest identical stories from 2 different feeds. | Duplicate entry is removed; single record retained. |
| **TC-04** | Poor Quality | Ingest low-information/vague article ("AI is cool"). | Low relevance score assigned; item rejected. |
| **TC-05** | Empty Feed | Feed with zero relevant tech updates. | Graceful response: *"No relevant updates found."* |
| **TC-06** | Parsing | Raw RSS payload with 10 structured items. | All 10 extracted cleanly without field truncation. |
| **TC-07** | Summarization | Technical paper extract provided. | Produces max 3-sentence summary + "Why It Matters". |
| **TC-08** | Review Workflow | Coordinator edits, reorders, and deletes items. | Draft updates state to "Approved" with edited output. |

---

## 🛠 Tech Stack

- **Backend:** Python / FastAPI
- **AI / LLM Orchestration:** LangChain / OpenAI API / Gemini API
- **Data Parsing & Scraping:** BeautifulSoup4, Feedparser
- **Frontend / Dashboard:** React / Next.js / Tailwind CSS (or Streamlit prototype)
- **Database:** SQLite / PostgreSQL

---

## 📄 License

Distributed under the MIT License. See `LICENSE` for more information.

---

## 🤝 Acknowledgments

Developed for **TCS Tech Day @ Fr. C. Rodrigues Institute of Technology** under Theme: *AI for Education + Knowledge Sharing*.
