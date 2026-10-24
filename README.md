# my-robo-new

A minimal [Botpress](https://botpress.io) v1 chatbot: the standard "Hello World" starter with the Botpress web chat module. It greets users and says goodbye, and is a starting point for a larger bot.

> This uses the **original Botpress v1 platform** (`botpress` 1.x, `botpress-web` 1.x), which is no longer maintained and is not compatible with Botpress v11 and later.

## What it does

- Replies to a greeting (`hello`, `hi`, `hey`, `test`, `GET_STARTED`...) with the `#welcome` message block.
- Replies to `bye`, `goodbye`, `quit`, `exit`, `stop`, `done` or `leave` with the `#goodbye` block.
- Exposes `GET /api/botpress-analytics/ping`, which answers `pong`, as a simple health check.

Messages are defined in [`content.yml`](content.yml) (UMM blocks with typing indicators and random variants), and the matching rules are in [`index.js`](index.js).

## Run it

Requires Node.js 8 or newer.

```bash
npm install
npm start          # runs `botpress start`
```

Open `http://localhost:3000` (or the port in `PORT` / `BOTPRESS_PORT`) for the Botpress admin UI and the web chat.

## Configuration

Settings are in [`botfile.js`](botfile.js) and can be overridden with environment variables.

| Variable | Default | Meaning |
|---|---|---|
| `PORT` or `BOTPRESS_PORT` | `3000` | HTTP port for the API and UI |
| `BOTPRESS_DATA_DIR` | `./data` | Where Botpress stores its runtime data |
| `BOTPRESS_CONFIG_DIR` | `./modules_config` | Module configuration files |
| `DATABASE` | SQLite (`data/db.sqlite`) | Set to `postgres` to use PostgreSQL |
| `DATABASE_URL`, `PG_HOST`, `PG_PORT`, `PG_USER`, `PG_PASSWORD`, `PG_DB`, `PG_SSL` | none | PostgreSQL connection settings, used when `DATABASE=postgres` |
| `BOTPRESS_PASSWORD` | none | Password for the admin UI, if you enable authentication |
| `BOTPRESS_LICENSE_KEY`, `BOTPRESS_CUSTOMER_ID` | none | Only for Botpress Pro/Enterprise features |

## Project structure

```
index.js            Bot logic (hear rules and replies)
content.yml         Message blocks (#welcome, #goodbye)
botfile.js          Botpress settings
theme.scss          Web chat styling
data/               Runtime data (database, secret key, logs); git-ignored, created on first run
modules_config/     Per-module config (created on first run)
```

## Notes

- `data/` holds the SQLite database and a generated `secret.key`. They are not tracked in git; do not commit them.
- Next steps from the Botpress starter: add a connector module (Messenger, Slack...), then add your own `bp.hear` rules and message blocks.
- The `LICENSE` file is the Botpress end-user license that shipped with the starter template, and `package.json` carries the same license string.
