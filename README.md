# 🤖 AI Meeting Scheduler — Telegram Voice & Text Assistant (n8n)

An **n8n workflow** that turns Telegram into a smart scheduling assistant. Send a text or voice message like *"Schedule a meeting with Sara tomorrow at 2 PM"* and the AI agent checks your calendar, finds the contact's email, creates a Google Calendar event with a **Google Meet link**, and emails the invitation automatically.

## 🎥 Demo

> 📺 **Demo video:** [PASTE YOUR DEMO LINK HERE](#)

## ✨ Features

- 🎙️ Text and **voice** input (voice is transcribed with OpenAI)
- 🧠 Understands natural language dates and times, with chat memory
- 📅 Checks Google Calendar for conflicts before scheduling
- 👥 Looks up emails in Google Sheets and saves new contacts
- 🎥 Creates Google Meet links and sends email invitations via Gmail
- 🌍 Replies in the same language you write in

## 📦 Requirements

- n8n instance (cloud or self-hosted)
- Telegram bot token ([@BotFather](https://t.me/BotFather))
- OpenAI API key
- Google account (Calendar, Sheets, Gmail) with OAuth2 credentials in n8n
- A Google Sheet with two columns: `name` and `email`

## 🚀 Setup

1. In n8n, go to **Workflows → Import from file** and select `email_scadualing_with_voice.json`.
2. Add your credentials (Telegram, OpenAI, Google Calendar, Google Sheets, Gmail) to the matching nodes.
3. Select your own Google Sheet and Calendar in their nodes.
4. In the `If` node, replace the Telegram chat ID and name with your own.
5. Activate the workflow and message your bot. 🎉

## 💬 Example

| You say | Result |
|---|---|
| "Schedule a meeting with Sara tomorrow at 2 PM" | Event + Meet link created, invitation emailed to Sara |
| 🎙️ *(voice)* "Set up a call with Ahmad on Thursday at 7" | Voice transcribed, then same flow |
