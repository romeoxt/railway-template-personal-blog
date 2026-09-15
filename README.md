# Deploy and Host Personal Blog with Railway

A minimal markdown blog — publish posts via API, serve a clean public site from PostgreSQL.

## About Personal Blog

Personal Blog is a FastAPI application for developers who want a real blog URL without WordPress or a static-site build pipeline. Write posts in Markdown, publish with a curl command, and readers get a fast homepage and `/post/slug` pages.

## About Hosting Personal Blog

Self-hosting your blog keeps content and data in your Railway project. PostgreSQL stores posts, the API handles publishing, and Railway manages builds, health checks, and public HTTPS — deploy once and write from anywhere.

## Environment Variables

| Variable | Description | Secret | Example/Notes |
| --- | --- | --- | --- |
| `DATABASE_URL` | PostgreSQL connection string | Yes | `${{Postgres.DATABASE_URL}}` |
| `BLOG_TITLE` | Site title on the homepage | No | `My Blog` |
| `BLOG_TAGLINE` | Subtitle under the title | No | `Notes from building in public` |
| `ADMIN_API_KEY` | Key for `POST /admin/posts` | Yes | `${{secret(32)}}` — send as `X-API-Key` |

## Deploy and Host

1. Deploy this repo from GitHub on Railway.
2. Add **PostgreSQL** and attach a **volume**.
3. Set the environment variables above on the app service.
4. Enable **public HTTP** and deploy.
5. Confirm `/health` returns OK.
6. Publish your first post:

```bash
curl -X POST https://YOUR-RAILWAY-URL/admin/posts \
  -H "Content-Type: application/json" \
  -H "X-API-Key: YOUR_ADMIN_API_KEY" \
  -d "{\"title\":\"Hello world\",\"body_markdown\":\"# Hello\\n\\nFirst post.\"}"
```

7. Visit your Railway URL to see the post live.

## Common Use Cases

- Developer blogs and build-in-public logs
- MVP marketing sites that need a `/blog` with real posts
- Personal writing separate from Notion or Medium
- API-first publishing from scripts, CI, or note-taking tools

## Dependencies for Personal Blog Hosting

The Railway template includes:

- **Personal Blog API** — this GitHub repo (FastAPI + Uvicorn)
- **PostgreSQL** — Railway PostgreSQL plugin with persistent volume

## Deployment Dependencies

- [FastAPI documentation](https://fastapi.tiangolo.com/)
- [Railway PostgreSQL docs](https://docs.railway.com/databases/postgresql)

## Why Deploy Personal Blog on Railway?

GitHub deploy, private Postgres networking, health checks, and a public URL in one project — no separate static host or CMS install.

## Template Content

| Service | Source |
| --- | --- |
| Personal Blog | GitHub repo (this template) |
| Postgres | Railway PostgreSQL plugin |

## Run locally

```bash
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
copy .env.example .env
uvicorn app.main:app --reload --port 8000
```

## Marketing site

See `website/index.html` for the template landing page.

## Author

romeoxt — herbylegall9@gmail.com

## License

MIT
