# 🧠 Product Hunt RAG Analyzer

The **Product Hunt RAG Analyzer** is an AI-powered competitive intelligence system that analyzes Product Hunt competitors using **Retrieval-Augmented Generation (RAG)**.

It transforms raw Product Hunt data into actionable business insights such as:

* Feature gaps
* Sentiment trends
* Market positioning
* Strategic recommendations

![Python](https://img.shields.io/badge/Python-3.9+-blue)
![License](https://img.shields.io/badge/License-MIT-green)
![Streamlit](https://img.shields.io/badge/Frontend-Streamlit-red)
![FastAPI](https://img.shields.io/badge/API-FastAPI-teal)

---

# 📋 Overview

Product Hunt RAG Analyzer helps entrepreneurs and product managers understand the competitive landscape by analyzing Product Hunt products and their reviews.

Simply describe your product idea, and the system will:

* 🔍 Identify competitors using semantic similarity search
* 💬 Analyze customer sentiment from reviews
* 📊 Detect feature gaps and opportunities
* 🤖 Generate AI-powered competitive insights
* 📈 Provide market positioning strategies
* 📄 Export structured intelligence reports

---

# ✨ Features

| Feature               | Description                            |
| --------------------- | -------------------------------------- |
| 🔍 Semantic Search    | FAISS-powered vector similarity search |
| 💬 Sentiment Analysis | RoBERTa-based sentiment analysis       |
| 📊 Feature Analysis   | Automated feature gap detection        |
| 🤖 LLM Generation     | Groq API integration                   |
| 📈 Market Positioning | Competitive landscape analysis         |
| 📄 Report Generation  | Export JSON, Markdown, and PDF reports |
| 🌐 REST API           | FastAPI backend with OpenAPI docs      |
| 🖥️ Web Interface     | Interactive Streamlit dashboard        |
| ⚡ CLI Tool            | Command-line automation support        |

---

# 🏗️ Architecture

```text
┌─────────────────────────────────────────────────────────────┐
│                     User Interfaces                         │
├─────────────────┬───────────────────┬──────────────────────┤
│   Streamlit UI  │   FastAPI REST    │         CLI          │
│ (streamlit_app) │     (src/api)     │     (src/cli.py)     │
└────────┬────────┴────────┬──────────┴──────────┬───────────┘
         │                 │                     │
         └─────────────────┼─────────────────────┘
                           ▼
┌─────────────────────────────────────────────────────────────┐
│                 Analysis Pipeline (src/main.py)             │
├─────────────────────────────────────────────────────────────┤
│ Stage 1: Competitor Identification                          │
│ Stage 2: Review Retrieval & Analysis                        │
│ Stage 3: LLM Generation                                     │
│ Stage 4: Report Generation                                  │
└─────────────────────────────────────────────────────────────┘
                           │
        ┌──────────────────┼───────────────────┐
        ▼                  ▼                   ▼
┌───────────────┐ ┌───────────────┐ ┌──────────────────────┐
│  Embeddings   │ │   Sentiment   │ │  Feature Analysis    │
│ (MiniLM-L6)   │ │   (RoBERTa)   │ │   (Gap Detection)    │
└───────────────┘ └───────────────┘ └──────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│                  FAISS Vector Storage                       │
│          (Products Index + Reviews Index)                  │
└─────────────────────────────────────────────────────────────┘
```

---

# ⚡ Quick Workflow

```text
User Idea
   ↓
Embedding
   ↓
FAISS Retrieval
   ↓
Review Retrieval
   ↓
Sentiment + Feature Analysis
   ↓
LLM (RAG Context)
   ↓
Strategic Insights
   ↓
Structured Report
```

---

# 🚀 Quick Start

## Prerequisites

* Python 3.9+
* Groq API Key

---

# 📦 Installation

## Clone Repository

```bash
git clone https://github.com/FariaFerdous75/Product-Hunt-RAG-Analyzer.git
cd Product-Hunt-RAG-Analyzer
```

---

## Create Virtual Environment

### Windows

```bash
python -m venv .venv
.venv\Scripts\activate
```

### Linux/macOS

```bash
python -m venv .venv
source .venv/bin/activate
```

---

## Install Dependencies

```bash
pip install -r requirements.txt
```

---

## Configure Environment

Create `.env` file:

```env
GROQ_API_KEY=your_api_key_here
```

---

## Build FAISS Indices

```bash
python -m src.cli build-index --dataset-path dataset --output-dir data/indices
```

---

# ▶️ Running the Application

## Option 1 — Streamlit UI

```bash
streamlit run streamlit_app/app.py
```

Access:

```text
http://localhost:8501
```

---

## Option 2 — FastAPI Server

```bash
python -m src.cli serve --host 0.0.0.0 --port 8000
```

API:

```text
http://localhost:8000
```

Docs:

```text
http://localhost:8000/docs
```

---

## Option 3 — CLI

```bash
python -m src.cli analyze \
--product-idea "AI-powered task manager" \
--max-competitors 5 \
--output-format json
```

---

# 📖 Usage

## Build Index

```bash
python -m src.cli build-index \
--dataset-path dataset \
--output-dir data/indices
```

---

## Run Analysis

```bash
python -m src.cli analyze \
--product-idea "AI-powered code review tool" \
--max-competitors 10 \
--output-format markdown
```

---

## View Statistics

```bash
python -m src.cli stats --indices-dir data/indices
```

---

# 🌐 API Endpoints

| Method | Endpoint         | Description             |
| ------ | ---------------- | ----------------------- |
| GET    | `/health`        | Health check            |
| GET    | `/stats`         | Dataset statistics      |
| POST   | `/analyze`       | Submit analysis request |
| GET    | `/analysis/{id}` | Retrieve analysis       |

---

# 📁 Project Structure

```text
product-hunt-rag-analyzer/
│
├── config/
├── data/
├── dataset/
├── logs/
├── src/
│   ├── api/
│   ├── evaluation/
│   ├── modules/
│   ├── utils/
│   ├── cli.py
│   └── main.py
│
├── streamlit_app/
├── requirements.txt
├── setup.py
└── README.md
```

---

# ⚙️ Configuration

Example configuration:

```yaml
models:
  embedding:
    name: "all-MiniLM-L6-v2"

  sentiment:
    name: "cardiffnlp/twitter-roberta-base-sentiment-latest"

  llm:
    provider: "groq"
    model: "llama-3.3-70b-versatile"
```

---

# 🧪 Testing

Run all tests:

```bash
pytest tests/ -v
```

Coverage report:

```bash
pytest tests/ --cov=src --cov-report=html
```

---

# 🛠️ Development

## Useful Commands

```bash
make install
make build-index
make run-api
make test
make clean
```

---

# 🔧 Troubleshooting

## FAISS Indices Not Found

```bash
python -m src.cli build-index --dataset-path dataset --output-dir data/indices
```

---

## Groq API Error

* Verify API key
* Check internet connection
* Ensure API quota is available

---

## Memory Issues

Reduce batch size in config:

```yaml
processing:
  embedding_batch_size: 16
```

---

# 📄 License

This project is licensed under the **MIT License**.

---

# 🤝 Contributing

Contributions are welcome.

Steps:

1. Fork the repository
2. Create feature branch
3. Commit changes
4. Push branch
5. Open Pull Request

---

# 📬 Contact

For questions or suggestions, open an issue on GitHub.

---

# ❤️ Built With

* Python
* FastAPI
* Streamlit
* FAISS
* Groq API
* HuggingFace Transformers
