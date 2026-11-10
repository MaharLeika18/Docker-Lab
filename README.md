# Containerize It — Docker Lab

Package the finished SecureNotes API into a Docker image, then run it together
with a Postgres database using Docker Compose. The Dockerfile, build ignore
rules, and Compose stack are implemented; `TASKS.md` contains the completed
checklist and reflection.

**Start with `TASKS.md`** — it lists every task in order with the exact commands.

The container configuration is in:
```
Dockerfile            <- Part A (TASKs A1-A5) + Part B (B1)
.dockerignore         <- Part B (B2)
docker-compose.yml    <- Part C (C1-C2)
```
The app in `app/`, `requirements.txt`, and the tests stay as given.

## Quick start
```bash
python -m venv venv && source venv/bin/activate
pip install -r requirements.txt
pytest -q

docker --version                   # need Docker Desktop running
```

To start the full stack and verify API-to-database connectivity:

```bash
docker compose up -d
curl http://localhost:8000/health/db
docker compose ps
docker compose down
```

## Accounts (the app)
| username | password  | role |
|----------|-----------|------|
| admin    | admin123  | admin |
| alice    | alicepass | owns note 1 |
| bob      | bobpass   | owns note 2 |

Keep the `bcrypt==4.0.1` pin in `requirements.txt` — newer bcrypt breaks passlib.
