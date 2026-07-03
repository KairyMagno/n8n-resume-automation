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
CANDIDATE SENDS RESUME (Email with PDF Attachment)
          │
          ▼
📧 EMAIL TRIGGER (IMAP)
          │
          ▼
📄 EXTRACT FROM FILE (PDF)
          │
          ▼
🔧 MINI PARSE PROMPT
          │
          ▼
🌐 MINI PARSE GROQ
          │
          ▼
🔧 MINI PARSE EXTRACT
{ full_name, email }
          │
          ▼
📊 READ ACCEPTED SHEET
          │
          ▼
📊 READ REJECTED SHEET
          │
          ▼
🔧 COMBINE SHEETS
          │
          ▼
🔧 CHECK DUPLICATE
{ is_duplicate, resume_email }
          │
          ▼
🔀 IF NEW APPLICANT?
          │
     ┌────┴────┐
     ▼         ▼
❌ DUPLICATE   ✅ NEW
     │         │
     ▼         ▼
📊 READ       🔧 IT FILTER PROMPT
NOTIFIED      │
SHEET         ▼
     │        🌐 IT FILTER GROQ
     ▼         │
🔧 CHECK      ▼
NOTIFIED      🔧 IT FILTER EXTRACT
     │        { is_it_developer, reason }
     ▼         │
🔀 NOT          ▼
NOTIFIED?      🔀 IF IT DEVELOPER?
     │              │
┌────┴────┐    ┌────┴────┐
▼         ▼    ▼         ▼
ALREADY   NOT  NON-IT   IT DEV
(STOP)    │    │         │
          │    ▼         ▼
          │  📊 SAVE    🔧 RESUME
          │  REJECTED   PARSE PROMPT
          │    │         │
          │    ▼         ▼
          │  ✉️ REJECT  🌐 RESUME
          │  EMAIL      PARSE GROQ
          │              │
          │              ▼
          │            🔧 RESUME
          │            PARSE EXTRACT
          │              │
          │              ▼
          │            🔧 ADD BINARY
          │              │
          │              ▼
          │            📂 UPLOAD TO DRIVE
          │              │
          │              ▼
          │            🔧 DRIVE LINK
          │              │
          │              ▼
          │            📊 SAVE TO ACCEPTED
          │              │
          │         ┌────┴────┐
          │         ▼         ▼
          │    ✉️ CONFIRM   📧 HR
          │    EMAIL        NOTIFY
          │
          ▼
     ✉️ DUPLICATE EMAIL
          │
          ▼
     🔧 NOTIFIED DATA
          │
          ▼
     📊 SAVE TO NOTIFIED


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

Business Value
This solution automates several time-consuming recruitment tasks:

Resume collection and organization

Initial candidate screening and IT developer classification

Qualification assessment and structured resume parsing

Duplicate application detection and prevention

One-time duplicate notification (no spam)

Applicant communication (4 email types)

Resume archiving with searchable Google Drive links

Candidate record management in structured spreadsheets

By leveraging AI-driven evaluation, recruiters can focus on interviewing qualified IT developers instead of manually reviewing every application.

Email Automation
Email Type	Recipient	Purpose
Confirmation (Green)	IT Candidate	Application received confirmation
Rejection (Dark)	Non-IT Candidate	Profile doesn't match IT roles
Duplicate Notice (Orange)	Repeat Applicant	One-time notification - sent only once
HR Alert (Blue)	HR Team	New qualified candidate summary with links
Skills Demonstrated
This project showcases:

Workflow Automation (28 nodes)

AI Integration (3 Groq API calls)

API Integration (Google Sheets, Drive, Gmail)

Business Process Automation

PDF Document Processing

Conditional Logic Design (4 IF nodes)

Data Management (3 Google Sheets tabs)

Cloud Service Integration (OAuth 2.0)

Recruitment Process Automation

Duplicate Detection Logic

One-Time Notification System

Professional Email Design (HTML/CSS)

Setup Instructions
Import Resume Automation.json into n8n

Replace all YOUR_* placeholders:

YOUR_GROQ_API_KEY - Get from console.groq.com

YOUR_EMAIL@gmail.com - Your Gmail address

YOUR_HREMAIL@gmail.com - HR/Recruitment email

YOUR_SHEET_ID - Google Sheet ID

YOUR_DRIVE_FOLDER_ID - Google Drive folder ID

Configure credentials in n8n:

IMAP (Gmail)

SMTP (Gmail)

Google Sheets OAuth2

Google Drive OAuth2

Create Google Sheet with tabs: Accepted, Rejected, Duplicate Notified

Create Google Drive folder for resume storage

Activate the workflow

Author
Kairy Ken Magno

IT Graduate | AI Automation Enthusiast | Full-Stack Developer

This project was developed as part of my portfolio to demonstrate practical applications of AI, workflow automation, and business process optimization using modern cloud technologies.
