# AnkiForge — APKG → MCQ Intelligence

Convert your Anki flashcard decks into AI-powered multiple choice quizzes — directly in the browser. No server, no uploads, 100% private.

## ✨ Features

- **Upload any .apkg** — Works with all Anki decks including images, audio, cloze deletion, and complex HTML templates
- **Images rendered inline** — Photos, diagrams, and media display exactly as they appear in Anki
- **AI MCQ Generation** — Claude AI creates 4-option questions with distractors and explanations
- **Interactive Quiz Mode** — Practice with instant feedback and score tracking
- **Export anywhere** — Download as JSON, CSV, Markdown, or Anki-importable TSV
- **100% browser-based** — All parsing happens locally via JSZip + sql.js (WASM)

## 🚀 Deploy to Vercel (Recommended)

### Option 1: GitHub + Vercel (easiest)

1. Push this folder to a GitHub repository
2. Go to [vercel.com](https://vercel.com) → New Project
3. Import your GitHub repo
4. Click **Deploy** — done!

### Option 2: Vercel CLI

```bash
npm i -g vercel
cd ankiforge
vercel --prod
```

### Option 3: Any static host
This is a single HTML file. Host it on:
- **Netlify**: Drag the folder to [app.netlify.com/drop](https://app.netlify.com/drop)
- **GitHub Pages**: Push to `gh-pages` branch
- **Cloudflare Pages**: Connect GitHub repo

## 🔑 Claude API Key

You need an Anthropic API key for MCQ generation:
1. Get one at [console.anthropic.com](https://console.anthropic.com)
2. In the app, click **⚡ MCQ Panel** and enter your key
3. The key is stored only in `sessionStorage` (never sent anywhere except the Anthropic API)

## 🧠 How It Works

```
.apkg file
    ↓ JSZip
collection.anki2 (SQLite) + media/
    ↓ sql.js (WASM)
notes + cards + templates + deck structure
    ↓ Template renderer
Rendered card HTML with inline images
    ↓ Claude API (claude-sonnet-4)
4-option MCQ with explanation + difficulty rating
    ↓
Quiz mode / Export
```

## 📁 Project Structure

```
ankiforge/
├── index.html     # Entire app (single file, no build step)
├── vercel.json    # Vercel deployment config
└── README.md      # This file
```

## 🔧 Technical Notes

- **APKG format**: Anki packages are ZIP files containing `collection.anki2` (SQLite) and numbered media files with a JSON mapping
- **Field separator**: Anki uses `\x1f` (ASCII 31) to separate fields
- **Template system**: Supports `{{FieldName}}`, `{{FrontSide}}`, cloze deletions, type-in fields
- **Media**: All images/audio are extracted to blob URLs for secure local rendering
- **No CORS issues**: Uses `anthropic-dangerous-direct-browser-access` header for direct API calls

## 📄 License

MIT — free to use, modify, and deploy.
