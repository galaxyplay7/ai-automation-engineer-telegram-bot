# Setup Guide

This guide takes you from an empty n8n instance to a working bot in about 10–15 minutes.

## Requirements

- An **n8n** instance (self-hosted or n8n Cloud) recent enough for the AI Agent node to offer **Enable Fallback Model**. The template uses AI Agent node v3.1. If your instance is older, update n8n first.
- The instance must be reachable over **HTTPS from the internet**, because Telegram delivers messages by webhook.
- Accounts: Telegram, Groq, Google AI Studio (Gemini), and a Google Cloud project.

## Step 1: Import the workflow

1. In n8n open **Workflows → Add workflow → … → Import from File**.
2. Select `workflow/ai-automation-engineer-bot.json`.
3. Save. Red warning icons on some nodes just mean credentials are not attached yet.

## Step 2: Telegram bot

1. In Telegram, open [@BotFather](https://t.me/BotFather) and send `/newbot`.
2. Choose a display name and a username ending in `bot`.
3. Copy the **HTTP API token**.
4. In n8n create a **Telegram API** credential with that token.
5. Select it in all four Telegram nodes:
   - Telegram Trigger
   - Send Typing Action
   - Send Telegram Reply
   - Send File to Telegram

> A bot token can only have **one webhook**. If the same bot is used by another active workflow or another n8n instance, the last one activated "steals" the messages. Use one bot per workflow.

## Step 3: Groq (primary model)

1. Sign in at [console.groq.com](https://console.groq.com) and create an API key.
2. In n8n create a **Groq** credential and select it in **Groq Chat Model**.
3. The default model is `openai/gpt-oss-120b`. You can switch to any chat model your Groq account offers.

## Step 4: Google Gemini (fallback model)

1. Create an API key at [aistudio.google.com](https://aistudio.google.com).
2. In n8n create a **Google Gemini (PaLM) API** credential and select it in **Gemini Fallback Model**.
3. The default model is `models/gemini-3.5-flash-lite`. Model names change over time, so pick whatever is current in the node's model list.

## Step 5: Google Drive (Word & PDF generation)

1. In [Google Cloud Console](https://console.cloud.google.com) create or select a project.
2. Enable the **Google Drive API** (*APIs & Services → Library*).
3. Configure the **OAuth consent screen**. While in testing mode, add your own Google account as a test user.
4. Create an **OAuth client ID** (type: *Web application*) and add the redirect URL that n8n shows in the credential dialog.
5. In n8n create a **Google Drive OAuth2 API** credential with the client ID and secret, then click **Sign in with Google**.
6. Select it in:
   - Create Google Doc
   - Download as DOCX or PDF
   - Delete Temporary Google Doc

> If you enabled an API *after* connecting the credential and get permission errors, reconnect the credential so it picks up the new access.

## Step 6: Activate and test

1. Click **Active** (or **Publish** on newer n8n versions).
2. Message your bot:
   - `Hi, what can you help me with?` should return a normal chat reply.
   - `Create a short Word document about n8n error handling` should return a `.docx` file.
   - `Make that a PDF` should return a `.pdf` file.

## Optional: self-referencing tools

The two document tools (**create_word_document** and **create_pdf_document**) call this same workflow through `{{ $workflow.id }}`, so they keep working after import without editing IDs. If your n8n version does not accept an expression there, open each tool node and choose this workflow from the **Workflow** list instead.

## Optional: customization

| What | Where |
|---|---|
| Persona, rules and reply style | AI Automation Engineer Agent → *System Message* |
| Memory length | Simple Memory → *Context Window Length* |
| Document fonts and colors | Build Styled HTML → *Theme* block at the top of the code |
| Retry behavior | Groq Chat Model → *Settings* → Retry On Fail / Max Tries / Wait Between Tries |
| Fallback model | Replace or reconfigure **Gemini Fallback Model** |
