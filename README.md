🧠 Product Hunt RAG Analyzer
The Product Hunt RAG Analyzer is an AI-powered competitive intelligence system that analyzes Product Hunt competitors using Retrieval-Augmented Generation (RAG). It transforms raw Product Hunt data into actionable business insights such as feature gaps, sentiment trends, market positioning, and strategic recommendations.

Python 3.9+ License: MIT Streamlit FastAPI

📋 Overview
Product Hunt RAG Analyzer helps entrepreneurs and product managers understand the competitive landscape by analyzing Product Hunt products and their reviews. Simply describe your product idea, and the system will:

Identify Competitors: Find similar products using semantic search with FAISS vector indices
Analyze Sentiment: Understand user sentiment from reviews using transformer-based NLP
Extract Feature Gaps: Discover missing features and opportunities from user feedback
Generate Insights: Create comprehensive competitive intelligence reports using LLM (Groq API)
Provide Recommendations: Get actionable market positioning and differentiation strategies
✨ Features
Feature	Description
🔍 Semantic Search	FAISS-powered vector similarity search for competitor identification
💬 Sentiment Analysis	RoBERTa-based sentiment analysis with aspect extraction
📊 Feature Analysis	Automated feature gap detection and prioritization
🤖 LLM Generation	Groq API integration for intelligent insights generation
📈 Market Positioning	Competitive landscape analysis and saturation detection
📄 Report Generation	Export reports in JSON, Markdown, or PDF formats
🌐 REST API	FastAPI backend with OpenAPI documentation
🖥️ Web Interface	Streamlit-based interactive dashboard
⚡ CLI Tool	Command-line interface for automation and scripting
🏗️ Architecture
┌─────────────────────────────────────────────────────────────────┐                                    
│                        User Interfaces                          │
├─────────────────┬─────────────────────┬─────────────────────────┤
│  Streamlit UI   │     FastAPI REST    │         CLI             │
│  (streamlit_app)│     (src/api)       │      (src/cli.py)       │
└────────┬────────┴──────────┬──────────┴────────────┬────────────┘
         │                   │                       │
         └───────────────────┼───────────────────────┘
                             ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Analysis Pipeline (src/main.py)              │
├─────────────────────────────────────────────────────────────────┤
│  Stage 1: Competitor Identification                             │
│  Stage 2: Review Retrieval & Analysis                           │
│  Stage 3: LLM Generation                                        │
│  Stage 4: Report Generation                                     │
└─────────────────────────────────────────────────────────────────┘
                             │
         ┌───────────────────┼───────────────────────┐
         ▼                   ▼                       ▼
┌─────────────────┐ ┌─────────────────┐ ┌─────────────────────────┐
│   Embeddings    │ │    Sentiment    │ │    Feature Analysis     │
│  (MiniLM-L6)    │ │   (RoBERTa)     │ │  (Gap Detection)        │
└─────────────────┘ └─────────────────┘ └─────────────────────────┘
         │                   │                       │
         └───────────────────┼───────────────────────┘
                             ▼
┌─────────────────────────────────────────────────────────────────┐
│                    FAISS Vector Storage                         │
│              (Products Index + Reviews Index)                   │
└─────────────────────────────────────────────────────────────────┘

2.Quick review

User Idea
   ↓
Embedding
   ↓
FAISS Retrieval (Competitors)
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
🚀 Quick Start
Prerequisites
Python 3.9 or higher
Groq API Key (free tier available)
Installation
Clone the repository

git clone https://github.com/IsratJahan09/Product-Hunt-RAG-Analyzer.git
cd product-hunt-rag-analyzer
Create virtual environment

python -m venv .venv

# Windows
.venv\Scripts\activate

# Linux/macOS
source .venv/bin/activate
Install dependencies

pip install -r requirements.txt
Configure environment

# Copy example environment file
cp .env.example .env

# Edit .env and add your Groq API key
# GROQ_API_KEY=your_api_key_here
Build FAISS indices (required before first use)

python -m src.cli build-index --dataset-path dataset --output-dir data/indices
Running the Application
Option 1: Web Interface (Streamlit)
streamlit run streamlit_app/app.py
Access at: http://localhost:8501

Option 2: REST API (FastAPI)
python -m src.cli serve --host 0.0.0.0 --port 8000
API: http://localhost:8000
Docs: http://localhost:8000/docs
ReDoc: http://localhost:8000/redoc
Option 3: Command Line
python -m src.cli analyze \
    --product-idea "A task management app with AI-powered prioritization" \
    --max-competitors 5 \
    --output-format json \
    --output-file report.json
📖 Usage
CLI Commands
Command	Description
build-index	Build FAISS indices from Product Hunt dataset
analyze	Run competitive analysis for a product idea
stats	Display dataset statistics from indices
serve	Start FastAPI web service
evaluate	Run system evaluation and validation
Examples
# Build indices with IVF index type for large datasets
python -m src.cli build-index \
    --dataset-path dataset \
    --output-dir data/indices \
    --index-type ivf

# Run analysis with custom competitor count
python -m src.cli analyze \
    --product-idea "An AI-powered code review tool for developers" \
    --max-competitors 10 \
    --output-format markdown \
    --output-file analysis_report.md

# View dataset statistics
python -m src.cli stats --indices-dir data/indices

# Run full system evaluation
python -m src.cli evaluate --eval-type full --output-format html
API Endpoints
Method	Endpoint	Description
GET	/health	Health check
GET	/stats	Dataset statistics
POST	/analyze	Submit analysis request
GET	/analysis/{id}	Get analysis results
Example API Request
curl -X POST "http://localhost:8000/analyze" \
    -H "Content-Type: application/json" \
    -d '{
        "product_idea": "A collaborative whiteboard for remote teams",
        "max_competitors": 5,
        "output_format": "json"
    }'
