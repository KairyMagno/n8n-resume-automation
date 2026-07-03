# AI Resume Analyzer & Candidate Screening System

## Overview
The **AI Resume Analyzer & Candidate Screening System** is an end-to-end recruitment automation solution built with **n8n** and **Groq AI (Llama 3.1)**. The workflow automates resume intake, candidate evaluation, IT developer classification, document management, and applicant communication, significantly reducing manual screening effort for recruiters.

The system receives resumes through email, extracts and analyzes PDF content using AI, classifies candidates as IT Developers or non-IT roles, parses qualified resumes into structured data, generates hiring recommendations, and automatically routes applicants through the appropriate recruitment process.

## Key Features
- Automated resume submission via email
- PDF resume extraction and text processing
- AI-powered candidate evaluation using Groq (Llama 3.1)
- Intelligent IT developer classification and filtering
- Full resume parsing with structured data extraction
- Duplicate detection across multiple submissions
- One-time duplicate notification tracking
- Candidate data storage in Google Sheets (Accepted, Rejected, Duplicate Notified)
- Resume archiving in Google Drive with shareable links
- Automated professional HTML email notifications (Confirmation, Rejection, Duplicate, HR Alert)
- LinkedIn & GitHub profile extraction
- End-to-end workflow automation with no manual intervention

## System Workflow
```text
Candidate Sends Resume (Email + PDF)
                │
                ▼
           IMAP Trigger
                │
                ▼
      PDF Text Extraction
                │
                ▼
      Mini Parse (Groq AI)
                │
                ▼
 Extract Basic Information
 (Full Name, Email Address)
                │
                ▼
 Read Accepted Applicants
                │
                ▼
 Read Rejected Applicants
                │
                ▼
   Combine Applicant Lists
                │
                ▼
      Duplicate Check
                │
                ▼
           Decision Logic
        ┌───────────────┐
        │   IF Node     │
        └──────┬────────┘
               │
      ┌────────┴─────────┐
      ▼                  ▼

 Duplicate            New Applicant
      │                  │
      ▼                  ▼
Read Notified      IT Filter (Groq AI)
Applicants               │
      │                  ▼
      │          Determine if Resume
      │         Matches IT Developer
      │                  │
      │                  ▼
      │            Decision Logic
      │         ┌───────────────┐
      │         │   IF Node     │
      │         └──────┬────────┘
      │                │
      │      ┌─────────┴──────────┐
      │      ▼                    ▼

Already Notified          Non-IT Developer
      │                          │
      ▼                          ▼
     End                  Save to Rejected
                                  │
                                  ▼
                          Send Rejection Email

Not Yet Notified                  IT Developer
      │                                │
      ▼                                ▼
Send Duplicate              Resume Parsing (Groq AI)
Application Email                    │
      │                               ▼
      ▼                      Attach PDF Binary
Save Notification                    │
      │                               ▼
      ▼                     Upload to Google Drive
     End                              │
                                      ▼
                              Generate Drive Link
                                      │
                                      ▼
                           Save to Accepted Sheet
                                      │
                           ┌──────────┴──────────┐
                           ▼                     ▼

                Send Confirmation Email     Notify HR
```

## Technology Stack

### Workflow Automation
- n8n (Self-hosted Docker)

### Artificial Intelligence
- Groq API
- Llama 3.1 (8B Instant)

### Cloud Services
- Gmail API (IMAP + SMTP)
- Google Drive API
- Google Sheets API

### Data Processing
- PDF Extraction
- JSON Processing
- JavaScript Expressions

### Integration & Automation
- REST APIs
- Conditional Logic (Multi-branch IF nodes)
- Email Automation (Professional HTML Templates)
- Document Management

## Google Sheets Structure

### Accepted (Qualified IT Developers):
| Name | Email | Phone | Role | Skills | Experience | Education | Resume Link | LinkedIn | GitHub | Date Applied |

### Rejected (Non-IT Applicants):
| Name | Email | Reason | Date Applied |

### Duplicate Notified (One-time notification tracking):
| Email | Date Notified |

## AI Evaluation Structure

### IT Developer Classification:
```json
{
  "is_it_developer": true,
  "reason": "..."
}
```

## 🚀 Business Value

This workflow automates the early stages of the recruitment process, reducing manual work while ensuring applicants are handled consistently.

### Key Features

- 📥 Automatically collects resumes from incoming emails
- 📄 Extracts and parses resume information from PDF files
- 🤖 Uses AI to identify whether an applicant is an IT developer
- 📊 Performs structured resume parsing for qualified candidates
- 🔍 Detects duplicate applications using applicant records
- 🚫 Prevents duplicate notification spam with one-time alerts
- 📧 Automatically sends appropriate emails to applicants
- ☁️ Archives resumes in Google Drive with shareable links
- 📋 Maintains applicant records in Google Sheets
- 👥 Notifies HR when a qualified IT candidate is received

By leveraging AI-driven screening, recruiters can spend more time interviewing qualified candidates instead of manually reviewing every resume.

---

## 📧 Automated Email Workflow

| Email Type | Recipient | Purpose |
|------------|-----------|---------|
| 🟢 Confirmation | Qualified IT Candidate | Confirms that the application has been received successfully |
| ⚫ Rejection | Non-IT Candidate | Informs the applicant that their profile does not match current IT roles |
| 🟠 Duplicate Notice | Duplicate Applicant | Sends a one-time notification for duplicate applications |
| 🔵 HR Alert | HR Team | Notifies HR of a newly qualified candidate with resume and Drive link |

---

## 🛠️ Skills Demonstrated

- Workflow Automation (28 n8n Nodes)
- AI Integration using Groq LLM
- Google Sheets API Integration
- Google Drive API Integration
- Gmail IMAP & SMTP Automation
- PDF Resume Processing
- Business Process Automation
- Conditional Logic Design (4 IF Nodes)
- Structured Data Management
- Duplicate Detection & Validation
- One-Time Notification System
- HTML Email Template Design
- OAuth 2.0 Authentication
- AI-Powered Recruitment Automation

---

## ⚙️ Setup Instructions

### 1. Import the Workflow

Import **`Resume Automation.json`** into your n8n instance.

### 2. Configure Environment Variables

Replace all placeholder values:

- `YOUR_GROQ_API_KEY`
- `YOUR_EMAIL@gmail.com`
- `YOUR_HREMAIL@gmail.com`
- `YOUR_SHEET_ID`
- `YOUR_DRIVE_FOLDER_ID`

### 3. Configure Credentials

Create and connect the following credentials in n8n:

- Gmail IMAP
- Gmail SMTP
- Google Sheets OAuth2
- Google Drive OAuth2

### 4. Prepare Google Services

Create a Google Sheet with the following tabs:

- Accepted
- Rejected
- Duplicate Notified

Create a Google Drive folder where resumes will be stored.

### 5. Activate the Workflow

Once credentials and resources are configured, enable the workflow and begin receiving applications automatically.

---

## 👨‍💻 Author

**Kairy Ken Magno**

*IT Graduate • AI Automation Enthusiast • Full-Stack Developer*
This project was developed as part of my portfolio to demonstrate practical applications of AI, workflow automation, and business process optimization using modern cloud technologies.
