# 📊 Auto Dialer Tool – Data Model

## 1. Users

| Field         | Type      | Description                          |
|--------------|-----------|--------------------------------------|
| user_id      | UUID (PK) | Unique identifier for the user       |
| name         | String    | Full name                            |
| email        | String    | Email address                        |
| role         | Enum      | SDR, Manager, Admin                  |
| team_id      | UUID (FK) | Associated team                      |
| crm_user_id  | String    | CRM platform user ID                 |
| created_at   | Timestamp | Account creation time                |

---

## 2. Teams

| Field    | Type      | Description              |
|---------|-----------|--------------------------|
| team_id | UUID (PK) | Unique team ID           |
| name    | String    | Team name (e.g. SDR West)|
| org_id  | UUID (FK) | Associated organization  |

---

## 3. Organizations

| Field           | Type      | Description                     |
|----------------|-----------|---------------------------------|
| org_id         | UUID (PK) | Unique org ID                   |
| name           | String    | Organization name               |
| crm_type       | Enum      | Salesforce, HubSpot, Zoho, etc.|
| crm_auth_token | String    | Encrypted API token             |
| plan_type      | Enum      | Free, Pro, Enterprise           |

---

## 4. Contacts

| Field          | Type      | Description                       |
|---------------|-----------|-----------------------------------|
| contact_id     | UUID (PK) | Internal contact ID               |
| crm_contact_id | String    | External CRM ID                   |
| org_id         | UUID (FK) | Associated organization           |
| name           | String    | Full name                         |
| email          | String    | Email address                     |
| phone_number   | String    | Primary phone number              |
| timezone       | String    | IANA timezone                     |
| lead_score     | Integer   | CRM-derived lead score            |
| stage          | Enum      | Prospect, Qualified, Closed, etc. |

---

## 5. CallSessions

| Field            | Type      | Description                         |
|------------------|-----------|-------------------------------------|
| call_id          | UUID (PK) | Unique call ID                      |
| user_id          | UUID (FK) | Caller user ID                      |
| contact_id       | UUID (FK) | Contact being called                |
| start_time       | Timestamp | Call start time                     |
| end_time         | Timestamp | Call end time                       |
| duration_seconds | Integer   | Duration in seconds                 |
| outcome          | Enum      | Connected, Voicemail, No Answer     |
| disposition      | String    | Custom outcome label                |
| recording_url    | String    | URL to call recording               |
| notes            | Text      | Call notes                          |

---

## 6. CallQueue

| Field          | Type      | Description                         |
|---------------|-----------|-------------------------------------|
| queue_id       | UUID (PK) | Unique queue ID                     |
| user_id        | UUID (FK) | Assigned user                       |
| contact_id     | UUID (FK) | Contact to call                     |
| priority       | Integer   | Sort order or urgency               |
| scheduled_time | Timestamp | Time to dial                        |
| status         | Enum      | Queued, Skipped, Completed          |

---

## 7. CRMLog

| Field           | Type      | Description                     |
|-----------------|-----------|---------------------------------|
| log_id          | UUID (PK) | Unique log ID                   |
| crm_object_type | Enum      | Contact, Call, Note, etc.       |
| crm_object_id   | String    | External CRM object ID          |
| action          | Enum      | Created, Updated, Deleted       |
| status          | Enum      | Success, Failed                 |
| timestamp       | Timestamp | When sync occurred              |
| message         | String    | Debug or error info             |

---

## 8. AnalyticsSnapshot

| Field             | Type      | Description                         |
|------------------|-----------|-------------------------------------|
| snapshot_id       | UUID (PK) | Unique snapshot ID                  |
| org_id            | UUID (FK) | Associated organization             |
| date              | Date      | Snapshot date                       |
| calls_made        | Integer   | Number of calls made                |
| avg_duration      | Float     | Average call length                 |
| connection_rate   | Float     | Percent of calls connected          |
| talk_time_minutes | Float     | Total time spent talking (minutes)  |

---

## 9. DNCSuppressionList

| Field            | Type       | Description                         |
|------------------|------------|-------------------------------------|
| phone_number     | String PK  | Phone number to suppress            |
| reason           | String     | Reason for suppression (e.g. DNC)   |
| added_by_user_id | UUID (FK)  | User who added suppression          |
| added_at         | Timestamp  | Date added                          |

---

## 🔗 Relationships

- Users → belong to Teams and Organizations
- Organizations → own Contacts
- Users → make CallSessions to Contacts
- CallQueue → schedules Contacts for Users
- CRMLog → tracks CRM sync for Contacts and Calls
- DNCSuppressionList → blocks dialing of specified numbers
- AnalyticsSnapshot → summarizes daily activity per Org
