# Changelog

## 2026-06-16 — Initial release

### v1.0.0 — CLI tool + Web app

**Initial release of X Article → PDF converter.**

**Features:**
- CLI tool (`x-article-pdf`) for one-shot conversion from the terminal
- Web app (`x-article-web`) with LAN-accessible form for mobile/tablet use
- Dark-themed PDF matching X's article aesthetic
- All images embedded as base64: cover art, author avatar, body images via `article.media_entities`
- No API auth required — uses public fxtwitter API
- Zero Python dependencies — stdlib only + Chrome headless for PDF output
- Persistent disk saves on web app (`~/Downloads/x-articles/`)
- Error handling for invalid URLs, missing articles, network failures, and timeouts

**Files:**
- `x-article-pdf` — CLI tool (398 lines)
- `x-article-web` — Web app (626 lines)
- `README.md` — Project documentation
- `CHANGELOG.md` — This file