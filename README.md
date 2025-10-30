# 🧠 Cortx — Voice-Powered AI Personal Assistant  
### Built with n8n · Google Gemini · ElevenLabs  

Cortx is an advanced **multi-agent AI personal assistant** that listens, understands, and acts on your **voice commands**.  
It uses **n8n** for workflow orchestration, **Google Gemini** for reasoning and content generation, and **ElevenLabs** for natural voice interaction.  

This assistant can manage your **emails**, **calendar**, **contacts**, and even **create research-backed content** — entirely through voice.  

---

## 🚀 Key Features

- 🎙️ **Voice-First Interaction** — Talk to your assistant directly using ElevenLabs speech processing.  
- 📧 **Email Management** — Send, draft, and search emails through Gmail.  
- 📅 **Calendar Automation** — Create, update, and delete Google Calendar events.  
- 👥 **Contact Management** — Add, retrieve, or update contacts from Airtable.  
- ✍️ **AI Content Generation** — Research and write formatted HTML blogs using Gemini and Tavily.  
- 🔗 **Agentic Architecture** — Parent and Child agents collaborate to perform multi-step reasoning.  
- 🌐 **Web-Connected Intelligence** — Tavily provides live web data for factually enriched results.  

---

## 🧠 Architecture Overview  

Cortx follows a **multi-agent system** composed of one **Parent Agent** and several **Child Agents**, each responsible for a specific task domain.

### 🎛️ Parent Agent (Central Brain)
**Workflow:** `Ultimate Personal Assistant.json`  

Responsible for understanding user intent, routing tasks, and executing multi-step logic.  
The Parent Agent uses **Gemini** for reasoning and **Tavily AI** for web search integration.  

**Example Flow:**
> “Look up a contact’s email and send them a meeting invite.”  
1. Calls the **Contact Agent** to retrieve the email.  
2. Passes the result to the **Email Agent** to send the invite.  

---

## 🤖 Child Agents (Specialized Sub-Workflows)

### 1. 📧 Email Agent  
**Workflow:** `Email Agent.json`  
- Handles sending, replying, and drafting emails.  
- Uses **Gmail OAuth2** for authentication.  
- Triggered by parent workflow when the intent involves email operations.  

---

### 2. 📅 Calendar Agent  
**Workflow:** `Calendar Agent.json`  
- Creates, updates, and deletes **Google Calendar** events.  
- Manages scheduling tasks automatically from natural language commands.  

---

### 3. 👥 Contact Agent  
**Workflow:** `Contact Agent.json`  
- Retrieves, adds, or updates contacts stored in **Airtable**.  
- Airtable base functions as a unified personal contact database.  

---

### 4. ✍️ Content Creator Agent  
**Workflow:** `Content Creator Agent.json`  
- Performs topic research using **Tavily AI**.  
- Uses **Gemini** to generate a formatted HTML blog post with citations.  
- Ideal for automated, data-backed content creation.  

---

## 🗣️ ElevenLabs Integration (Voice Interface)

Cortx leverages **ElevenLabs** for high-quality **speech-to-text (STT)** and **text-to-speech (TTS)** capabilities.  

### 🔹 How It Works  
1. ElevenLabs captures and transcribes your voice input into text.  
2. The text payload is sent to n8n’s **Parent Agent Webhook**.  
3. Cortx executes the required actions.  
4. Optionally, ElevenLabs TTS can deliver a natural spoken response.  

This enables a fully **hands-free, conversational AI experience**.  

---

## 🧩 Technology Stack

| Tool | Purpose |
|------|----------|
| **n8n** | Workflow orchestration engine |
| **Google Gemini** | LLM for reasoning and generation |
| **ElevenLabs** | Speech-to-text and text-to-speech engine |
| **Gmail API** | Email management |
| **Google Calendar API** | Event scheduling and management |
| **Airtable API** | Contact database |
| **Tavily AI** | Web search and factual knowledge retrieval |

---

## ⚙️ Setup & Installation

### 1. Import Workflows  
Import all five `.json` workflows into your n8n instance:  

- `Ultimate Personal Assistant.json`  
- `Email Agent.json`  
- `Calendar Agent.json`  
- `Contact Agent.json`  
- `Content Creator Agent.json`  

---

### 2. Activate the Parent Workflow  
- Enable the **Ultimate Personal Assistant** workflow.  
- Copy the **Production Webhook URL** from the Webhook node.  

---

### 3. Configure ElevenLabs Webhook  
- In your ElevenLabs account, set up a webhook that sends transcribed text to the n8n webhook.  
- The payload format should look like:  
  ```json
  {
    "query": "your transcribed text"
  }
