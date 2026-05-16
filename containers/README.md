# N8N + SQLite Docker Setup

## Structure

```
containers/
├── docker-compose.yml          # Main orchestration
├── Dockerfile                  # Custom n8n image with sqlite3
├── .env                        # Environment variables
├── car_listings_template.csv   # DataTable schema reference
└── README.md                   # This file
```

## Services

### n8n
- **Port**: 5678
- **URL**: http://localhost:5678

## Getting Started

### 1. Start services
```bash
cd containers
docker-compose up -d
```

### 2. Access n8n
- Open http://localhost:5678
- Create initial account
- Import workflow from `../workflows/Car Listings Scraper.json`
- Configure the **Telegram** credential

## Environment Variables

Edit `.env` to change:
- `N8N_HOST` — n8n hostname
- `N8N_PORT` — n8n port
- `TIMEZONE` — timezone for scheduling

## Volumes

- `n8n_data` — n8n configuration and database

## Useful Commands

```bash
# View logs
docker-compose logs -f n8n

# Rebuild image
docker-compose up -d --build

# Stop services
docker-compose down

# Stop and remove volumes
docker-compose down -v
```

## Notes

- Database files are persisted in the `n8n_data` Docker volume
