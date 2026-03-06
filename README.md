# n8n Automation Workflows

A collection of production-ready n8n workflows built during my AI Bootcamp. These workflows cover real business use cases including AI-powered CV screening, appointment booking automation, and server uptime management.

---

## Workflows

### 1. HR AI Agent — CV Screening

**File:** `HR_AI_Agent_CV-Screening.json`

An end-to-end recruitment automation pipeline that monitors a Gmail inbox for incoming job applications, uses GPT-4o-mini to classify and score candidates, and logs results to a Google Sheet for easy review.

**What it does:**
- Monitors a Gmail inbox every minute for new emails
- Uses an AI text classifier to identify genuine job applications vs unrelated emails
- Extracts the attached CV (PDF) and saves it to a Google Drive folder
- Runs the CV through an AI Agent powered by GPT-4o-mini, which scores the candidate from 0 to 10 based on the job description
- Outputs a structured report including candidate details, years of experience, technical skills, fit score breakdown, and reasoning
- Appends all results automatically to a Google Sheet for HR review

**Tools used:** n8n, OpenAI GPT-4o-mini, Gmail, Google Drive, Google Sheets, LangChain Text Classifier, Structured Output Parser

**Use case:** Any business that receives CV applications by email and wants to automate the initial screening process.

---

### 2. Booking Automation

**File:** `Booking_Automation.json`

A full-cycle appointment booking system that syncs with Google Calendar, handles form submissions, sends WhatsApp confirmations via Twilio, and automatically sends reminders and follow-ups.

**What it does:**

*Calendar Sync (runs every 30 minutes):*
- Checks Google Calendar for existing bookings
- Generates available time slots for the next 14 days based on business hours (Mon–Sat, 9am–5pm, Africa/Johannesburg timezone)
- Writes available slots to a Google Sheet for use in booking forms

*Booking Handler (triggered on form submission):*
- Reads new bookings from a Google Form response sheet
- Parses and validates booking data including name, phone number, service type, and selected time slot
- Generates a unique booking ID and logs the booking to a CRM spreadsheet
- Sends a WhatsApp confirmation message via Twilio with confirm, cancel, and reschedule options

*WhatsApp Webhook Listener:*
- Listens for customer replies via webhook
- Routes confirmed bookings to create a Google Calendar event and update the CRM
- Handles cancellations and reschedule requests with appropriate responses

*Reminder Scheduler (runs every hour):*
- Scans confirmed bookings and sends a 24-hour reminder and a 2-hour reminder before each appointment
- Sends a follow-up message after the appointment requesting a review and offering a discount on the next booking
- Tracks which reminders have been sent to avoid duplicates

**Tools used:** n8n, Google Calendar, Google Sheets, Google Forms, Twilio (WhatsApp), Webhooks, Luxon (datetime handling)

**Use case:** Any service-based business (salons, clinics, tutors, consultants) that takes appointments and wants to automate booking confirmations and reminders.

---

### 3. Keep Alive Ping

**File:** `Keep_Alive_Ping.json`

A lightweight utility workflow that pings an n8n instance health endpoint on a schedule to prevent the server from going to sleep on free-tier hosting platforms like Render.

**What it does:**
- Triggers on a set interval (every few minutes)
- Sends an HTTP GET request to the `/healthz` endpoint of an n8n instance
- Keeps the server awake and responsive without any manual intervention

**Tools used:** n8n, HTTP Request node, Schedule Trigger

**Use case:** Anyone running n8n on a free-tier cloud host like Render where instances spin down after inactivity.

---

## Setup Instructions

Each workflow JSON can be imported directly into any n8n instance:

1. Open your n8n instance
2. Click **New Workflow**
3. Click the **...** menu and select **Import from file**
4. Upload the JSON file
5. Update all placeholder values (marked as `REPLACE_WITH_...`) with your own credentials and IDs
6. Connect your credentials for Gmail, Google Drive, Google Sheets, OpenAI, and Twilio as needed
7. Activate the workflow

---

## Requirements

- n8n (self-hosted or cloud)
- OpenAI API key (for HR AI Agent)
- Google account with access to Gmail, Drive, Sheets, and Calendar
- Twilio account with a WhatsApp-enabled number (for Booking Automation)

---

## About

These workflows were built as personal projects to explore real-world automation and AI integration. They are designed to be reusable templates that anyone can adapt for their own business needs.

Built by [Sibabalwe Desemela](https://www.linkedin.com/in/sibabalwe-desemela-554789253/) | [GitHub](https://github.com/SibzDesign)
