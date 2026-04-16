# Intelligent Traffic System

AI-powered traffic monitoring system using video analytics and real-time congestion prediction.

## Sub-Groups

| Group | Repo | Description |
|-------|------|-------------|
| B1 | [its-detection-edge](https://github.com/Intelligent-Traffic-Ecosystem/its-detection-edge) | Camera capture & edge preprocessing |
| B2 | [its-data-intelligence](https://github.com/Intelligent-Traffic-Ecosystem/its-data-intelligence) | Stream processing & analytics API |
| B3 | [its-dashboard-ui](https://github.com/Intelligent-Traffic-Ecosystem/its-dashboard-ui) | Traffic dashboard & visualization |
| B4 | [its-infrastructure-ops](https://github.com/Intelligent-Traffic-Ecosystem/its-infrastructure-ops) | Platform, security & orchestration |

## Architecture

```
┌──────────┐    ┌──────────┐    ┌─────────────┐    ┌────────────┐    ┌──────────┐
│ Cameras  │───▶│ B1 Edge  │───▶│   Kafka     │───▶│ B2 Stream  │───▶│ Postgres │
│          │    │ (detect) │    │             │    │ Processor  │    │          │
└──────────┘    └──────────┘    └─────────────┘    └────────────┘    └────┬─────┘
                                                                         │
                ┌──────────┐    ┌─────────────┐    ┌────────────┐        │
                │ B3 Dash  │◀───│ B2 API      │◀───│ REST + WS  │◀───────┘
                │ (Next.js)│    │ (FastAPI)   │    │            │
                └──────────┘    └─────────────┘    └────────────┘
                                       │
                ┌──────────┐           │
                │ B4 Infra │◀──────────┘ (Prometheus /metrics, /health)
                │ (Kong,   │
                │  K8s)    │
                └──────────┘
```

## Getting Started

### Clone with submodules

```bash
git clone --recurse-submodules https://github.com/Intelligent-Traffic-Ecosystem/its-main.git
cd its-main
```

If you already cloned without submodules:
```bash
git submodule update --init --recursive
```

### Run the full system

```bash
# Copy and configure environment variables
cp .env.example .env

# Start all services
docker compose up -d

# Check status
docker compose ps
```

### Update submodules to latest

```bash
git submodule update --remote --merge
```

## Environment Variables

See `.env.example` for the full list of configuration options.
