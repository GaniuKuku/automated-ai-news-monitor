# Automated #AI News Monitor

<div align="center">

![n8n](https://img.shields.io/badge/n8n-%23FF6D5A.svg?style=for-the-badge&logo=n8n&logoColor=white)
![JavaScript](https://img.shields.io/badge/javascript-%23323330.svg?style=for-the-badge&logo=javascript&logoColor=%23F7DF1E)
![Google Sheets](https://img.shields.io/badge/Google%20Sheets-%2334A853.svg?style=for-the-badge&logo=google-sheets&logoColor=white)
![Airtable](https://img.shields.io/badge/Airtable-18BFFF?style=for-the-badge&logo=Airtable&logoColor=white)
![Telegram](https://img.shields.io/badge/Telegram-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white)
![REST API](https://img.shields.io/badge/REST_API-005571?style=for-the-badge&logo=json&logoColor=white)

</div>

![Architecture Diagram](images/ai.png)

## Overview
An end-to-end automated data pipeline that monitors the web for #AI news, prevents duplicate logging, analyzes the sentiment using rule-based JavaScript logic, and dynamically routes the data to appropriate databases and communication channels.

## Architecture & Data Flow
1. **Extraction:** A Schedule Trigger fires every 15 minutes, calling the **Serper.dev API** to scrape the latest #AI news mentions.
2. **De-Duplication:** A `Compare Datasets` bouncer cross-references incoming URLs against historical records in **Google Sheets** to drop previously processed articles.
3. **Transformation & Logic:** A custom **JavaScript** node processes the text snippets to classify sentiment as Positive, Negative, or Neutral.
4. **Loading & Routing:** - All unique mentions are logged to **Google Sheets** as a master database.
   - A Switch node dynamically routes **Negative** mentions to a **Telegram** bot for immediate team alerts.
   - **Positive** mentions are routed directly into an **Airtable** CRM base for testimonials.

## Tech Stack
* **Orchestration:** n8n
* **APIs:** Serper.dev, Telegram Bot API, Airtable API
* **Languages:** JavaScript, JSON
* **Storage:** Google Sheets, Airtable

## How to Run
1. Install n8n locally or sign up for an n8n cloud account.
2. Download the `workflow.json` file from this repository.
3. In your n8n workspace, go to the Options menu (top right) and click **Import from File**.
4. Upload the JSON file.
5. You will need to supply your own credentials for:
   - Google Sheets OAuth2
   - Serper.dev API Key
   - Telegram Bot Token & Chat ID
   - Airtable Personal Access Token
