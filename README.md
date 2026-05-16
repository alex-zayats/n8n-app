# N8N Car Listings Scraper (OTOMOTO)

Automated n8n workflow that scrapes used car listings from [otomoto.pl](https://www.otomoto.pl) and sends Telegram notifications about new listings.

## What it does

1. **Cron trigger** — runs every 2 hours
2. **Fetch listings** — scrapes otomoto.pl for used, undamaged cars in Warsaw (price: 5 000–35 000 PLN), sorted by newest first
3. **Parse** — extracts structured data (title, brand, price, fuel type, mileage) from JSON-LD embedded in the page HTML
4. **Upsert** — stores new listings in an n8n DataTable (`car_listings`), deduplicating by content hash
5. **Diff** — compares freshly scraped listings against the existing table to find new ones
6. **Notify** — sends a Telegram message: either the count of new listings or a "no updates" confirmation

## Repository structure

```
workflows/
└── Car Listings Scraper.json   # n8n workflow definition

containers/
├── docker-compose.yml          # n8n service (port 5678)
├── Dockerfile                  # n8n image
├── .env                        # environment variables
├── car_listings_template.csv   # DataTable schema reference
└── README.md                   # Docker setup guide
```

## Quick start

```bash
cd containers
docker-compose up -d
```

Open http://localhost:5678, create an account, and import `workflows/Car Listings Scraper.json`.

Configure the **Telegram** credential in n8n before activating the workflow.
