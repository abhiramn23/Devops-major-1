# Flask Hello World App

A simple beginner-friendly Flask application.

## Run Locally

```bash
pip install -r requirements.txt
python3 app.py
```

Open http://127.0.0.1:5000 in your browser.

## Run with Docker

```bash
docker build -t flask-app .
docker run -p 5000:5000 flask-app
```