📁 Project Structure
product-hunt-rag-analyzer/
├── config/
│   └── default_config.yaml     # Application configuration
├── data/
│   ├── indices/                # FAISS vector indices
│   ├── processed/              # Processed data files
│   └── raw/                    # Raw data files
├── dataset/
│   ├── products.jsonl          # Product Hunt products
│   ├── reviews.jsonl           # Product reviews
│   └── evaluation/             # Evaluation datasets
├── logs/                       # Application logs
├── src/
│   ├── api/                    # FastAPI REST API
│   │   ├── app.py              # FastAPI application
│   │   ├── models.py           # Pydantic models
│   │   └── routers/            # API route handlers
│   ├── evaluation/             # Evaluation framework
│   │   ├── metrics.py          # Evaluation metrics
│   │   ├── runner.py           # Evaluation runner
│   │   └── validation.py       # Validation utilities
│   ├── modules/                # Core analysis modules
│   │   ├── embeddings.py       # Embedding generation
│   │   ├── feature_analysis.py # Feature extraction
│   │   ├── llm_generation.py   # LLM integration
│   │   ├── positioning_analysis.py # Market positioning
│   │   ├── preprocessing.py    # Text preprocessing
│   │   ├── rag_retrieval.py    # RAG retrieval logic
│   │   ├── report_generation.py # Report generation
│   │   ├── sentiment.py        # Sentiment analysis
│   │   └── vector_storage.py   # FAISS index management
│   ├── utils/                  # Utility modules
│   │   ├── config.py           # Configuration management
│   │   ├── dataset_loader.py   # Dataset loading
│   │   ├── index_builder.py    # Index building utilities
│   │   ├── logger.py           # Logging utilities
│   │   └── rate_limiter.py     # API rate limiting
│   ├── cli.py                  # Command-line interface
│   └── main.py                 # Main analysis pipeline
├── streamlit_app/              # Streamlit web interface
│   ├── app.py                  # Main Streamlit app
│   ├── components/             # UI components
│   ├── pages/                  # Multi-page app pages
│   └── utils/                  # Frontend utilities
├── .env.example                # Environment variables template
├── Makefile                    # Build automation
├── requirements.txt            # Python dependencies
├── ProductHunt_RAG_Finetuning.ipynb           
└── setup.py                    # Package setup
⚙️ Configuration
Configuration is managed via config/default_config.yaml. Key settings:

# Model Configuration
models:
  embedding:
    name: "all-MiniLM-L6-v2"    # Sentence transformer model
    device: "cpu"                # cpu or cuda
  
  sentiment:
    name: "cardiffnlp/twitter-roberta-base-sentiment-latest"
    
  llm:
    provider: "groq"
    model: "llama-3.3-70b-versatile"
    temperature: 0.7
    max_tokens: 3000

# Retrieval Configuration
retrieval:
  max_competitors: 5
  reviews_per_competitor: 10
  min_similarity_threshold: 0.5

# FAISS Index Configuration
storage:
  faiss:
    index_type: "flat"          # flat, ivf, or hnsw
Environment Variables
Variable	Description	Default
GROQ_API_KEY	Groq API key for LLM	Required
FASTAPI_HOST	API server host	0.0.0.0
FASTAPI_PORT	API server port	8000
LOG_LEVEL	Logging level	INFO
INDICES_DIR	FAISS indices directory	./data/indices
🧪 Testing
# Run all tests with coverage
pytest tests/ -v --cov=src --cov-report=html

# Run specific test module
pytest tests/test_embeddings.py -v

# Run with verbose output
make test
📊 Evaluation
The system includes a comprehensive evaluation framework:

# Full system evaluation
python -m src.cli evaluate --eval-type full --output-format html

# Retrieval quality evaluation
python -m src.cli evaluate --eval-type retrieval

# Sentiment analysis evaluation
python -m src.cli evaluate --eval-type sentiment

# Feature gap detection evaluation
python -m src.cli evaluate --eval-type feature_gaps
🛠️ Development
Using Makefile
make help          # Show available commands
make install       # Install dependencies
make setup         # Set up environment
make build-index   # Build FAISS indices
make run-api       # Start FastAPI server
make run-cli       # Run CLI example
make test          # Run tests
make clean         # Clean generated files
make quickstart    # Full setup + build indices
Code Quality
# Format code
make format

# Lint code
make lint

# Type checking
make type-check
🔧 Troubleshooting
Common Issues
1. FAISS indices not found

# Build indices first
python -m src.cli build-index --dataset-path dataset --output-dir data/indices
2. Groq API connection error

Verify your API key in .env
Check internet connectivity
Ensure API key has sufficient quota
3. Out of memory during embedding generation

Reduce batch size in config: processing.embedding_batch_size: 16
Use CPU instead of GPU: models.embedding.device: "cpu"
4. Slow analysis performance

Use IVF or HNSW index types for large datasets
Enable GPU acceleration if available
Reduce reviews_per_competitor in config
📄 License
This project is licensed under the MIT License - see the LICENSE file for details.

🤝 Contributing
Contributions are welcome! Please feel free to submit a Pull Request.

Fork the repository
Create your feature branch (git checkout -b feature/AmazingFeature)
Commit your changes (git commit -m 'Add some AmazingFeature')
Push to the branch (git push origin feature/AmazingFeature)
Open a Pull Request
📬 Contact
For questions or feedback, please open an issue on GitHub.

Built with ❤️ using Python, FastAPI, Streamlit, and Groq
