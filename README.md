# Project 2 - t02app

## Prerequisites
- Docker Engine (or Docker Desktop)
- Node.js and npm
- AWS SAM CLI

## 1. Run the Web Stack
```bash
cd t02app
docker compose up -d
docker compose ps
curl -s -o /dev/null -w "%{http_code}\n" http://localhost:8080
