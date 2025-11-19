# Daily-News-Summarization-Agent-for-Discord
This agent delivers a curated, AI-summarized news digest to a Discord channel every morning at 10 AM. It automates the whole process—fetching top headlines from trusted sources, summarizing with AI, and sending the result straight to your community

💡 Why This Agent?
Traditional news delivery (RSS feeds, scraping) often faces authorization issues and breaks due to changing source rules.
AI-powered workflows solve these problems by leveraging public news APIs and advanced language models for readable, useful news digests.

🏗️ Architecture & How It Works
n8n Workflow Orchestration: All logic flows are built in n8n.

NewsAPI as Source: Uses NewsAPI for reliable and global daily headlines.

AI Summarization: Headlines are summarized via OpenAI GPT-4 (can use other LLMs).

Discord Delivery: A Discord channel receives the digest message via webhook.

Trigger: Daily at 09:59 AM using n8n's Schedule Trigger node.

Workflow Steps:

Schedule Trigger: Fires every day at 10 AM.

Fetch Headlines: HTTP Request to NewsAPI with the required API key.

AI Summarize Headlines: Passes all headlines to the LLM agent with a concise morning-digest prompt.

Send to Discord: Posts summary to a Discord channel using HTTP (webhook).

🧠 Design Decisions & Rationale
Public API over RSS Feeds: RSS feeds often require special authentication or break without notice. NewsAPI offers a stable, well-documented alternative.

AI Summarization for User Value: Raw headlines feel fragmented; summarization provides context and engagement.

Discord for Delivery: Discord is widely used by communities and teams—webhook integration is easy and reliable.

No Database Needed: Simplicity—no historical backend unless business needs evolve.

⚡ Problems Faced & Solutions
1. RSS Authorization/401 Errors

Many RSS sources are restricted or poorly maintained.

Solved: Switched to NewsAPI, which only requires an API key and offers public endpoints.

2. Data Mapping Errors

Initial attempts to use .flatMap failed because the data structure did not match.

Solved: Carefully mapped the headlines using .map, robustly checked that the array existed.

3. AI Prompt and Output Wrangling

Getting readable summaries out of the LLM took prompt tuning and checking output structure.

Solved: Used tested template and checked output key (text or similar).

4. Discord Integration

Ensured the right content format and referenced the AI summary output key properly.

🎉 What We Achieved
Fully automated news agent: No manual feed checks, no broken sources.

Friendly morning news delivered to Discord daily.

High reliability, modular design. Easily extendable for new channels or data sources.

Fast response: Workflow runs in seconds and is simple to maintain.

📦 How To Use
Get your NewsAPI API Key: Sign up here.

Set up your Discord channel: Create a webhook and paste its URL into n8n.

Configure n8n workflow:

Paste your NewsAPI key and Discord webhook in the workflow nodes.

Use the provided prompt and mapping to pass headlines to OpenAI (or your chosen LLM).

Test And Go Live: Run the workflow once manually and check your Discord channel.

🤖 Future Improvements
Add historical news storage (Google Sheets, Notion, Airtable).

Enable more flexible source selection (support for Categories, Regions).

Push to other platforms (WhatsApp, Slack).
