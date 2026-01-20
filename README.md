# Expoproj - API & Application

A full-stack application with Node.js/TypeScript backend API, MySQL database, Redis caching, and Solr search integration.

## Project Overview

This project provides a complete backend infrastructure with:
- **API Server**: Node.js + TypeScript (runs on `localhost:9090`)
- **Database**: MySQL 8.0 (port `3307`)
- **Caching**: Redis (port `6379`)
- **Search Engine**: Solr 9.8.1 (port `8983`)
- **Job Queue**: Bull Board (port `9999`)
- **LLM Integration**: Ollama API support (port `11434`)

## Prerequisites

- Docker & Docker Compose
- Node.js 18+ with pnpm package manager
- Linux/macOS environment

## Quick Start

### 1. Clone Repository

```bash
git clone <repository-url>
cd expoproj
```

### 2. Start Docker Services

```bash
docker compose up -d
```

This starts:
- MySQL database
- Redis cache
- Solr search engine

### 3. Install Dependencies

```bash
cd api
pnpm install
```

### 4. Run the API Server

```bash
pnpm dev
```

The API will start on `http://localhost:9090`

## Service Endpoints

| Service | URL | Port |
|---------|-----|------|
| API Server | http://localhost:9090 | 9090 |
| Bull Board (Jobs) | http://localhost:9999 | 9999 |
| Solr Admin | http://localhost:8983/solr | 8983 |
| Redis | localhost | 6379 |
| MySQL | localhost | 3307 |
| Ollama API | http://localhost:11434 | 11434 |

## Configuration

Database and Redis credentials are defined in `docker-compose.yml`. Update them in the docker-compose configuration file as needed before deployment.

Database details:
- **Database Name**: `aviary-db`
- **Default User**: Set in docker-compose.yml

## Stopping Services

```bash
docker compose down
```

To remove data volumes:
```bash
docker compose down -v
```

## Project Structure

```
expoproj/
├── api/                    # Node.js API application
│   ├── src/
│   │   ├── main.ts         # Application entry point
│   │   ├── service/        # Business logic
│   │   └── mysql/          # Database scripts
│   └── package.json
├── data/                   # Volumes for persistent data
│   └── volumes/
│       ├── mysql-data/
│       ├── redis-data/
│       └── solr-data/
└── docker-compose.yml      # Service configuration
```

## Troubleshooting

**Port 3307 already in use:**
```bash
sudo fuser -k 3307/tcp
docker compose down -v
docker compose up -d
```

**MySQL connection failed:**
- Ensure MySQL container is running: `docker logs expoproj-mysql-1`
- Check `api/config/default.yml` uses correct port and credentials
- Verify environment variables in `docker-compose.yml`

**API won't start:**
```bash
cd api
pnpm install
pnpm dev
```

## Environment Setup

Create `.env` file in `api/` directory for local development:
```env
NODE_ENV=development
DB_HOST=localhost
DB_PORT=3307
REDIS_URL=redis://localhost:6379
```

Update credentials in `docker-compose.yml` and corresponding config files before deployment.
