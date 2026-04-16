# Intelligent Traffic System

AI-powered traffic monitoring system using video analytics and real-time congestion prediction.

## Sub-Groups

| Group | Repo | Description |
|-------|------|-------------|
| B1 | [its-detection-edge](https://github.com/Intelligent-Traffic-Ecosystem/its-detection-edge) | Camera capture & edge preprocessing |
| B2 | [its-data-intelligence](https://github.com/Intelligent-Traffic-Ecosystem/its-data-intelligence) | Stream processing & analytics API |
| B3 | [its-dashboard-ui](https://github.com/Intelligent-Traffic-Ecosystem/its-dashboard-ui) | Traffic dashboard & visualization |
| B4 | [its-infrastructure-ops](https://github.com/Intelligent-Traffic-Ecosystem/its-infrastructure-ops) | Platform, security & orchestration |

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

Submodules pin to a specific commit. After pushing new changes to a sub-repo, update the reference here:

```bash
# Pull latest commits for all submodules
git submodule update --remote --merge

# Stage, commit, and push the updated references
git add services/
git commit -m "Update submodules to latest"
git push
```

To update a single submodule (e.g. B2 only):

```bash
cd services/b2-data
git pull origin main
cd ../..
git add services/b2-data
git commit -m "Update B2 submodule to latest"
git push
```

## Environment Variables

See `.env.example` for the full list of configuration options.
