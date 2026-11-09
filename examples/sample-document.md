# Sample Document Input

This is the kind of `content` the agent passes to `create_word_document` / `create_pdf_document`. You can paste it into the **Document Request** node's test input to try the pipeline without the agent.

**Test input (pinned data for *Document Request*):**

```json
{
  "title": "n8n Production Checklist",
  "chat_id": "YOUR_TELEGRAM_CHAT_ID",
  "format": "pdf",
  "content": "# n8n Production Checklist\n> Before you activate a workflow\n@ Version 1.0 | Internal guide\n\n## Reliability\n1. Error handling\n- Add an error workflow that alerts you\n- Use Retry On Fail on flaky API nodes\n2. Rate limits\n- Add a fallback model to AI agents\n\n## Security\n- Store secrets in credentials, never in Code nodes\n- Restrict webhooks with authentication\n\n## Summary\n| Area | Status |\n|---|---|\n| Error workflow | Done |\n| Fallback model | Done |\n\n_Review this list every quarter._"
}
```

**Rendered result:**

- Title "N8N PRODUCTION CHECKLIST" with subtitle and info line, then a divider
- Section "RELIABILITY" with numbered items 1 and 2, each with nested bullets
- Section "SECURITY" with a bullet list
- Section "SUMMARY" with a two-column table and a tinted header row
- An italic closing note

Replace `YOUR_TELEGRAM_CHAT_ID` with your own chat ID (send a message to your bot and look at `message.chat.id` in the Telegram Trigger output).
