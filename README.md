# 🛡️ SecureGuard AI — Intelligent Web Application Firewall

> An AI-powered Web Application Firewall that detects and explains security threats in real-time using Machine Learning and Large Language Models.

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-000000?style=for-the-badge&logo=flask&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2CA5E0?style=for-the-badge&logo=docker&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=for-the-badge&logo=github-actions&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)
![JWT](https://img.shields.io/badge/JWT-000000?style=for-the-badge&logo=JSON%20web%20tokens&logoColor=white)

---

## 🔍 What is SecureGuard AI?

Traditional WAFs block threats using static rules — they fail against novel or evolving attacks. SecureGuard AI uses a trained **Random Forest classifier** to detect malicious HTTP requests (SQL Injection, XSS) based on learned patterns, and integrates the **Gemini LLM** to generate human-readable threat explanations — turning raw alerts into actionable analyst insights.

---

## ✨ Features

- 🔴 **Real-time threat detection** — Analyzes incoming HTTP requests and flags SQL Injection and XSS attacks instantly
- 🤖 **AI-powered explanations** — Gemini LLM explains *why* a request was flagged in plain English
- 🔐 **JWT Authentication** — Secure dashboard access with token expiry and role-based control
- 📊 **Live monitoring dashboard** — Real-time request logs, threat timeline, and attack type breakdown
- 🐳 **Fully containerized** — Docker setup for one-command deployment
- ⚙️ **CI/CD pipeline** — Automated testing and deployment via GitHub Actions

---

## 🏗️ Architecture

```
Incoming HTTP Request
        │
        ▼
┌───────────────┐
│  Flask Server  │  ← Intercepts and routes requests
└──────┬────────┘
       │
       ▼
┌───────────────┐
│  ML Classifier │  ← Random Forest (F1: 93%)
│  (scikit-learn)│    Detects SQLi / XSS patterns
└──────┬────────┘
       │
  ┌────┴────┐
  │         │
SAFE     MALICIOUS
  │         │
  ▼         ▼
Allow    ┌──────────────┐
Request  │  Gemini LLM  │  ← Generates threat explanation
         └──────┬───────┘
                │
                ▼
         ┌─────────────┐
         │  Dashboard  │  ← JWT-protected, real-time logs
         └─────────────┘
```

---

## 🚀 Getting Started

### Prerequisites
- Python 3.9+
- Docker
- Gemini API key ([get one here](https://makersuite.google.com/))

### Run with Docker (Recommended)

```bash
git clone https://github.com/rachel/secureguard-ai.git
cd secureguard-ai
cp .env.example .env        # Add your Gemini API key
docker-compose up --build
```

Visit `http://localhost:5000`

### Run Locally

```bash
git clone https://github.com/rachel/secureguard-ai.git
cd secureguard-ai
python -m venv venv
source venv/bin/activate    # Windows: venv\Scripts\activate
pip install -r requirements.txt
python app.py
```

---

## 🧠 Model Performance

| Metric | Score |
|--------|-------|
| F1-Score | 93% |
| Precision | 94% |
| Recall | 92% |
| Dataset | SQL Injection Dataset (Kaggle) |

Trained on 50K+ HTTP request samples. Model detects:
- **SQL Injection** — pattern-based and obfuscated variants
- **Cross-Site Scripting (XSS)** — reflected and stored XSS payloads

---

## 📁 Project Structure

```
secureguard-ai/
├── app.py                  # Flask application entry point
├── model/
│   ├── train.py            # Model training script
│   ├── classifier.pkl      # Trained Random Forest model
│   └── vectorizer.pkl      # Feature vectorizer
├── auth/
│   └── jwt_handler.py      # JWT authentication logic
├── templates/
│   └── dashboard.html      # Monitoring dashboard
├── static/                 # CSS and JS assets
├── .github/
│   └── workflows/
│       └── deploy.yml      # GitHub Actions CI/CD
├── Dockerfile
├── docker-compose.yml
├── requirements.txt
└── README.md
```

---

## 🔐 Authentication

Dashboard access is protected via JWT:

```bash
# Get token
POST /auth/login
{ "username": "admin", "password": "your_password" }

# Access protected routes
GET /dashboard
Headers: { "Authorization": "Bearer <token>" }
```

Tokens expire after 24 hours. Refresh tokens supported.

---

## ⚙️ CI/CD Pipeline

Every push to `main` triggers:
1. ✅ Unit tests via `pytest`
2. ✅ Model validation (F1 threshold check)
3. ✅ Docker image build
4. ✅ Deployment

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Backend | Python, Flask |
| ML Model | scikit-learn (Random Forest) |
| LLM Integration | Google Gemini API |
| Authentication | JWT (PyJWT) |
| Containerization | Docker, Docker Compose |
| CI/CD | GitHub Actions |
| Database | SQLite (request logs) |
| Frontend | HTML, CSS, Jinja2 |

---

## 📌 Why This Project?

Rule-based WAFs fail against:
- Novel attack patterns not in their ruleset
- Obfuscated payloads that bypass signature matching
- Zero-day variants of known attacks

SecureGuard AI learns from patterns rather than rules — making it adaptive. The LLM explanation layer bridges the gap between automated detection and human analyst understanding, a core challenge in real-world SOC environments.

---

## 🗺️ Roadmap

- [ ] Add Command Injection and Path Traversal detection
- [ ] Integrate SIEM alerting (Slack / email webhooks)
- [ ] Rate limiting and IP reputation scoring
- [ ] Deploy to AWS EC2 with public demo

---

## 👩‍💻 Author

**Rachel Mariam Koshy**

This is a proof-of-concept project built for learning purposes. 


