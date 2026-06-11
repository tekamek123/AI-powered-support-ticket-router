# 🎫 AI-Powered Support Ticket Router

> Automatically classify and route customer support tickets to the right team — instantly, accurately, and at scale.

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python)](https://python.org)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.111-009688?logo=fastapi)](https://fastapi.tiangolo.com)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)
[![Linter: flake8](https://img.shields.io/badge/linter-flake8-blue)](https://flake8.pycqa.org)

---

## 📋 Table of Contents

- [Problem Statement](#-problem-statement)
- [Solution Overview](#-solution-overview)
- [Architecture](#-architecture)
- [Project Structure](#-project-structure)
- [Tech Stack](#-tech-stack)
- [Setup & Installation](#-setup--installation)
- [Usage](#-usage)
- [Running Tests](#-running-tests)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🚨 Problem Statement

Customer support teams are overwhelmed with incoming tickets from multiple channels (email, chat, web forms). Manually triaging and routing these tickets leads to:

- ⏳ **Slow response times** — agents waste time reading and re-assigning tickets
- ❌ **Mis-routing** — tickets sent to the wrong team, causing frustration and delays
- 📉 **Inconsistent prioritization** — urgent issues get buried under low-priority requests
- 🔁 **High operational cost** — human triage is not scalable as ticket volume grows

### Example Scenario

| Incoming Ticket                  | Expected Team         | Without AI Router                            |
| -------------------------------- | --------------------- | -------------------------------------------- |
| _"My payment was charged twice"_ | 💳 Billing            | Goes to General Support → re-routed manually |
| _"App crashes on login"_         | 🛠️ Engineering        | Goes to Billing → re-routed again            |
| _"How do I reset my password?"_  | 📚 Self-Service / FAQ | Occupies a live agent unnecessarily          |

---

## 💡 Solution Overview

This system uses **Natural Language Processing (NLP)** to:

1. **Classify** each ticket into a category (e.g. `billing`, `technical`, `account`, `general`)
2. **Detect urgency** level (`low` / `medium` / `high` / `critical`)
3. **Route** the ticket to the appropriate team or agent queue automatically
4. **Expose** the logic via a **REST API** so it can be integrated with any helpdesk (Zendesk, Freshdesk, Jira Service Desk, etc.)

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                        CLIENT / HELPDESK                        │
│              (Zendesk · Freshdesk · Custom UI · cURL)           │
└───────────────────────────┬─────────────────────────────────────┘
                            │  POST /api/v1/tickets/route
                            ▼
┌─────────────────────────────────────────────────────────────────┐
│                        FastAPI Layer                            │
│   • Request validation (Pydantic)                               │
│   • Auth middleware                                             │
│   • /health  /docs  /api/v1/tickets/route                       │
└────────────────┬──────────────────────────┬─────────────────────┘
                 │                          │
                 ▼                          ▼
┌───────────────────────┐      ┌────────────────────────────┐
│   Classifier Module   │      │     Router Module          │
│                       │      │                            │
│  • Text pre-processing│      │  • Routing rules engine    │
│  • NLP model inference│─────▶│  • Priority scoring        │
│  • Category + confidence     │  • Agent / queue selection │
│    score output       │      │  • Escalation logic        │
└───────────────────────┘      └────────────────────────────┘
          │
          ▼
┌─────────────────────────────┐
│       ML Model Layer        │
│                             │
│  Option A: scikit-learn     │
│    (TF-IDF + LogisticReg)   │
│                             │
│  Option B: Transformers     │
│    (DistilBERT fine-tuned)  │
└─────────────────────────────┘
```

> 📌 **Architecture diagram placeholder** — A visual diagram (PNG/SVG) will be added here once the system is fully implemented.

---

## 📁 Project Structure

```
aI-powered-support-ticket-router/
│
├── src/                        # Application source code
│   ├── __init__.py
│   ├── classifier/             # NLP classification logic
│   │   └── __init__.py
│   ├── router/                 # Routing engine
│   │   └── __init__.py
│   └── api/                    # FastAPI app & endpoints
│       └── __init__.py
│
├── tests/                      # Unit & integration tests
│   └── __init__.py
│
├── data/
│   ├── raw/                    # Original, unprocessed datasets
│   └── processed/              # Cleaned & feature-engineered data
│
├── config/                     # YAML/JSON config files
├── notebooks/                  # Jupyter notebooks for EDA & experiments
│
├── .env.example                # Environment variable template
├── .flake8                     # Flake8 linter configuration
├── .gitignore                  # Git ignore rules
├── .pre-commit-config.yaml     # Pre-commit hooks (black + flake8)
├── pyproject.toml              # Black formatter & pytest config
├── requirements.txt            # Production dependencies
├── requirements-dev.txt        # Development/tooling dependencies
├── LICENSE                     # MIT License
└── README.md                   # This file
```

---

## 🛠️ Tech Stack

| Layer         | Technology                                         |
| ------------- | -------------------------------------------------- |
| Language      | Python 3.10+                                       |
| Web Framework | FastAPI + Uvicorn                                  |
| ML / NLP      | scikit-learn · Hugging Face Transformers · PyTorch |
| Data Handling | pandas · numpy                                     |
| Validation    | Pydantic v2                                        |
| Logging       | Loguru                                             |
| Testing       | pytest + pytest-asyncio                            |
| Code Quality  | Black · Flake8 · pre-commit                        |

---

## ⚙️ Setup & Installation

### Prerequisites

- Python **3.10+** installed
- `git` installed
- (Optional) A virtual environment manager

### 1 — Clone the repository

```bash
git clone https://github.com/tekamek123/AI-powered-support-ticket-router.git
cd aI-powered-support-ticket-router
```

### 2 — Create and activate a virtual environment

```bash
# Create
python -m venv venv

# Activate
# Windows
venv\Scripts\activate
# macOS / Linux
source venv/bin/activate
```

### 3 — Install dependencies

```bash
# Production dependencies
pip install -r requirements.txt

# Development dependencies (includes black, flake8, pre-commit)
pip install -r requirements-dev.txt
```

### 4 — Configure environment variables

```bash
# Copy the example file
cp .env.example .env

# Edit .env and fill in your values
```

### 5 — Install pre-commit hooks

```bash
pre-commit install
```

### 6 — Run the API server

```bash
uvicorn src.api.main:app --reload
```

The API will be available at **http://localhost:8000**
Interactive docs at **http://localhost:8000/docs**

---

## 🚀 Usage

### Route a ticket via the API

```bash
curl -X POST http://localhost:8000/api/v1/tickets/route \
  -H "Content-Type: application/json" \
  -d '{
    "subject": "Payment charged twice",
    "body": "I was billed twice for my subscription this month. Order #12345.",
    "channel": "email"
  }'
```

### Example Response

```json
{
  "ticket_id": "TKT-20260611-001",
  "category": "billing",
  "priority": "high",
  "confidence": 0.94,
  "assigned_team": "Billing Support",
  "routing_reason": "Detected duplicate charge complaint with high confidence"
}
```

---

## 🧪 Running Tests

```bash
# Run all tests
pytest

# Run with coverage report
pytest --cov=src --cov-report=term-missing

# Run a specific test file
pytest tests/test_classifier.py -v
```

---

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/your-feature-name`
3. Make your changes and ensure all hooks pass: `pre-commit run --all-files`
4. Commit your changes using the project commit convention
5. Push and open a Pull Request

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.
