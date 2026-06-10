# AI Email Order Tracker

An intelligent email automation system that monitors Gmail for order-related emails, extracts structured order data using Google Gemini AI, logs everything to Google Sheets, and automatically creates or updates Trello cards based on order status — in English and French.

---

## How It Works

```
Gmail receives order email (English or French)
        ↓
AI Agent extracts structured order data
        ↓
Order logged to Google Sheets database
        ↓
Google Sheets Trigger fires
        ↓
Check if Trello card exists
   ↙              ↘
New order       Existing order
Create card     Update card
   ↓                ↓
Log Trello Card ID back to Sheets
```

---

## Screenshot

![Workflow](screenshot.png)

---

## Features

- **Multilingual** — processes emails in English and French
- **AI data extraction** — extracts Order ID, Client, Supplier, Status, Dates, Language
- **Smart Trello routing** — New → To Do, In Production → Doing, Shipped/Delivered → Done
- **Duplicate handling** — updates existing Trello cards instead of creating duplicates
- **Full audit trail** — all orders tracked in Google Sheets with Trello Card IDs
- **Custom JavaScript logic** — status-based list routing

---

## Tech Stack

| Tool | Purpose |
|------|---------|
| n8n | Workflow orchestration |
| Google Gemini | AI email data extraction |
| Gmail API | Email monitoring trigger |
| Google Sheets | Order database |
| Trello API | Project board management |
| JavaScript | Conditional routing logic |

---

## Order Status → Trello Board Mapping

| Email Status | Trello List |
|-------------|-------------|
| New | To Do |
| In Production | Doing |
| Shipped / Delivered | Done |
| Delayed / Other | To Do (default) |

---

## Extracted Fields

```json
{
  "Order_ID": "string",
  "Client_Name": "string",
  "Supplier_Name": "string",
  "Status": "New | In Production | Shipped | Delivered | Delayed | Follow-up Needed",
  "Order_Date": "YYYY-MM-DD",
  "Delivery_Date": "YYYY-MM-DD",
  "Last_Update": "YYYY-MM-DD",
  "Source_Email": "string",
  "Language": "English | French",
  "Notes": "string"
}
```

---

## Setup

1. Import `Email_Order_Tracker_CLEAN.json` into your n8n instance
2. Connect credentials:
   - Gmail OAuth2
   - Google Sheets OAuth2
   - Google Gemini API
   - Trello API
3. Create Google Sheet with columns matching extracted fields above
4. Create Trello board with 3 lists: To Do, Doing, Done
5. Update Trello List IDs in the JavaScript nodes
6. Activate both workflows

> **Note:** No actual credentials or IDs are stored in this file. Connect your own after importing.

---

## Built By

**Saivignesh P** — Agentic AI Engineer
[LinkedIn](https://linkedin.com/in/saivignesh-pandian) · [GitHub](https://github.com/saivigneshpandian)
