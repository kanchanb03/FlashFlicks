# 🃏 FlashFlicks – Full-Stack Flashcard Platform  

A containerized Django application that lets learners create decks, flip through flashcards, quiz themselves, and track mastery in real time. Built to showcase clean REST-style back-end design, responsive Bootstrap front-end styling, and DevOps-friendly Docker workflows.  

---

## 💡 Key Features  
* **Deck & card management** – CRUD UI and REST endpoints for folders, decks, and individual flashcards  
* **Study modes** – flip-card carousel, multiple-choice quiz, and “mark as learned” toggles  
* **Progress analytics** – per-deck accuracy, study streaks, and global dashboard charts  
* **Responsive UI** – Bootslander (Bootstrap 5) theme + custom CSS for dark/light palettes  
* **JWT-based auth** – register / login APIs and protected routes for user-specific data  
* **Docker one-command deploy** – `docker compose up` brings up web, Postgres, and nginx in seconds  

---

## 🔧 Tech Stack  
| Layer          | Technology / Tool                               |
|----------------|-------------------------------------------------|
| Backend        | Django 4 • Django REST Framework                |
| Database       | PostgreSQL 15                                   |
| Front-end      | HTML5 • CSS3 • ES6 • Bootstrap 5 (Bootslander)  |
| Auth           | JSON Web Tokens (`djangorestframework-simplejwt`)|
| Containerization| Docker • docker-compose                        |
| CI / CD        | GitHub Actions (lint → test → build)            |
| Testing        | Pytest-Django • Coverage.py                     |
| Analytics      | Chart.js (progress graphs)                      |

---

## 🚀 Quick Start  

```bash
# 1 — Clone
git clone https://github.com/your-username/flashflicks.git
cd flashflicks

# 2 — Environment
cp .env.sample .env                 # adjust secrets if desired

# 3 — Launch (Docker)
docker compose up --build -d        # web :8000, db :5432, nginx :80

# 4 — Create superuser
docker compose exec web python manage.py createsuperuser
```

Visit **`http://localhost`** for the site or **`/api/docs/`** for browsable OpenAPI docs.  

---

## 🏗️ Architecture Overview  

```text
┌────────────┐  REST JSON   ┌──────────────┐
│  Front-end │ ───────────▶ │   Django     │
│ Bootstrap  │              │  API + HTML  │
└────────────┘              └──────┬───────┘
        ▲ static / media (nginx)    │ ORM
        │                           ▼
┌────────────┐              ┌──────────────┐
│    nginx   │◀────────────▶│  PostgreSQL  │
└────────────┘   reverse-proxy +          └──────────────┘
   TLS, caching     docker network
```

* **Django app** – `deck`, `flashcard`, `progress`, and `users` apps form a clear domain separation.  
* **nginx** – serves static assets, proxies API, and terminates HTTPS (self-signed in dev).  
* **Docker compose** – defines repeatable local / CI environments.  

---

## 📝 Usage Example  

```python
# Create a flashcard via the API
import requests, json, os

token = os.getenv("JWT")          # acquired from /api/token/
headers = {"Authorization": f"Bearer {token}"}

payload = {
    "front": "What is a closure in Python?",
    "back":  "A function that remembers the environment in which it was created.",
    "deck":  3
}

r = requests.post("http://localhost/api/cards/", 
                  headers=headers, json=payload)
print(r.status_code, r.json())
```

---

## ✅ Tests  

```bash
docker compose exec web pytest -q
```

Coverage reports appear in **`htmlcov/index.html`**.  

---

## 🤝 Contributing  
1. Fork → feature branch  
2. Run `pre-commit install` for auto-formatting (black, isort, flake8)  
3. Ensure `pytest` passes and open a PR describing **what** + **why**  

---

## 📄 License  
MIT — see **`LICENSE`**.  

---

## 🙋‍♀️ Questions?  
Open an issue or start a Discussion. Happy studying!  
