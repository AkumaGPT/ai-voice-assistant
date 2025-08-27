# 🗓️ AI Voice Assistant (n8n Workflow)

This repository contains two **n8n workflows** that together create an **AI-powered scheduling assistant**.  
The assistant can **check availability** and **schedule meetings** in Google Calendar through natural language requests.

---

## Features

- **Check Availability**
  - Parses requested date & time from a webhook request.
  - Checks your Google Calendar for conflicts.
  - If unavailable, suggests up to **3 closest slots** or the **next available day**.

- **Schedule Meetings**
  - Books meetings directly into Google Calendar.
  - Defaults to **30-minute duration**.
  - Confirms the booking with a natural, user-friendly message.

- **Conversational AI**
  - Uses **OpenAI GPT (gpt-4.1-mini)** via LangChain.
  - Ensures responses sound natural (not robotic).

---

## 📂 Workflows

### 1. `GetAvailability.json`
- **Purpose:** Check if a requested time slot is free.
- **Flow:**
  1. Webhook receives request (date/time).
  2. Gets current date & time.
  3. Fetches Google Calendar events.
  4. AI Agent evaluates availability & suggests alternatives.
  5. Responds to the webhook with a natural answer.

### 2. `ScheduleMeeting.json`
- **Purpose:** Schedule a confirmed meeting.
- **Flow:**
  1. Webhook receives booking request.
  2. Extracts requested date & time.
  3. Creates a **30-minute meeting** in Google Calendar.
  4. AI Agent confirms success with meeting details.
  5. Responds to the webhook with a confirmation message.

---

## ⚙️ Setup Instructions

1. **Import Workflows**
   - In your n8n instance, go to **Workflows → Import from File**.
   - Upload:
     - `GetAvailability.json`
     - `ScheduleMeeting.json`

2. **Configure Credentials**
   - **Google Calendar:** Connect your Google account.
   - **OpenAI API:** Add your API key (used under `Udo API` credentials).

3. **Activate Webhooks**
   - Each workflow starts with a webhook trigger.
   - Example endpoints:
     - `/webhook/94e2842e-9019-45e6-8060-e934f94323b4` → Availability
     - `/webhook/7d5f616b-4b2a-4efe-94ce-fea5231a13df` → Scheduling
   - Use these endpoints in your chatbot, frontend, or voice assistant.

4. **Test**
   - Send a POST request with `date` and `time`.
   - Verify the AI response (availability or confirmation).

---

## 📌 Example Interaction

**User:**  
“Book me a meeting on August 27th at 2pm.”

**Assistant Responses:**
- ✅ If free → “The requested time of 2:00pm on August 27th, 2025, is available. Would you like me to schedule it?”
- ⏳ If busy → “That time isn’t available. The closest options are 3:00pm, 4:00pm, or 10:00am the next day.”
- 📅 After booking → “The meeting has been successfully scheduled for August 27th, 2025, from 2:00pm to 2:30pm.”

---

## 🔧 Tech Stack
- [n8n](https://n8n.io/) – Workflow automation
- [LangChain](https://www.langchain.com/) – AI orchestration
- [OpenAI GPT](https://platform.openai.com/) – Conversational intelligence
- [Google Calendar API](https://developers.google.com/calendar) – Event scheduling

---

## 📜 License
MIT License – free to use and modify.
