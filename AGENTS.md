# Repository Guidelines

## Project Structure & Module Organization
The FastMCP server lives in `src/server.py`; add tools in place or split into modules under `src/` when complexity grows. Deployment settings sit in `render.yaml`, while runtime dependencies stay in `requirements.txt`. Keep docs and onboarding info in `README.md`.

## Build, Test, and Development Commands
Run `pip install -r requirements.txt` inside your activated Conda env to sync dependencies. Start the server locally with `python src/server.py`; it listens on `0.0.0.0:${PORT:-8000}` and exposes MCP at `/mcp`. Inspect requests end-to-end by running `npx @modelcontextprotocol/inspector` in a second terminal and pointing it at `http://localhost:8000/mcp`.

## Coding Style & Naming Conventions
Target Python 3.13 and follow PEP 8: 4-space indentation, snake_case functions, and descriptive docstrings on MCP tools. Place FastMCP tool registrations near their logic and keep return payloads JSON-serializable. Order imports standard library → third-party → local.

## Testing Guidelines
There is no automated suite yet; validate changes by exercising tool endpoints through the Inspector after launching `python src/server.py`. When adding tests, mirror the server layout under `tests/` and name files `test_<feature>.py` so pytest or the built-in runner can discover them. Include sample payloads that cover both success and failure responses for each MCP tool.

## Commit & Pull Request Guidelines
Follow the existing log format `[scope] concise summary` (e.g., `[server] add balance tool`). Keep commits focused and mention user-visible changes in the body. PRs should explain the problem, outline the solution, note manual test calls (Inspector transcripts help), and link to any relevant issues or deployment follow-ups. Add screenshots or curl transcripts if your change affects the HTTP surface.

## Security & Configuration Tips
Never commit secrets; load `ENVIRONMENT` and other runtime values via your Render dashboard or local `.env`. Confirm the service still binds to `0.0.0.0` for Render after config edits, and document any new environment variables in `README.md`.
