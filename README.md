# 🚀 n8n Job Scraper & Resume Matcher Workflow

This project is an **automated job scraping and matching workflow** built with [n8n](https://n8n.io/) and self-hosted using **Docker**.  

It scrapes job postings via the **ScrapingDog API**, processes them with **Google Gemini (PaLM)**, enriches them with your **resume details**, and stores results into a **Google Sheet** — including **personalized cover letters** and a **match score** against your resume.  

---

## 📌 Workflow Overview

![Workflow Screenshot](./workflow.png) <!-- Add your screenshot here -->

The workflow consists of the following steps:

1. **Schedule Trigger** → Runs daily at a set time.  
2. **HTTP Request** → Calls ScrapingDog `google_jobs` API to fetch job postings.  
3. **Message a Model (Gemini)** → Cleans and extracts structured job data.  
4. **Edit Fields** → Injects resume text.  
5. **Message a Model 1 (Gemini)** → Generates `match_score` and a personalized `cover_letter`.  
6. **Code Node** → Parses AI response into JSON.  
7. **Google Sheets** → Appends/updates structured results in a spreadsheet.  

---

## ⚙️ Setup Instructions

### 1. Clone Repo
```bash
git clone https://github.com/your-username/n8n-job-matcher.git
cd n8n-job-matcher
````

### 2. Docker Setup

Create a `docker-compose.yml` (example):

```yaml
version: '3.1'

services:
  n8n:
    image: n8nio/n8n
    ports:
      - "5678:5678"
    environment:
      - N8N_BASIC_AUTH_ACTIVE=true
      - N8N_BASIC_AUTH_USER=admin
      - N8N_BASIC_AUTH_PASSWORD=admin
      - SCRAPINGDOG_API_KEY=${SCRAPINGDOG_API_KEY}
      - GOOGLE_API_KEY=${GOOGLE_API_KEY}
    volumes:
      - ./n8n_data:/home/node/.n8n
```

Start n8n:

```bash
docker compose up -d
```

Access at: [http://localhost:5678](http://localhost:5678)

---

### 3. Import Workflow

* Open n8n dashboard → **Workflows** → **Import from File**.
* Upload `job-matcher-workflow.json`.

---

### 4. Configure Credentials

Inside n8n, set up:

* **ScrapingDog API Key**
* **Google Gemini (PaLM) API**
* **Google Sheets OAuth2**

⚠️ **Important:**

* Store real keys in `.env` (never commit them).
* Commit only `.env.example` with placeholders.

---

## 📊 Output in Google Sheets

Each job posting will be stored with:

* Job Title
* Company Name
* Location
* Job Type
* Posted Days Ago
* Description Summary
* Responsibilities
* Qualifications
* Salary
* Apply Links
* Match Score
* Cover Letter

---

## 📜 License

MIT License — free to use and modify.

---

## 🙌 Author

**Rahul Kumar** – Data Analyst & Data Science Enthusiast

* [LinkedIn](https://www.linkedin.com/in/rahulkumar19k8/)
* [GitHub](https://github.com/rahulkumar-24)

```

---


```
