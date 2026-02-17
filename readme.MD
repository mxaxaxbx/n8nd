# n8n Docker Setup

This repository contains a Docker setup to run [n8n](https://n8n.io/) — an extendable workflow automation tool.

## 🐳 Docker Setup

This setup builds a container using the official `n8nio/n8n:latest` image, with basic authentication enabled and PostgreSQL as the database.

### 📁 Project Structure

```
.
├── Dockerfile
├── .env
├── docker-compose.yml
└── README.md

````

## ⚙️ Environment Variables

Add your environment variables in a `.env` file:

```env
# Required
DB_TYPE=postgres
DB_POSTGRESDB_URL=postgres://user:pass@your-host.com:5432/postgres

# Optional: Basic Auth
N8N_BASIC_AUTH_ACTIVE=true
N8N_BASIC_AUTH_USER=<adminuser>
N8N_BASIC_AUTH_PASSWORD=<adminpassword>

# Optional: Port
PORT=8080
````

> Replace `user`, `pass`, `your-host.com`, and `<adminuser>/<adminpassword>` with your actual credentials.

## 📦 Dockerfile

```Dockerfile
FROM n8nio/n8n:latest

ENV PORT=8080
ENV N8N_PORT=$PORT

EXPOSE 8080
```

## 📦 docker-compose.yml

```yaml
services:
  app:
    build:
      context: .
      dockerfile: Dockerfile
    ports:
      - "8080:8080"
    env_file:
      - .env
```

## 🚀 Running the Project

Build and start the container:

```bash
docker-compose up
```

Visit the app at: [http://localhost:8080](http://localhost:8080)

## 🔐 Authentication

Basic authentication is enabled if `N8N_BASIC_AUTH_ACTIVE=true`. Use the credentials from the `.env` file to log in.

## 🧹 Stopping the Service

```bash
docker-compose down
```
