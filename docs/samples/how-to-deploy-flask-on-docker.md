# Deploy a Flask App in Docker

!!! note
    Sample how-to. Short, task-focused, and testable.

## Prerequisites
- Docker installed
- Python 3.9+

## Steps
1. Create files:
    ```bash
    mkdir flask-docker && cd flask-docker
    echo "from flask import Flask; app = Flask(__name__); @app.get('/')\ndef home(): return 'Hello, Docker!'" > app.py
    echo "Flask==3.0.0" > requirements.txt
    ```
2. Add a `Dockerfile`:
    ```dockerfile
    FROM python:3.12-slim
    WORKDIR /app
    COPY requirements.txt .
    RUN pip install -r requirements.txt
    COPY . .
    EXPOSE 5000
    CMD ["python", "app.py"]
    ```
3. Build and run:
    ```bash
    docker build -t flask-demo .
    docker run -p 5000:5000 flask-demo
    ```
4. Visit `http://localhost:5000`

## Troubleshooting
- If the container exits, check logs:
    ```bash
    docker logs <container_id>
    ```
