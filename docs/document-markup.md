# Document Markup Reference

The agent writes document content in a lightweight, Markdown-like markup. The **Build Styled HTML** node converts it into a styled document.

## Syntax

| Markup | Renders as | Typical use |
|---|---|---|
| `# Title` | Large uppercase title in accent color, starts the header block | Document title, or a person's name on a CV |
| `> text` (right after `#`) | Bold muted subtitle | Role / tagline |
| `@ text` (right after `#`) | Small muted info line | Contact line: `City \| email \| LinkedIn` |
| `## Section` | Uppercase section heading + divider line | Summary, Experience, Skills |
| `### Item` | Bold item heading | Sub-topic |
| `### Item \|\| Note` | Bold item left, italic note right-aligned | `### Senior Engineer \|\| 2015 - Present` |
| `> text` (elsewhere) | Bold accent-colored line | Company name under a job title |
| `@ text` (elsewhere) | Small muted line | Location, remarks |
| `- item` | Bullet list | Responsibilities, features |
| `1. item` | Numbered list | Steps, projects |
| `1. item` then `- sub` | Numbered item with nested bullets (numbering continues) | Project + details |
| `\| A \| B \|` + `\|---\|---\|` | Table with tinted header row | Comparisons, skill matrix |
| `**text**` | Bold | Emphasis |
| `_text_` | Italic | Notes, references |
| blank line | New paragraph | |
| `---` | Ends current block (no visible line) | Spacing |

If the content does not start with `#`, the tool's `title` is used as the document title.

## Example: CV

```text
# Jane Doe
> Senior Mechanical Engineer & AI Automation Engineer
@ Jakarta, Indonesia | jane@example.com | linkedin.com/in/janedoe | github.com/janedoe

## Professional Summary
Mechanical engineer with **15+ years** in EPC projects, now building workflow automations and AI agents with n8n.

## Experience
### Senior Mechanical Engineer || Jan 2015 - Present
> Example Energy Co.
- Led a team of 10 engineers on a 450 MW gas power plant project
- Automated document review with n8n, cutting review time by 28%

## Projects
1. Change Order Approval Automation (n8n)
- Google Forms → Google Sheets → ERP via API, with Slack approvals
- Approval cycle reduced from 5 days to 1 day
2. Telegram AI Assistant with Word/PDF output
- Groq primary model with Gemini fallback

## Skills
**Automation:** n8n, Make, REST APIs, webhooks
**AI:** prompt engineering, tool calling, RAG

| Language | Level |
|---|---|
| Indonesian | Native |
| English | Professional |

_References available on request._
```

## Default theme

| Element | Style |
|---|---|
| Font | Times New Roman 11 pt (title 20 pt, section 12 pt) |
| Accent color | Dark blue `#1F3864` |
| Body text | Slate `#334155` |
| Muted text | `#64748b` |
| Table header | `#D9E2F3` background, accent text |

Change these in the **Theme** block at the top of the **Build Styled HTML** Code node.
