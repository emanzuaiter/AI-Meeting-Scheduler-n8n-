# 🤖 AI Meeting Scheduler — Telegram Voice & Text Assistant (n8n)

An **n8n workflow** that turns Telegram into a smart scheduling assistant. Instead of opening your calendar, writing an email and creating a meeting link by hand, you just send a text or voice message like *"Schedule a meeting with Sara tomorrow at 2 PM"* and an AI agent does everything for you: it checks your calendar, finds the contact's email, creates a Google Calendar event with a **Google Meet link**, and emails the invitation automatically.

## 🎥 Demo

> 📺 **Demo video:** [PASTE YOUR DEMO LINK HERE](https://drive.google.com/file/d/1cEEJDswu60tfZs80zaEsQTSJ8N3OLf6S/view?usp=drive_link))

## ✨ Features

- 🎙️ **Text and voice input:** voice notes are transcribed automatically with OpenAI.
- 🧠 **Natural language understanding:** handles requests like "tomorrow at 2 PM" or "Thursday at 7", and remembers the conversation per chat.
- 📅 **Conflict detection:** checks Google Calendar first and suggests another time if you are busy.
- 👥 **Contact lookup:** finds the participant's email in Google Sheets, and saves new contacts when you provide their email.
- 🎥 **Google Meet links:** every event is created with a Meet link.
- 📧 **Email invitations:** sends a formatted email with the date, time, subject and meeting link via Gmail.
- 🌍 **Multilingual:** replies in the same language you write in (Arabic, English, etc.).
- 🔒 **Access control:** only the authorized Telegram user can trigger the workflow.

## 📦 Requirements

- n8n instance (cloud or self-hosted)
- Telegram bot token ([@BotFather](https://t.me/BotFather))
- OpenAI API key
- Google account (Calendar, Sheets, Gmail) with OAuth2 credentials set up in n8n
- A Google Sheet with two columns: `name` and `email`

## 🚀 Setup

1. In n8n, go to **Workflows → Import from file** and select `email_scadualing_with_voice.json`.
2. Create your credentials (Telegram, OpenAI, Google Calendar, Google Sheets, Gmail) and attach them to the matching nodes.
3. Select your own **Google Sheet** (contacts) and **Calendar** in their nodes.
4. In the `If` node, replace the Telegram chat ID and name with your own so only you can use the bot.
5. Change the timezone in the AI Agent prompt if needed (default: `Asia/Amman`).
6. **Activate** the workflow and send a message to your bot. 🎉

## 💬 Example: How It Works Step by Step

**You send on Telegram (text or voice):**

> "Schedule a meeting with Sara tomorrow at 2 PM about the project update"

**What happens behind the scenes:**

1. **Telegram Trigger** receives the message and checks that it comes from an authorized user.
2. **Voice or text?** If it is a voice note, the audio is downloaded and transcribed to text with OpenAI. If it is text, it goes straight to the agent.
3. **AI Agent** reads the request and extracts the participant (*Sara*), the date (*tomorrow*), the time (*2 PM*) and the subject (*project update*).
4. **Check calendar:** the agent looks at Google Calendar for that time slot.
   - If you are busy, it replies on Telegram and asks you to pick another time. Nothing is created.
   - If the slot is free, it continues.
5. **Find the email:** the agent searches the Google Sheet for "Sara".
   - If found, it uses her email.
   - If not found, it asks you: *"I don't have Sara's email, what is it?"* Once you reply, it saves her to the sheet for next time.
6. **Create the event:** a Google Calendar event is created at the requested time with a **Google Meet link**, and Sara is added as a guest.
7. **Send the invitation:** Gmail sends Sara an email with the subject, date, time and the Meet link.
8. **Confirm:** the agent replies to you on Telegram only after everything succeeded:

> ✅ "Done! Your meeting with Sara is scheduled for tomorrow at 2:00 PM. The invitation with the Meet link was sent to her email."

**Voice example:** send a voice note saying *"Set up a call with Ahmad on Thursday at 7"*. It is transcribed first, then follows exactly the same steps above.
