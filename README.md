# DevOps Major Project - Flask CI/CD Pipeline

A minimal Flask web application with a complete DevOps pipeline including Docker, Nginx reverse proxy, Jenkins CI/CD, Prometheus monitoring, and Grafana dashboards.

## Project Structure

```
devops-major-1/
├── app.py                              # Flask application
├── requirements.txt                    # Python dependencies
├── Dockerfile                          # Flask app Docker image
├── Jenkinsfile                         # Jenkins CI/CD pipeline
├── docker-compose.yml                  # All services orchestration
├── jenkins/
│   └── Dockerfile                      # Custom Jenkins with Docker CLI
├── nginx/
│   ├── Dockerfile                      # Nginx reverse proxy image
│   └── nginx.conf                      # Nginx config
└── monitoring/
    └── prometheus/
        └── prometheus.yml              # Prometheus scrape config
```

## Services

| Service      | Port   | Description                          |
|-------------|--------|--------------------------------------|
| Flask App   | `5000` | Python Flask web application         |
| Nginx       | `80`   | Reverse proxy to Flask               |
| Jenkins     | `8080` | CI/CD pipeline automation            |
| Prometheus  | `9090` | Metrics collection & monitoring      |
| Grafana     | `3000` | Metrics visualization & dashboards   |

## Architecture

```
User Request → Nginx (port 80) → Flask App (port 5000)
                                      ↑
                              Prometheus (scrapes metrics)
                                      ↑
                              Grafana (visualizes metrics)

GitHub → Jenkins (CI/CD) → Docker Compose (Build & Deploy)
```

## Quick Start

### Prerequisites
- Docker
- Docker Compose

### Run Locally

```bash
# Clone the repository
git clone https://github.com/abhiramn23/Devops-major-1.git
cd Devops-major-1

# Start all services
sudo docker-compose up -d --build

# Verify all containers are running
sudo docker ps
```

### Access Services

| Service    | URL                          | Credentials             |
|-----------|------------------------------|-------------------------|
| Flask App | http://localhost:5000        | —                       |
| Nginx     | http://localhost:80          | —                       |
| Jenkins   | http://localhost:8080        | Setup on first launch   |
| Prometheus| http://localhost:9090        | —                       |
| Grafana   | http://localhost:3000        | admin / admin           |

## Jenkins Setup

1. Open http://localhost:8080
2. Get the unlock password:
   ```bash
   sudo docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
   ```
3. Paste password → Install suggested plugins → Create admin user
4. Create a new **Pipeline** job pointing to this GitHub repo
5. Set **Script Path** to `Jenkinsfile`

## Grafana Setup

1. Open http://localhost:3000 (login: `admin` / `admin`)
2. Go to **Connections → Data Sources → Add data source**
3. Choose **Prometheus** → URL: `http://prometheus:9090`
4. Click **Save & Test**
5. Create a dashboard with query: `up`

## CI/CD Pipeline

The `Jenkinsfile` defines two stages:

1. **Pull Code** — Clones the `main` branch from GitHub
2. **Build & Deploy** — Runs `docker compose down` then `docker compose up --build -d`

## Stop All Services

```bash
sudo docker-compose down
```

## Technologies Used

- **Python Flask** — Web framework
- **Docker & Docker Compose** — Containerization & orchestration
- **Nginx** — Reverse proxy
- **Jenkins** — CI/CD automation
- **Prometheus** — Monitoring & metrics
- **Grafana** — Visualization & dashboards
