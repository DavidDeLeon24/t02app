# Project 2 - t02app

## Prerequisites
- Docker Engine
- Node.js and npm
- AWS SAM CLI

## 1. Run the Web Stack
cd t02app
docker compose up -d
docker compose ps
curl -s -o /dev/null -w "%{http_code}
" http://localhost:8080

## 2. Tear Down the Web Stack
docker compose down

## 3. Invoke the Serverless Function
cd local-fn
sam local invoke HelloWorldFunction
