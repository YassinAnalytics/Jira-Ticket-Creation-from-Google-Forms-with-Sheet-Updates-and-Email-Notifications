# Jira-Ticket-Creation-from-Google-Forms-with-Sheet-Updates-and-Email-Notifications
Automated workflow that creates Jira issues directly from Google Forms. The flow validates and normalizes the data, creates the Jira issue, writes the key back to the Google Sheet, and sends a Gmail notification.


## Context
This template bridges lightweight Google Forms with enterprise Jira. It enables instant ticket creation while keeping Jira the single source of truth. The flow is idempotent (no duplicates) and production-friendly, with clean field normalization and safe mappings.

## Target Users
- Product / Ops teams running request portals on Google Forms
- Engineering managers who need quick Jira integration without custom UI
- Project managers who track intake in Google Sheets but want Jira as the system of record
- Orgs that want controlled ticket creation without exposing Jira directly
  
## Technical Requirements
- Jira Cloud project + API email + API token + “Create issues” permission
- Google Form + response Sheet
- Gmail credential for notifications

## Workflow Steps

<img width="1416" height="594" alt="image" src="https://github.com/user-attachments/assets/a9d025b8-78d8-4c0b-8a04-897f316dad1e" />


- Trigger when a row is added
- Normalize Fields – Trim/clean text
- Create Jira Issue – POST to Jira REST; safe mappings
- Update Google Sheet – Match by Horodateur or rowNumber; write jira_key, issue_url, status, updated_at.
- Send Gmail – HTML email with key, title, link, priority, requester.

  
## Key Features
- Real-time (no polling): Forms → trigger→ n8n
- Idempotent updates using the Form timestamp (“Horodateur”)
- Clean normalization: summary/description/labels all standardized once
- Safe Jira mappings: priority via ID
- Notification: branded HTML email with all key fields

## Expected Output
- Google Form to create the issue

<img width="566" height="816" alt="image" src="https://github.com/user-attachments/assets/47951fbc-96eb-4766-a157-fe05afa17348" />

- Sheet updated with jira_key, issue_url, status, updated_at

<img width="1770" height="678" alt="image" src="https://github.com/user-attachments/assets/e4707f70-f122-4c73-bec9-286470f0697a" />

- A valid Jira issue in the configured project
- 
<img width="1490" height="617" alt="image" src="https://github.com/user-attachments/assets/3f05bb33-8236-4e91-b35e-eb4568cd24a9" />

- Email sent to stakeholders / requester

<img width="558" height="365" alt="image" src="https://github.com/user-attachments/assets/feed62c2-2af8-4e33-9ed1-951f308a5d41" />

## How it works

⏰ Trigger – As soon as a row is added, the workflow is triggered

🧱 Normalize – Clean summary/description/labels; pick reporter_email

🧾 Create – POST to /rest/api/3/issue, capture { id, key, self }

📗 Update – Write jira_key, issue_url, status, updated_at back to the Sheet

✉️ Notify – Send Gmail HTML confirmation to stakeholders/requester

## Tutorial video:
https://www.youtube.com/watch?v=SP_GAyBfv0Q

## Link
Get the free template here: https://n8n.io/workflows/8447-jira-ticket-creation-from-google-forms-with-sheet-updates-and-email-notifications/



