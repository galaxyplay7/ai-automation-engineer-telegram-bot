# Changelog

## [1.0.0] - 2026-11-09

### Added
- Telegram AI assistant specialized in automation (n8n, Make, Zapier, APIs, AI agents) with strict accuracy rules.
- Groq `openai/gpt-oss-120b` as the primary model with **Retry On Fail** (2 tries, 3 s wait).
- Google Gemini as an automatic **fallback model** via the AI Agent's *Enable Fallback Model*.
- Window memory (10 messages per chat).
- **Word (.docx) and PDF generation** tools: lightweight markup → styled HTML → Google Doc (Drive conversion) → DOCX/PDF export → Telegram, with automatic cleanup.
- Document theme: Times New Roman 11 pt, dark-blue accent, section dividers, right-aligned dates, nested numbered lists, styled tables.
- Long-reply splitting and Telegram-safe HTML escaping.
- In-canvas tutorial sticky notes.

### Fixed during development
- Divider lines leaking into the next bullet or paragraph in Google Docs (spacer paragraph after `<hr>`).
- Numbered lists restarting at 1 when bullets sat between items (nested lists).
- Telegram `can't parse entities` errors caused by underscores in file names and URLs (HTML parse mode + escaping).
