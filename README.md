# clearpass

Crawl a website — or a published Google Slides deck — and save what you find as PNG, JPEG, PPTX, DOCX, PDF, or interactive MHTML archives. Includes a TUI (Terminal UI) for ease of use.

## Install

```bash
npm install -g clearpass
```

Requires Node 18+. A headless Chromium build installs automatically on first setup.

## Usage

**Interactive TUI Shell** (recommended for first-time use):

```bash
clearpass
```
Once inside the TUI, use the following commands:
- `/snap <url>` or just `<url>`: Capture a single URL as screenshots.
- `/scrape <url>`: Extract website text as Markdown (great for PDF/DOCX).
- `/slides <url>`: Capture a Google Slides presentation.
- `/bulk`: Enter bulk-URL mode (paste multiple URLs, hit enter twice).
- `/format <fmt>`: Set default output format (`png`, `jpeg`, `pptx`, `docx`, `pdf`, `mhtml`).
- `/max <number>`: Set max pages/slides (default 300).
- `/out <dir>`: Set output folder.
- `?` or `/help`: Show all commands.
- `q` or `/quit`: Exit.

**Direct CLI mode:**

```bash
clearpass -u https://example.com -o ./shots -f mhtml -m 25
```

**Text Scraping to PDF:**

```bash
clearpass -u https://example.com --scrape -f pdf
```

**Uninstall:**

```bash
clearpass uninstall
```

**Full command list:**

```bash
clearpass --help
```

## How it decides a page is "ready"

Instead of waiting on network events, clearpass hashes the visible frame every ~200ms and waits until the picture stops changing before it screenshots or scrapes. On Slides specifically, it also reads the on-screen page counter, so a slide with a multi-step build animation gets captured only once it's fully revealed, not mid-build.

### Smart Security & Captcha Detection
It can smartly detect when a site has blocked you with Cloudflare, Turnstile, or typical reCAPTCHA/hCaptcha prompts, and will gracefully abort the capture with a clear error message instead of hanging indefinitely.

## Formats

- `png` / `jpeg`: Individual screenshots.
- `pptx` / `docx`: A single compiled document; screenshots/extracted text are embedded.
- `pdf`: A standard PDF file containing the screenshots or scraped markdown text.
- `mhtml`: A raw web archive format. **Use this if you want links and interactive content to remain clickable and functional when saved locally.**

## License

MIT