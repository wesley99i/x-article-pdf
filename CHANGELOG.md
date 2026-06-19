# Changelog

## 2026-06-19 — v1.2.0 — Batch conversion in web app

**Added batch conversion support to `x-article-web` — convert multiple X articles at once.**

**Features:**
- Multi-URL textarea replaces single URL input — paste many X article links (one per line)
- Paste button reads clipboard via browser API (navigator.clipboard.readText) for one-click pasting
- /convert-batch POST endpoint processes all URLs sequentially, saves PDFs to ~/Downloads/x-articles/
- Results page shows clickable download links for successful conversions + error messages for failures
- /download/ GET endpoint serves saved PDFs inline in the browser
- Old /convert single-URL endpoint preserved for backward compatibility

**Files changed:**
- `x-article-web` — new HTML form, JS, endpoints, and CSS for batch workflow (904 lines, +130 lines)
- `CHANGELOG.md` — This entry

## 2026-06-19 — v1.2.1 — UI fixes

**Fixed page loading, mobile UX, and UI structure.**

**Fixes:**
- Switched from single-threaded `TCPServer` to `ThreadingTCPServer` — main page and library now load instantly even while batch conversions are running
- Removed `autofocus` on textarea to fix mobile keyboard fighting
- Bumped textarea font-size to 16px to prevent iOS auto-zoom on focus
- Reduced card padding on screens <500px for better mobile screen use
- Duplicate CSS rules cleaned up

**Features:**
- Mobile-first sticky header with navigation links (Converter, Library) and hamburger menu
- Proper footer with Library link and GitHub link
- /library page — table of all saved PDFs with open/download links
- /download/ endpoint now supports `?dl=1` to force download vs inline view
- Library page shares same header/footer with active nav indicator

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