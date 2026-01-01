# AI-Lead-Generator-Qualifier-n8n-Workflow-
## 📋 Overview

This n8n workflow serves as an autonomous **AI Sales Agent**. It monitors a Gmail inbox for new inquiries, uses **Google Gemini** to extract structured data (Lead Name, Budget, Intent), scores the lead based on quality, and instantly notifies the team via Slack if the lead is "Hot" or "Warm."

## ✨ Features

* **Real-time Monitoring:** Polls Gmail every minute for unread messages in the Inbox.
* **AI-Powered Extraction:** Uses **Google Gemini** to ignore "fluff" and extract key data points:
    * 👤 **Lead Name**
    * 🏢 **Company**
    * 💰 **Budget** (identifies currency and amounts)
    * 🎯 **Intent** (what solution they need)
* **Intelligent Scoring:** Automatically categorizes leads as:
    * 🔥 **Hot:** Budget or deadline mentioned.
    * 🌤️ **Warm:** Solution requested but no numbers.
    * 🗑️ **Junk:** Spam or sales pitches.
* **Smart Filtering:** Automatically filters out "Junk" leads to reduce noise.
* **Instant Alerts:** Sends a formatted Slack notification to the team.

## 🛠️ The Workflow Logic

1.  **Gmail Trigger:** Watches for emails with labels `INBOX` and `UNREAD`.
2.  **AI Agent (Gemini):** Processes the email body text using a custom prompt: *"You are an elite Data Extraction Specialist..."*
3.  **Code Node:** Cleans the JSON output from the AI to ensure valid data structure.
4.  **If / Else Filter:**
    * **Pass:** If Lead Score is "Hot" OR "Warm".
    * **Stop:** If Lead Score is "Junk".
5.  **Slack Notification:** Posts details to the designated channel.

## 🚀 Setup Guide

### Prerequisites
* An active [n8n](https://n8n.io/) instance (Cloud or Self-hosted).
* **Google Cloud Console** project with Gemini API enabled.
* **Gmail** account credentials (OAuth2).
* **Slack** workspace and App Webhook.

### Installation
1.  Clone this repository or download the `Lead-Generator.json` file.
2.  Open your n8n dashboard.
3.  Click **Import Workflow** (top right) and select the JSON file.
4.  Configure the Credentials:
    * `Gmail account 2`: Connect your Gmail OAuth2.
    * `Google Gemini(PaLM) Api`: Add your Gemini API Key.
    * `Slack OAuth2`: Connect your Slack account.
5.  Activate the workflow!

## 📄 Output Example

**Incoming Email:**
> "Hi, I'm John from TechCorp. We need a chatbot. We have $5k set aside for this."

**Slack Alert:**
> 🚨 **NEW LEAD DETECTED** 🚨
>
> 👤 **Name:** John Doe
> 🏢 **Company:** TechCorp
> 💰 **Budget:** $5k
> ⭐ **Score:** Hot
> 🎯 **Intent:** Chatbot

## 👨‍💻 Author

**Kimani BotLab**
* *Website:* [Link to your site]
* *Twitter/X:* [Link]
* *LinkedIn:* [Link]

---
*Note: This workflow relies on the specific JSON prompt structure defined in the `AI Agent` node.*
