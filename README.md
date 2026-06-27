# FinAPI — Financial Sentiment Analysis Engine

> **Python · Flask · FinBERT · SQLite · Hugging Face Transformers**

A production-ready REST API that fetches real-time stock prices and financial news,
stores them in a SQLite database, and enriches them with AI-powered sentiment analysis
using FinBERT — a Transformer model fine-tuned on 4.9 billion financial tokens.

---

## Author

**Rihem Dardouri**
Master en Économie et Finance Quantitative
École Polytechnique de Tunisie

---

## Project Roadmap

| Lab | Theme | Technologies | Status |
|-----|-------|-------------|--------|
| Lab 1 | REST API — Real-time stock prices | Flask · yfinance | ✅ Done |
| Lab 2 | ETL Pipeline — Data storage | SQLAlchemy · SQLite | ✅ Done |
| Lab 3 | NLP — Financial sentiment analysis | FinBERT · Transformers | ✅ Done |

---

## Installation

git clone https://github.com/dardouririhem721-create/finapi-lab1
cd finapi-lab1
python -m venv .venv
source .venv/Scripts/activate
pip install -r requirements.txt
pip install -e .

---

## Quick Start

python scripts/run_etl.py AAPL MSFT GOOGL
python scripts/enrich_sentiment.py
python -m finapi.app

Server runs at http://localhost:5000

---

## 📡 API Endpoints

### Lab 1 — Real-time Market Data

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | /health | Server health check |
| GET | /price/<ticker> | Latest closing price |
| GET | /history/<ticker>?days=N | Price history (1–365 days) |

### Lab 2 — Database

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | /db/prices/<ticker> | Stored prices from SQLite |
| GET | /db/news/<ticker> | Stored news from SQLite |

### Lab 3 — FinBERT Sentiment Analysis

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | /sentiment | Analyze sentiment of a single text |
| POST | /sentiment/batch | Analyze up to 100 texts at once |
| GET | /db/sentiment-summary/<ticker> | Sentiment distribution for a ticker |

---

##  Usage Examples

curl http://localhost:5000/health

curl http://localhost:5000/price/AAPL

curl "http://localhost:5000/history/MSFT?days=5"

curl http://localhost:5000/db/prices/AAPL

curl http://localhost:5000/db/news/AAPL

curl -X POST http://localhost:5000/sentiment -H "Content-Type: application/json" -d "{\"text\": \"Apple stock soared after earnings beat expectations.\"}"

curl -X POST http://localhost:5000/sentiment/batch -H "Content-Type: application/json" -d "{\"texts\": [\"Apple stock soared after blockbuster earnings\", \"Tesla missed estimates, shares plunge\", \"The Fed kept interest rates unchanged\"]}"

curl http://localhost:5000/db/sentiment-summary/AAPL

---

##  Database Migration

python -c "from finapi.db import init_db; init_db()"
python scripts/run_etl.py AAPL MSFT GOOGL
python scripts/enrich_sentiment.py

---

##  Project Structure

finapi-lab1/
│
├── finapi/
│   ├── __init__.py
│   ├── app.py
│   ├── prices.py
│   ├── db.py
│   ├── models.py
│   ├── sentiment.py
│   └── etl/
│       ├── __init__.py
│       ├── prices_etl.py
│       └── news_etl.py
│
├── scripts/
│   ├── run_etl.py
│   └── enrich_sentiment.py
│
├── data/
│   └── finapi.db
│
├── tests/
├── pyproject.toml
├── requirements.txt
└── README.md

---

## About FinBERT

FinBERT is a BERT model fine-tuned on financial corpora (analyst reports, Reuters, Bloomberg).
It classifies text into positive, neutral, or negative sentiment with high accuracy
on financial jargon such as "beat estimates", "guidance raised", or "missed targets".

Model: ProsusAI/finbert on Hugging Face

---

Document pédagogique — ITBS · SMARTLab ISG Tunis