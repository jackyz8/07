# FFGlory — patched deployment bundle

## Railway deployment
1. Upload/push the contents of this folder to a private GitHub repository.
2. Create a Railway project from that repository.
3. Admin login works without `.env`: edit `admin_config.json` in the project root and change `username` and `password` before deployment. Keep this file private. On Railway, you can instead set `ADMIN_USERNAME` and `ADMIN_PASSWORD` in Variables; those override the file.
4. Build command: `pip install -r requirements.txt` (Railway normally detects Python requirements automatically).
5. Start command: `python app.py`.
6. Open the generated Railway domain and check `/health` for `status: ok`.

The included account/token JSON files are intentionally empty templates because the original archive contained authentication/session material. Add your own valid data privately at runtime. Do not upload secrets to GitHub.

## Important
- `CguFF_pb2.py`, `DRIFT/step1_clan.png`, `DRIFT/step2_clan.png`, and `DRIFT/favicon.ico` were not present in the source archive. Missing optional assets are listed in `MISSING_FILES.txt`; no fake protobuf modules were generated.
- `/api/guildinfo` now accepts an authenticated session or `X-Guild-API-Key` matching `GUILD_API_KEY`.
- `/api/clanjoin` is admin-only.
- `/health` reports service status and uptime.
- Initial admin is created from `admin_config.json` (server-side, not exposed in HTML), unless Railway variables `ADMIN_USERNAME` and `ADMIN_PASSWORD` override it. The old `.env` file has been removed from this bundle.
- Static HTML deployment on Vercel alone will not run this Python backend; use a Python-capable host such as Railway for the full app.

## Local run
`pip install -r requirements.txt` then `python app.py`.
