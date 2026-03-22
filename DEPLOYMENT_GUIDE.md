# 🎉 Emily & Cédric Wedding Bot — Deployment Guide

## What you have
- `app.py` — the bot server (pre-loaded with all wedding details)
- `requirements.txt` — Python dependencies
- `Procfile` — tells Render how to start the server

---

## Step 1: Get your Anthropic API key (5 min)
1. Go to https://console.anthropic.com
2. Sign up for a free account
3. Go to "API Keys" → click "Create Key"
4. Copy and save your key (starts with `sk-ant-...`)

---

## Step 2: Set up Twilio WhatsApp Sandbox (5 min)
1. Go to https://twilio.com and sign up for free
2. In the console, go to: Messaging → Try it out → Send a WhatsApp message
3. You'll see a sandbox number (e.g. +1-415-523-8886) and a join code
4. Share with guests: "Send 'join <your-code>' to +1-415-523-8886 on WhatsApp to chat with our wedding assistant"
5. Keep this page open — you'll need the webhook URL field later

---

## Step 3: Deploy to Render (10 min)
1. Go to https://render.com and sign up for free
2. Click "New +" → "Web Service"
3. Choose "Deploy from existing code" → upload the three files
   OR connect a GitHub repo containing the three files
4. Settings:
   - Name: emily-cedric-wedding-bot
   - Environment: Python 3
   - Build Command: pip install -r requirements.txt
   - Start Command: gunicorn app:app
5. Under "Environment Variables", add:
   - Key: ANTHROPIC_API_KEY
   - Value: (paste your key from Step 1)
6. Click "Create Web Service"
7. Wait ~2 minutes. You'll get a URL like: https://emily-cedric-wedding-bot.onrender.com

---

## Step 4: Connect Twilio to your bot (2 min)
1. Go back to Twilio WhatsApp Sandbox settings
2. In the "When a message comes in" field, paste:
   https://emily-cedric-wedding-bot.onrender.com/webhook
3. Make sure it says "HTTP POST"
4. Click Save

---

## Step 5: Test it!
Send a WhatsApp message to your Twilio number and ask:
- "What is the dress code for Saturday?"
- "How do I get to the château from Barcelona?"
- "What time does the ceremony start?"

---

## Sharing with guests
Add to your invitations:
> "Have questions about the weekend? WhatsApp our wedding assistant!
> Send 'join <your-code>' to +1-415-523-8886"

---

## Cost estimate
- Render: FREE
- Twilio sandbox: FREE
- Anthropic API: ~$0.002 per conversation = ~$2–5 for 100 guests total

## Need help?
Contact the person who set this up for you! 😊
