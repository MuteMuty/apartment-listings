# Apartment listings

**Scrapes about 500 apartments for sale from sreality.cz into PostgreSQL and shows them in a React app with no ads.** One command starts all three parts.

<img src="https://github.com/MuteMuty/luxonis/assets/69723817/c8fa9e53-5244-4291-b89c-407af58f00b7" alt="Light theme: a listing titled 'For sale apartment 3+1 60 m²' in Nový Jičín for 2,159,000 CZK, with a photo carousel, thumbnails below it and page numbers at the top" width="900"/>
<img src="https://github.com/MuteMuty/luxonis/assets/69723817/d0e07b7d-d9a7-4e7a-8e24-0f29bd4e696a" alt="The same listing in the dark theme" width="900"/>

## Why it exists

A take-home task for a hiring process, built in Jul 2023.

## How it works

| Part | Folder | What it does |
|---|---|---|
| Scraper | `backend/scrape.ts` | Opens 25 result pages of sreality.cz in headless Chrome with Puppeteer and saves each listing's title, location, price and image URLs to a `scraped_data` table. The table is recreated on every start. |
| API | `backend/serve.ts` | Express server on port 4000. `GET /` returns one page of listings using `LIMIT` and `OFFSET`. |
| Web app | `frontend/` | React and TypeScript. One listing per row with a photo carousel and thumbnails, page controls, and a light and dark theme. |
| Database | `docker-compose.yaml` | PostgreSQL 15 in its own container, with a named volume. |

The scraper drives a real browser instead of parsing raw HTML, so it reads the page as a visitor sees it. The cost is a heavier Docker image and a slower first start.

## Run it

Needs Docker with Compose.

```sh
docker-compose up
```

Then open http://localhost:8080. The API is on http://localhost:4000. Listings appear once the scraper has finished.

## Tech

TypeScript, React, Express, node-postgres, Puppeteer, PostgreSQL 15, Docker Compose.

## Status

Finished in Jul 2023 and not maintained. sreality.cz has changed since then, so the scraper may no longer find listings. Made by [Erik Pahor](https://github.com/MuteMuty).
