# SOCIAL MEDIA MONITORING AND ALERTS WORKFLOW

# TABLE OF CONTENTS
- [CATEGORY](#category)
- [DETAILED DESCRIPTION](#detailed-description)
- [HOW IT WORKS (FUNCTIONALITY)](#how-it-works-functionality)
  -    [TRIGGER](#trigger)
  -    [DATA RETRIEVAL](#data-retrieval)
  -    [SENTIMENT ANALYSIS (RULE-BASED)](#sentiment-analysis-rule-based)
  -    [BRANCHING](#branching)
  -    [ACTION PER BRANCH](#actions-per-branch)
- [TOOLS REQUIRED](#tools-required)
- [SIZE OF PROJECT](#size-of-project)
- [SETUP REQUIREMENTS](#setup-requirements)
- [DEPLOYMENT TIME ESTIMATE](#deployment-time-estimate)
- [VALUE PROPOSITION (ROI)](#value-proposition-roi)
- [KNOWN LIMITATIONS](#known-limitations)
- [USE CASES](#use-cases)
- [VERSION UPDATES](#version-updates)


# Category
Marketing / Brand Monitoring / Public relations

<img width="1536" height="1024" alt="COVER IMAGE" src="https://github.com/user-attachments/assets/554cfcc2-88db-4d84-9861-adb321cac05b" />

<img width="1302" height="693" alt="social media monitoring and alerts v2" src="https://github.com/user-attachments/assets/d1069e52-1660-4d81-a1e7-b4a2c77db87c" />

# Detailed Description
This workflow automates the monitoring of brand mentions and industry-related keywords across social media and online news
Businesses/institutions need real-time awareness of how they are being discussed online, whether positively (for testimonials) or negatively (for crisis management and damage control). 

Instead of manually searching platforms, this system uses **n8n** to fetch mentions and thread posts from **Twitter/X** and articles or blogs in **Google News**, applies **rule-based sentiment classification**, and routes results to the appropriate destinations:

-  **Positive coverage** → Recorded in **Airtable** and logged in **Google Sheets** for testimonials and marketing.
-  **Negative coverage** → Trigger immediate **alerts to the team via Telegram & Slack**, and log into Google Sheets for monitoring.
-  **Neutral coverage** → Logged into Google Sheets only, providing a complete record for future analysis.

This workflow runs automatically every **15 minutes**, ensuring teams never miss key online discussions.

You can watch my DEMO video [HERE](https://drive.google.com/file/d/1U5OVnqKIw6XjgL2qGJPyc7YwPui-1PrV/view?usp=sharing)

You can download the JSON file [HERE](https://github.com/paschaldubem/SOCIAL-MEDIA-MONITORING-AND-ALERTS-WORKFLOW/blob/main/Social%20Media%20Monitoring%20%26%20Alerts%20%20Workflow.json)


# **How It Works (Functionality)**
## **Trigger**
-  The scheduler triggers the workflow every **15 minutes**.
<img width="1876" height="892" alt="Screenshot 2025-09-19 140145" src="https://github.com/user-attachments/assets/bedc045a-6ce6-4906-b107-fed4d8c150f2" />

## **Data Retrieval**
-  **Twitter/X Search Node** – Fetches tweets with specified keywords/hashtags and mentions.
<img width="1915" height="931" alt="Screenshot 2025-09-19 140304" src="https://github.com/user-attachments/assets/04f6a170-8585-4811-a777-1ab54121a211" />

-  **Google News (Serper.dev API)** – Retrieves recent news articles mentioning the same keywords.
<img width="1914" height="933" alt="Screenshot 2025-09-19 140511" src="https://github.com/user-attachments/assets/9f74e934-f5af-4696-b284-8294879d5413" />

## **Sentiment Analysis (Rule-Based)**
-  **Custom Function Node**: Assigns sentiment values by scanning content for defined keywords:
    -  Positive keywords → Positive sentiment
    -  Negative keywords → Negative sentiment
    -  Neither → Neutral sentiment
<img width="1916" height="946" alt="Screenshot 2025-09-19 140642" src="https://github.com/user-attachments/assets/c100c637-8d80-4671-87fc-e49ec28be350" />

## **Branching**
-  **Switch Node** separates results into **Positive, Neutral**, and **Negative** sentiment branches.
<img width="1907" height="933" alt="Screenshot 2025-09-19 140857" src="https://github.com/user-attachments/assets/5ab8bfec-8996-42cd-86f8-a5abb7a1892c" />

## **Actions per Branch**
**Positive**:
-  Record in Airtable (Testimonials table).
 <img width="1918" height="936" alt="Screenshot 2025-09-19 141029" src="https://github.com/user-attachments/assets/d2a89370-cc5f-4f1b-a46f-a97c0b7f422d" />
 
-  Append/update row in Google Sheets (“Positive Coverage”).
 <img width="1900" height="918" alt="Screenshot 2025-09-19 141211" src="https://github.com/user-attachments/assets/2a703a77-c70f-4bb8-b86f-37a4de0cc599" />


**Neutral**:
-  Append/update row in Google Sheets (“Neutral Coverage”)
<img width="1896" height="924" alt="Screenshot 2025-09-19 141318" src="https://github.com/user-attachments/assets/cbc24bf8-e2e7-430f-beec-336cecfa326d" />


**Negative**
-  Send real-time alerts via Telegram (headline + content + source link).
<img width="1903" height="932" alt="Screenshot 2025-09-19 141614" src="https://github.com/user-attachments/assets/f89dfb13-463a-4cfe-860f-8319f812db56" />


-  Send a team alert to the designated *#social channel* (headline + content + source link) via Slack.
<img width="1901" height="921" alt="Screenshot 2025-09-19 141701" src="https://github.com/user-attachments/assets/69853029-7923-4399-9bc1-b29eeeda6c38" />

-  Append/update row in Google Sheets (“Negative Coverage”).
<img width="1898" height="920" alt="Screenshot 2025-09-19 141759" src="https://github.com/user-attachments/assets/01868dfd-dc2c-4986-a9d1-d9fd7f7c7b01" />


# **Tools Required**
-  **n8n** (automation orchestrator)
-  **Twitter/X API** (tweet search) has a free tier but a basic subscription is recommended
-  **Serper.dev API** (Google News search) free tier
-  **Airtable** (positive testimonials storage) free plan but a paid plan is recommended
-  **Google Sheets** (centralized reporting/logs) free google console plan is sufficient
-  **Telegram Bot API** (negative coverage alerts) free plan is sufficient
-  **Slack API** (team notifications) premium plan is recommended.

# **Size of Project**
**Medium** (≈6 tasks: scheduling, data retrieval, sentiment analysis, Airtable logging, Google Sheets logging, and Telegram/Slack notifications).

# **Setup Requirements**
-  Twitter/X API credentials (bearer token, client ID).
-  Serper.dev API key (Google News search).
-  Airtable base + API key (for testimonials).
-  Google Sheets API credentials (for logging).
-  Telegram bot token + chat ID.
-  Slack app token or webhook URL

# **Deployment Time Estimate**
-  Setup & configuration: 1–4 days
-  Customization (keywords, sentiment rules, reporting): **3–5 days**.

# **Value Proposition (ROI)**
For marketing, PR, and brand image monitoring teams:
-  Saves **10+ hours per week** of manual brand monitoring.
-  Provides **real-time crisis alerts** → faster response to negative sentiment.
-  Builds a database of **positive testimonials** for marketing campaigns.
-  Centralizes all results into a single **Google Sheets spreadsheet** for analysis.

# **Known Limitations**
-  **Rule-based sentiment** may misclassify sarcasm or nuanced posts.
-  API rate limits: Twitter and Google News restrict query volumes on free tier accounts.
-  The Airtable free plan is limited to **1,000 records** per base.
-  Telegram & Slack require a stable internet connection.

# **Use Cases**
-  Tested internally: the workflow flagged negative posts (with the *“backlash”* keyword) for ESCP business school-related posts within 15 minutes.
-  The marketing team leveraged positive mentions from Airtable for testimonial campaigns.
-  The PR team reduced average response time to negative press mentions by **~60%**.

# **Version Updates**
-  **v1.0** – Initial release: Google News + sentiment branching.
-  **v1.1** – Added Slack and Telegram team alerts.
-  **v1.2** – Airtable integration for positive testimonials.
-  **v1.3** - Added twitter feed monitoring for wider news coverage
-  **Planned** – Dashboard visualization (Looker Studio or Supabase) for advanced reporting.


