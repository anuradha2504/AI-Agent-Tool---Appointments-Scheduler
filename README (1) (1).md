# Telegram Appointment Scheduler
🏥 # **Doctor Automated Appointment Scheduling AI**
**Intelligent Telegram Bot 🚀 | Real-time Sync with Google Calendar + Google Sheets**

This project is an Agentic AI–powered appointment scheduling system designed for healthcare professionals. Patients can **book, reschedule, or cancel appointments easily via Telegram,** while the system ensures real-time synchronization with **Google Calendar and Google Sheets.**

> **Live Bot:** ` t.me/Anu_Doctor_bot. 
> **Demo:** Demo video (placeholder)

---

## ✨ Features

| Action                     | Google Calendar                     | Google Sheets                             |
| -------------------------- | ----------------------------------- | ----------------------------------------- |
| **New Appointment**        | Creates a new event                 | Appends a new row                         |
| **Reschedule Appointment** | Creates new event + deletes old one | Old row → *Rescheduled*, new row appended |
| **Cancel Appointment**     | Deletes event                       | Row marked *Cancelled*                    |

| Feature                    | Description                                       |
| -------------------------- | ------------------------------------------------- |
| 🧠 AI Appointment Agent    | Handles natural-language scheduling conversations |
| 🔁 Real-time Sync          | Updates Google Calendar + Sheets instantly        |
| 📲 Telegram Integration    | Patients chat directly from their phones          |
| ✔ Availability Validation  | Always checks office timings & booked slots       |
| ⏱ Auto Slot Management     | 1 hr consultation + 15 min break logic applied    |
| 🔄 Modify / Cancel Support | Frees slots & updates records                     |
| 📑 Patient Data Logging    | Saves name, phone & appointment details in Sheets |
| 🤝 Guided Conversation     | Confirms before booking anything                  |
---

## 🧱 System Architecture
<img width="1024" height="1024" alt="image" src="https://github.com/user-attachments/assets/915a2064-ea25-4c9e-a044-494545432aba" />

**Components & Purpose**

| Component                              | Purpose                                     |
| -------------------------------------- | ------------------------------------------- |
| **Telegram Bot → @akvaidya_bot**       | Patient-facing conversation                 |
| **n8n Workflow (AI Agent)**            | Coordinates scheduling logic and tool calls |
| **Google Calendar**                    | Stores booked appointments and availability |
| **Google Sheets**                      | Permanent appointment ledger                |
| **OpenAI GPT Model**                   | Understands user messages and context       |

![Architecture Diagram](./images/architecture.png)

---

## 🕒 Clinic Operating Rules

| Days              | Hours             |
| ----------------- | ----------------- |
| **Monday–Friday** | 9:00 AM – 8:00 PM |
| **Saturday**      | 9:00 AM – 1:00 PM |
| **Sunday**        | Closed            |

**Appointment Duration:** 60 minutes
**Break Time:** 15 minutes

---

📅 Scheduling Logic

✔ Doctor Schedule:

Mon–Fri: 9:00 AM → 8:00 PM
Sat: 9:00 AM → 1:00 PM

Sun: Closed ❌
✔ Consultation Duration → 1 Hour
✔ Break Between Appointments → 15 min
✔ Time Slot Validation Every Request
✔ No booking without final user confirmation

⛔ Prevents double booking by validating existing events in Calendar.

## 💾 Required Google Sheet Format

Your Google Sheet must contain the following **exact column headers**:

```
Patient_Name | Date_and_Time | Phone_Number | Appointment_Status 
```

**Sheet Tab Name:** `Sheet1`

---

## 🔧 Setup Guide

### 1) Create Telegram Bot

1. Open Telegram → Search **BotFather**
2. Run `/newbot`
3. Copy the **Bot Token**
4. Paste it into the **Telegram Trigger** & **Send Message** nodes in n8n

### 2) Connect Google Calendar

* Ensure your Google API credentials in n8n include **Calendar read/write access**

### 3) Configure Google Sheets

1. Create the sheet with required headers
2. Copy the **Sheet ID** from the URL
3. Insert the Sheet ID into all Google Sheets nodes in n8n

### 4) Add OpenAI API Key

* Add your OpenAI API Key to the **OpenAI Chat Model** credentials in n8n

### 5) Import Workflow

* Go to **n8n → Workflows → Import** and select the JSON file located at `/workflow/appointment-workflow.json`

---

## 🔁 Workflow Logic

### ✅ New Booking

* Create event in Google Calendar
* Append appointment data to Google Sheet

### 🔄 Reschedule

* Create **new event** in Calendar
* Delete **old event** from Calendar
* Mark old sheet row as **Rescheduled**
* Append new row for the rescheduled appointment

### ❌ Cancel

* Delete event from Calendar
* Mark corresponding sheet row as **Cancelled**

---

## 🧪 Testing

| Action         | Expected Outcome                                                       |
| -------------- | ---------------------------------------------------------------------- |
| **Book**       | Event appears in Calendar + new row added                              |
| **Reschedule** | Old event deleted + row marked Rescheduled + new event + new row added |
| **Cancel**     | Event removed + row marked Cancelled                                   |

---

## 📄 License

This project is licensed under the **MIT License**.

---

## 🤝 Contributions

Contributions, PRs, and issues are **welcome**!
