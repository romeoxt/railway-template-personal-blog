# Railway Template Composer Setup

## Marketplace listing

- **Title:** Deploy and Host Personal Blog with Railway
- **Short description:** Minimal markdown blog — publish posts via API, serve a clean public site from PostgreSQL.
- **Category:** Starters
- **Overview:** paste `README.md`

## Services

| Service | Source | Volume | Public HTTP |
| --- | --- | --- | --- |
| Personal Blog | GitHub repo (this folder) | — | Yes |
| Postgres | Railway PostgreSQL plugin | `/var/lib/postgresql/data` | No |

## Variables — Personal Blog

| Variable | Value | Secret | Description |
| --- | --- | --- | --- |
| `DATABASE_URL` | `${{Postgres.DATABASE_URL}}` | Yes | Postgres connection |
| `BLOG_TITLE` | `My Blog` | No | Homepage title |
| `BLOG_TAGLINE` | `Notes from building in public` | No | Homepage subtitle |
| `ADMIN_API_KEY` | `${{secret(32)}}` | Yes | `X-API-Key` for `/admin/posts` |

## Settings — Personal Blog

- Healthcheck: `/health`
- Attach volume to PostgreSQL
