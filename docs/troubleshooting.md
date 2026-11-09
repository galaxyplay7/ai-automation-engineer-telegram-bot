# Troubleshooting

| Symptom | Likely cause | Fix |
|---|---|---|
| Bot does not respond at all | Workflow not active, or n8n not reachable over HTTPS | Activate the workflow; check your n8n URL is public and uses HTTPS |
| Bot stopped responding after you set up another workflow | The same bot token is used by another active Telegram Trigger, which took over the webhook | Use one bot per workflow; deactivate the other one, then deactivate and re-activate this workflow |
| `Bad Request: can't parse entities` | A message with special characters was sent in Markdown mode | Keep *Send Telegram Reply* on HTML parse mode with the escaping expression from the template |
| Tool error: `Workflow is not active and cannot be executed` | The document tools call a workflow that is not active | Activate this workflow (the tools call the workflow itself) |
| Tool error mentioning the workflow ID | Your n8n version does not accept `{{ $workflow.id }}` in the tool | Open each document tool and choose this workflow from the **Workflow** list |
| Google `403` / `insufficient permissions` | Google Drive API not enabled, or credential connected before enabling it | Enable Google Drive API in Google Cloud, then reconnect the credential |
| Google `401` / `invalid_grant` | OAuth token expired (common for apps in *Testing* mode, about every 7 days) | Reconnect the Google Drive credential, or publish the OAuth app |
| File arrives but the bot says it failed | The agent ran out of iterations or the model misread the tool result | Check the execution; try again, or lower temperature |
| Document looks unstyled | Content did not use the markup (for example tables without leading `\|`) | Ask again, or reinforce the markup rules in the system prompt |
| Replies are slow sometimes | Retry On Fail waiting, or the fallback model taking over | Expected under rate limits; reduce *Max Tries* if needed |
| `429 Too Many Requests` in executions | Free-tier rate limit | Fallback handles it; for heavy use, switch to a paid tier |

## Reading executions

Open **Executions** in n8n and click a failed run:

- A red **Groq Chat Model** node with a green **Gemini Fallback Model** means the fallback worked as designed.
- A red **Send Telegram Reply** means a Telegram API problem. Read the error description.
- For document issues, check the **Document Request** sub-execution (each tool call creates its own execution).
