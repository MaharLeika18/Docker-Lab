# Containerize It — Completed Docker Lab

## Part A — Build the image

- [x] **A1** — Use the pinned, slim `python:3.12-slim` base image.
- [x] **A2** — Set `/app` as the working directory.
- [x] **A3** — Copy `requirements.txt` and install dependencies before copying the source, preserving the dependency layer cache.
- [x] **A4** — Copy the application source into the image.
- [x] **A5** — Expose port `8000` and start Uvicorn bound to `0.0.0.0`.

## Part B — Improve the image

- [x] **B1** — Create and use the unprivileged `appuser`.
- [x] **B2** — Exclude virtual environments, Git metadata, bytecode, test artifacts, and environment files from the build context.

## Part C — Run the stack with Compose

- [x] **C1** — Build the API service, publish port `8000`, wait for the database health check, and pass `DATABASE_URL`.
- [x] **C2** — Run `postgres:16` with configured credentials, a persistent named volume, and a readiness health check.

Compose validation commands:

```powershell
pytest tests/test_dockerfile.py
pytest tests/test_compose.py
docker compose up -d
curl http://localhost:8000/health/db
docker compose ps
docker compose down
```

The expected health response is `{"database":"ok"}`. The Docker-based commands and screenshots still need to be captured in an environment with Docker running.

## Part D — Submit

- [x] Dockerfile, `.dockerignore`, `docker-compose.yml`, and this completed checklist are in the repository.
- [x] Push the completed work to the [GitHub repository](https://github.com/MaharLeika18/Docker-Lab/tree/Shekinah) on the `Shekinah` branch.
- [ ] Capture screenshots of a successful image build, `/docs` served by the container, and the API/database stack running.

## Reflection

1. **Why should the container behave the same on another operating system?**

   The image packages the application, Python runtime, and pinned dependencies together on a consistent base image. Docker runs that image with the same filesystem and runtime environment on supported hosts, avoiding differences between locally installed Python versions, packages, and operating-system configuration.

2. **Why install dependencies before copying the source code?**

   Docker caches each build layer. Requirements change less often than application code, so copying and installing them first lets Docker reuse the dependency-install layer after ordinary code edits, making rebuilds faster.
