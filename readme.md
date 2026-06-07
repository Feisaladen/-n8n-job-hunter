# 🤖 AI Job Hunter — n8n Workflow

> **Version:** v1.0 (Work in Progress — actively being updated)

An automated job hunting workflow built with n8n that searches the web for job opportunities, evaluates them using AI, and sends tailored cover letter applications — all on autopilot.

---

## 📌 What It Does

Every morning at 7AM, this workflow:

1. **Searches the web** for job openings using the Tavily API
2. **Loops through each result** and uses an AI model (via OpenRouter) to detect if there is an actual opening
3. **Scores the match** between the job and your profile (0–100)
4. **Writes a tailored cover letter** for each relevant opportunity
5. **Sends the application email** automatically via Gmail
6. **Logs the job** to a Google Sheet for tracking
7. **Sends a Telegram alert** notifying you of the application

---

## 🧱 Workflow Structure

```
Schedule Trigger (7AM daily)
    └── HTTP Request (Tavily job search)
        └── Loop Over Items
            └── Basic LLM Chain (does this page have a job opening?)
                └── Code (parse AI response)
                    └── IF has_opening == true
                        └── Basic LLM Chain (score match + write cover letter)
                            └── Code (parse AI response)
                                └── Send Email (Gmail)
                                    └── Log to Google Sheets
                                        └── Telegram Alert
```

---

## 🛠️ Tech Stack

| Tool | Purpose |
|---|---|
| [n8n](https://n8n.io) | Workflow automation engine |
| [Tavily API](https://tavily.com) | AI-powered web search for job listings |
| [OpenRouter](https://openrouter.ai) | LLM gateway for AI reasoning |
| Gmail (OAuth2) | Sending application emails |
| Google Sheets | Logging and tracking applications |
| Telegram Bot | Real-time alerts |

---

## ⚙️ Setup

### 1. Import the workflow
Import `job-hunter.json` into your n8n instance via **Workflows → Import from file**.

### 2. Set up credentials in n8n
Go to **Settings → Credentials** and add:

- `Tavily API` — get your key at [tavily.com](https://tavily.com)
- `OpenRouter API` — get your key at [openrouter.ai](https://openrouter.ai)
- `Gmail OAuth2` — connect your Gmail account
- `Google Sheets OAuth2` — connect your Google account
- `Telegram API` — create a bot via [@BotFather](https://t.me/BotFather)

### 3. Update placeholders in the workflow
Search for and replace all placeholders with your own details:

| Placeholder | Replace with |
|---|---|
| `YOUR_TAVILY_API_KEY` | Your Tavily API key |
| `YOUR_EMAIL` | Your email address |
| `YOUR_PHONE` | Your phone number |
| `YOUR_NAME` | Your full name |
| `YOUR_CV_LINK` | Link to your CV |
| `YOUR_GOOGLE_SHEET_ID` | Your Google Sheet ID |
| `YOUR_TELEGRAM_CHAT_ID` | Your Telegram chat ID |
| `YOUR_*_CREDENTIAL_ID` | Credential IDs from n8n |
| Profile in LLM prompt | Your skills, experience, projects |

### 4. Activate the workflow
Toggle the workflow to **Active** — it will run automatically every day at 7AM.

---

## 📁 Project Structure

```
AI-JOB-WORKFLOW/
├── job-hunter.json     # Main n8n workflow file
└── README.md           # This file
```

---

## 🚧 Roadmap (Upcoming in v2)

- [ ] Add deduplication to avoid applying to the same job twice
- [ ] Support multiple job search queries
- [ ] Add a scoring threshold (only apply if match score > 70)
- [ ] Store cover letters in Google Docs per application
- [ ] Add WhatsApp notification support
- [ ] Build a simple dashboard to track application stats

---

## ⚠️ Important Notes

- **Never commit real API keys or credentials** — use n8n's built-in credential manager and keep placeholders in the JSON
- This workflow is in **v1** and actively being improved
- Test with the workflow set to **inactive** first before going live
- Make sure your LLM prompt accurately reflects your actual skills and experience

---

*Built with n8n — automating the job hunt so you can focus on the work.*