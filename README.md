# YouTube Research Automation Tool

An automated AI-powered workflow built in n8n that turns a simple topic or keyword into deep viral video research and production-ready YouTube scripts. <br>
<img src="Screenshot 2026-06-06 204201.png" alt="App Screenshot">
## 📌 The Problem

Content creators spend hours searching for video ideas, analyzing what makes a video go viral, writing scripts, and optimization for SEO. This manual process causes several issues:

* **Time Consumption:** Spending hours looking at video stats and typing down video notes manually.
* **Bad Decisions:** Relying on feelings instead of actual numbers to find "outlier" videos that outperform a channel's average subscriber count.
* **Writer's Block:** Staring at a blank page trying to write a good video hook, body script, and description from scratch.

---

## 🚀 The Solution & Impact

This automation turns a multi-hour research and writing process into a **10-second form submission**.

### The Impact

* **Finds True Outliers:** It filters out videos that only got views because the creator is already famous. It finds videos that went viral solely because of a great topic or title.
* **Instant Production Materials:** Generates a full script hook, structured body sections, call-to-actions, description text, and tags.
* **Centralized Database:** Saves every single data point directly into a Google Sheet for easy review and execution.

---

## 🛠️ Tech Stack

* **Automation Platform:** n8n (Advanced AI Agent nodes, HTTP Request nodes, and JavaScript Code nodes)
* **APIs:** YouTube Data API v3, YouTube Transcript API
* **AI Models:** Google Gemini, Nvidia Nemotron-3-Nano (via OpenRouter)
* **Database:** Google Sheets

---

## 📐 System Architecture & Workflow

The entire system is split into three main modules: **Data Collection**, **Outlier Filtering**, and **AI Script Generation**.

```
[User Form Input] ➔ [YouTube API Search] ➔ [Relevance & Outlier Filters]
                                                        │
[Google Sheets] ◀── [Script Gen Agent] ◀── [Transcript & Channel Stats]

```

### 1. Data Collection & Filtering Module

* **YouTube_Topic_Form:** A native n8n form collects the main keyword or topic from the user.
* **YouTube_Search & Details:** Queries the YouTube API for the top 5 most relevant videos.
* **Relevance_Filter:** A custom JavaScript node scores and filters the videos to ensure they match the user's intent.

### 2. The Outlier Engine

* **YouTube_Channel_Details:** Fetches the total subscriber count for each video's channel.
* **Outlier_Filter (The Core Logic):** An n8n IF node checks every video against strict math rules:
1. The video must have more than 1,000 views.
2. **The View Count must be GREATER than the Channel Subscriber Count.** This ensures we only analyze videos that broke out of their regular audience bubble.



### 3. AI Analysis & Script Generation Module

* **Transcript_Scraper:** Scrapes the full text transcript of the passing videos.
* **Free_AI_Analysis_Agent:** Uses Gemini/Nemotron to analyze the original transcript and discover *why* the video went viral.
* **Script_Generator_Agent:** Takes the viral reasons, the original structure, and the topic to build a brand new script (Hook, Body, CTA) and SEO metadata.
* **Final_Storage_Sheets:** Saves all the generated scripts, data, and thumbnail ideas cleanly into a Google Sheet.

---

## 📊 Database Schema (Google Sheets Output)

The automation saves data using the following structured columns:

| Column Name | Description |
| --- | --- |
| **Search_Topic** | The original keyword entered into the form |
| **Original_Title** | The title of the viral video found |
| **Video_Views / Subscribers** | Performance metrics to prove it is an outlier |
| **Viral_Reason** | AI analysis explaining why the video succeeded |
| **New_Title / SEO_Title** | Optimized title variations for the new video |
| **Hook_Script** | The first 30 seconds designed to stop the scroll |
| **Body_Script / CTA_Script** | The main content sections and the ending sign-off |
| **Thumbnail_Concepts** | Text descriptions of visual ideas for the thumbnail |

---

## ⚙️ Setup Instructions

1. **Import the Workflow:** Download the `freeyoutuberesearchautomation.json` file from this repo and paste it into your n8n canvas.
2. **Add API Keys:** * Configure your **YouTube Data API Key** inside the HTTP Request nodes.
* Connect your **OpenRouter** or **Google Gemini** accounts to the AI Chat Model nodes.

3. **Connect Google Sheets:** Create a Google Sheet with the headers listed in the schema table above, and link it inside the `Final_Storage_Sheets` node.
4. **Execute:** Click "Execute Workflow", fill out the form, and watch your sheet fill up with scripts.

---
