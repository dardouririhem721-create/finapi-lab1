# FinAPI — Lab 1, Lab 2 & Lab 3

## Description

API REST Python avec Flask pour récupérer des cours boursiers en temps réel,
avec pipeline ETL, stockage SQLite et analyse de sentiment financier via FinBERT.

## Installation

git clone https://github.com/dardouririhem721-create/finapi-lab1
cd finapi-lab1
python -m venv .venv
source .venv/Scripts/activate
pip install -r requirements.txt
pip install -e .

## Lancer le serveur

python -m finapi.app

## ETL — Ingestion des données

python scripts/run_etl.py AAPL MSFT GOOGL

## Enrichissement sentiment (Lab 3)

python scripts/enrich_sentiment.py

## Migration DB (Lab 3)

Après modification du schéma, supprimer et recréer la base :

python -c "from finapi.db import init_db; init_db()"
python scripts/run_etl.py AAPL MSFT GOOGL
python scripts/enrich_sentiment.py

## Endpoints disponibles

### Lab 1

| Endpoint | Méthode | Description |
|----------|---------|-------------|
| /health | GET | Vérification du serveur |
| /price/<ticker> | GET | Dernier prix en temps réel |
| /history/<ticker>?days=N | GET | Historique des prix (1-365 jours) |

### Lab 2

| Endpoint | Méthode | Description |
|----------|---------|-------------|
| /db/prices/<ticker> | GET | Prix stockés en base SQLite |
| /db/news/<ticker> | GET | News stockées en base SQLite |

### Lab 3

| Endpoint | Méthode | Description |
|----------|---------|-------------|
| /sentiment | POST | Analyse le sentiment d'un texte unique |
| /sentiment/batch | POST | Analyse jusqu'à 100 textes en une requête |
| /db/sentiment-summary/<ticker> | GET | Résumé des sentiments par ticker |

## Exemples curl

# Santé du serveur
curl http://localhost:5000/health

# Dernier prix AAPL
curl http://localhost:5000/price/AAPL

# Historique 5 jours MSFT
curl "http://localhost:5000/history/MSFT?days=5"

# Prix stockés en base
curl http://localhost:5000/db/prices/AAPL

# News stockées en base
curl http://localhost:5000/db/news/AAPL

# Analyse de sentiment (texte unique)
curl -X POST http://localhost:5000/sentiment -H "Content-Type: application/json" -d "{\"text\": \"Apple stock soared after earnings beat expectations.\"}"

# Analyse de sentiment (batch)
curl -X POST http://localhost:5000/sentiment/batch -H "Content-Type: application/json" -d "{\"texts\": [\"Apple stock soared\", \"Tesla missed estimates\", \"Fed kept rates unchanged\"]}"

# Résumé sentiment AAPL
curl http://localhost:5000/db/sentiment-summary/AAPL

## Structure du projet

finapi-lab1/
├── .venv/
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
├── scripts/
│   ├── run_etl.py
│   └── enrich_sentiment.py
├── data/
│   └── finapi.db
├── tests/
├── pyproject.toml
├── .gitignore
├── requirements.txt
└── README.md

## Auteur

Rihem Dardouri — ITBS · Master Finance Quantitative