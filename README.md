# Docker Demo - Spring Boot Java Application
Dieses Projekt demonstriert eine einfache Spring Boot-Anwendung, die mit Docker containerisiert wurde und automatisierte CI/CD-Pipelines für die Veröffentlichung auf GitHub Container Registry (GHCR) und Docker Hub nutzt.

## Projektstruktur
* `src/main/java`: Enthält die Spring Boot Anwendung mit einem einfachen REST-Controller.
* `Dockerfile`: Multi-Stage Build zur Erstellung eines optimierten Java 24 Images.
* `docker-compose.yml`: Konfiguration zum lokalen Bauen und Starten des Containers.
* `.github/workflows/`: GitHub Action Workflows für das automatisierte Deployment.

## Voraussetzungen
- Docker  & Docker Compose

## Klonen
```bash
git clone https://github.com/laulaobm/docker-demo.git
cd DockerDemo
```

## Lokal Starten
Lokal kann das Projekt mit Docker und Docker Compose gestartet werden.

### Docker
Das Projekt nutzt einen Multi-Stage Build und baut zuerst die .jar um die Spring Boot App dann auf Port 8080 zu exposen.
```bash
docker build -t docker-spring-demo .
 docker run -d --name docker-spring-app -p 8080:8080 docker-spring-demo
```

### Docker Compose
Die docker-compose.yml demonstriert eine schmale Integrierung eines Containers mithilfe der Dockerfile.
```bash
docker compose up -d
```

## CI/CD Pipeline
Das Projekt enthält 2 GitHub Actions für das Deployment.

### GitHub Container Registry (GHCR)
* `Workflow`: .github/workflows/docker-ghcr-publish.yml
* `Ziel`: ghcr.io/${{ github.repository_owner }}/docker-spring-demo
* `Auth`: Nutzt das automatische ${{ secrets.GITHUB_TOKEN }}.

### DockerHub
* `Workflow`: .github/workflows/docker-hub-publish.yml
* `Ziel`: YOUR_DOCKERHUB_USER/docker-spring-demo
* `Voraussetzung`: Du musst DOCKERHUB_USERNAME und DOCKERHUB_TOKEN in deinen GitHub Repository Secrets hinterlegen. (Erstellung in TUT Folien kurz beschrieben)

### Tagging
Beide Pipelines folgen dieser Logik:
- Push auf main: Erzeugt das Tag :latest.
- Git Tag (z.B. v1.0.0): Erzeugt ein entsprechendes Image-Tag (z.B. :v1.0.0).







