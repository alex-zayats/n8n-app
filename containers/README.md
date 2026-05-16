# N8N + SQLite Docker Setup

## Structure

```
configs/
├── docker-compose.yml    # Main orchestration
├── Dockerfile.n8n        # Custom N8N image
├── .env                  # Environment variables
└── README.md             # This file
```

## Services

### 1. N8N Server
- **Port**: 5678
- **Database**: SQLite (file-based)
- **Volume**: `n8n_data` for persistence
- **URL**: http://localhost:5678

## Getting Started

### 1. Start Services
```bash
cd configs
docker-compose up -d
```

### 2. Access N8N
- Open http://localhost:5678
- Create initial account
- Import workflow from `../workflows/car-listings-scraper.json`

## Environment Variables

Edit `.env` to change:
- `N8N_HOST` - n8n hostname
- `N8N_PORT` - n8n port
- `TIMEZONE` - Timezone for scheduling

## Volumes

- `n8n_data` - N8N configuration and internal database
- `sqlite_data` - SQLite database files

## Useful Commands

```bash
# View logs
docker-compose logs -f n8n
docker-compose logs -f sqlite

# Rebuild images
docker-compose up -d --build

# Stop services
docker-compose down

# Stop and remove volumes
docker-compose down -v

## Next Steps

1. Create workflow in N8N that:
   - Uses Cron trigger
   - Fetches listings
   - Parses data


## Notes

- N8N will auto-initialize with SQLite on first run
- Database files are persisted in Docker volumes
