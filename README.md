# X Article → PDF

Convert X/Twitter articles to dark-themed, styled PDFs for offline reading. All images (cover, avatar, body images) are pre-downloaded and base64-embedded for reliable rendering.

## Features

- **CLI tool** — `x-article-pdf <url>` — one-shot conversion from the terminal
- **Web app** — `x-article-web` — serves a web UI on your LAN for mobile/tablet access
- **Batch conversion** — paste multiple X article links in the web app, convert all at once, download from clickable server links
- **Paste button** — reads clipboard directly via browser API for one-click pasting
- **Dark theme** — matches X's article aesthetic (black background, white text, blue accents)
- **All images embedded** — cover art, author avatar, and body images are pre-downloaded as base64 — no network needed during PDF generation
- **No API auth required** — uses the public fxtwitter API
- **Zero Python dependencies** — uses only stdlib + Chrome headless for PDF conversion

## Quick Start

### Prerequisites

- **Python 3.11+** (stdlib only)
- **Google Chrome or Chromium** (for PDF generation via headless mode)

### Installation

```bash
# Copy the scripts to somewhere in your PATH
cp x-article-pdf x-article-web ~/.local/bin/
chmod +x ~/.local/bin/x-article-pdf ~/.local/bin/x-article-web
```

### CLI Usage

```bash
# Basic — saves to ~/Downloads/<tweet-id>-article.pdf
x-article-pdf https://x.com/user/status/1234567890

# Custom output path
x-article-pdf https://x.com/user/status/1234567890 ~/trains/my-article.pdf

# Help
x-article-pdf --help
```

### Web App Usage

```bash
# Start the server (default port: 8765)
x-article-web

# Custom port
x-article-web --port 9000
```

Then open `http://<your-ip>:8765/` on any device on your network.

**Batch conversion:** Paste multiple X article URLs (one per line) into the textarea, or click the **📋 Paste** button to read directly from your clipboard. Click **Convert All** — each article is fetched, converted to PDF, and saved to `~/Downloads/x-articles/`. Results show clickable download links for successful conversions and error messages for any failures.

## How It Works

```
1. URL → fxtwitter API → article data (blocks, entities, media map)
2. Media images pre-downloaded → base64 data URIs
3. HTML rendered with dark X-style theme
4. Chrome headless → print-to-pdf
5. PDF streamed to browser (web) or saved to disk (CLI)
```

### What's Preserved in the PDF

- Author name, handle, avatar, bio, verified badge
- Cover image
- Article title and publication timestamp
- Body text with bold, italic, blockquotes, code blocks
- Ordered/unordered lists
- Embedded images (via MEDIA entities in X articles)
- Section headers (H2)
- Engagement metrics (views, likes, reposts, bookmarks)
- Dark background / light text theme

## Project Structure

| File | Purpose |
|------|---------|
| `x-article-pdf` | CLI tool — converts one URL to PDF |
| `x-article-web` | Web app — serves a LAN-accessible form for on-demand conversion |
| `README.md` | This file |
| `CHANGELOG.md` | Version history |

## Data Flow

```
User submits URL
       ↓
extract_tweet_id() — parses X/Twitter URL
       ↓
fetch_article() — calls fxtwitter API, builds media_id→URL map
       ↓
dl_image() — downloads all images, encodes as base64 data URIs
       ↓
render_html() — builds dark-themed HTML with embedded images
       ↓
generate_pdf() — Chrome headless → print-to-pdf
       ↓
PDF returned to user (download or save to disk)
```

## Technology

- **Python stdlib** — http.server, urllib, base64, re, json, subprocess, tempfile
- **fxtwitter API** — public, no auth needed, returns structured article data
- **Google Chrome** — headless mode with `--print-to-pdf` for pixel-perfect PDF rendering
- **Chrome headless flags**: `--headless --disable-gpu --no-margins --disable-software-rasterizer --print-to-pdf-no-header`

## License

MIT