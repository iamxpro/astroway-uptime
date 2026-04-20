# astroway-uptime

External uptime monitoring for astroway.info via GitHub Actions.
Runs every 5 minutes, pings 5 critical endpoints, alerts Telegram on 5xx/timeout.

## How it works

`.github/workflows/uptime.yml` runs on `cron: '*/5 * * * *'`:

1. Matrix of 5 URLs (main, cart, EN, app, API).
2. `curl` each with 25s timeout.
3. Non-2xx/3xx or connection failure → sends Telegram alert.

Free for public repos. Uses ~300 CI minutes/month (well under limit).

## Secrets required

- `TG_BOT` — Telegram bot API token
- `TG_CHAT` — group chat ID (e.g. `-5285216242`)

## Add or edit monitors

Edit the `matrix.target` list in the workflow. Push → next cron tick picks it up.

## Why not UptimeRobot/BetterStack/StatusCake

All removed free-tier Telegram/webhook integration by 2025. GitHub Actions is the last zero-cost path.
