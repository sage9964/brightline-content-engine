# Brightline Content Engine
### AI-Powered Content Repurposing Pipeline

# Part of an AI Automation Portfolio — [see all projects](https://sage9964.github.io)

---

## What it does

Brightline Consulting publishes weekly thought leadership articles. Manually rewriting each article for LinkedIn, Twitter/X, and email was taking 30–45 minutes nobody had.

This pipeline takes one article submission and automatically produces:
- A **LinkedIn post** — 150-200 words, strong hook, hashtags, engagement question
- A **Twitter/X thread** — 5-7 tweets, numbered, under 280 characters each
- An **email newsletter** — AI-written subject line, key takeaways, auto-sent via Gmail

Total time from submission to outputs: under a minute.

---

## Live demo

[Try the Brightline Content Engine →](https://tally.so/r/44R7r5)

---

## Architecture

```
Tally Form → n8n Webhook → Claude Sonnet (Anthropic) → Code Node (JS)
                                                              ↓
                                          Gmail (auto-send) + Google Docs × 2
```

**Stack:**
- **Tally** — form intake (professional, hosted, free tier, native webhook support)
- **n8n** — workflow engine
- **Claude Sonnet 4.6** — content generation via structured XML prompt
- **Gmail API** — auto-sends email newsletter
- **Google Docs API** — saves LinkedIn and Twitter drafts to a shared Drive folder

---

## Key design decisions

**One AI call, three outputs** — Claude returns all three content pieces in a single call using XML tags (`<linkedin_post>`, `<twitter_thread>`, `<email_newsletter>`). A JavaScript Code node parses the tags into separate fields. Three separate AI calls would add latency and cost with no benefit.

**Basic LLM Chain, not AI Agent** — no tools needed. AI Agent is for when the model needs to take actions. For pure generation tasks, Basic LLM Chain is the simpler, correct pattern.

**Tally over n8n Form Trigger** — Tally produces a professional client-facing form. n8n's built-in form trigger exposes a raw n8n URL, which is unpolished for real client delivery.

**Google Docs over Sheets for drafts** — formatted posts read better in a Doc. The consultant can edit directly before copying to the platform.

---

## Related projects

- [CoreFlash Systems — AI Lead Qualification & Booking Agent](https://sage9964.github.io/coreflash-chatbot)
