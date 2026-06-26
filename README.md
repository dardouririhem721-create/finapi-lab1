# FinAPI — Lab 1 & Lab 2

## Description
API REST Python avec Flask pour récupérer des cours boursiers en temps réel,
avec pipeline ETL et stockage dans une base de données SQLite.

## Installation
```bash
git clone https://github.com/dardouririhem721-create/finapi-lab1
cd finapi-lab1
python -m venv .venv
source .venv/Scripts/activate
pip install -r requirements.txt
```

## Lancer le serveur
```bash
python -m finapi.app
```

## ETL — Ingestion des données (Lab 2)
```bash
python scripts/run_etl.py AAPL MSFT GOOGL
```

## Endpoints disponibles

### Lab 1
| Endpoint | Description |
|----------|-------------|
| GET /health | Vérification du serveur |
| GET /price/<ticker> | Dernier prix en temps réel |
| GET /history/<ticker>?days=N | Historique des prix (1-365 jours) |

### Lab 2
| Endpoint | Description |
|----------|-------------|
| GET /db/prices/<ticker> | Prix stockés en base SQLite |
| GET /db/news/<ticker> | News stockées en base SQLite |

## Exemples

```bash
# Santé du serveur
curl http://localhost:5000/health

# Dernier prix AAPL
curl http://localhost:5000/price/AAPL

# Historique 5 jours MSFT
curl http://localhost:5000/history/MSFT?days=5

# Prix stockés en base
curl http://localhost:5000/db/prices/AAPL

# News stockées en base
curl http://localhost:5000/db/news/AAPL
```

## Structure du projet
```
finapi-lab1/
├── .venv/
├── finapi/
│   ├── __init__.py
│   ├── app.py
│   ├── prices.py
│   ├── db.py
│   ├── models.py
│   └── etl/
│       ├── __init__.py
│       ├── prices_etl.py
│       └── news_etl.py
├── scripts/
│   └── run_etl.py
├── data/
│   └── finapi.db
├── tests/
├── .gitignore
├── requirements.txt
└── README.md
```

