# 🚀 Auto Dialer Tool – Sprint Plan (Windsurf Implementation)

## 🗓️ Sprint Overview

- **Sprint Duration:** 2 weeks per sprint
- **Total MVP Timeline:** 4 weeks (2 sprints)
- **Team Composition (Agents):**
  - `@frontend-agent`: React UI and real-time updates
  - `@backend-agent`: API, auth, call routing logic
  - `@crm-agent`: CRM integration & sync workflows
  - `@telephony-agent`: Dialing engine using Twilio/Plivo
  - `@qa-agent`: Test coverage, automated checks
  - `@pm-agent`: Workflow scaffolding and backlog syncing

---

## 🧭 Sprint 0: Setup & Planning (Pre-Sprint Week)

### Goals
- Define technical architecture
- Set up repo, CI/CD, and Windsurf scaffolding
- Confirm CRM and dialer APIs
- Finalize user stories and backlog

### Tasks
- [ ] Configure Windsurf agents and environments
- [ ] Define backend service structure (FastAPI/Node)
- [ ] Confirm Twilio credentials and CRM OAuth flows
- [ ] Finalize data model (user, contact, call, log)
- [ ] Create mock contact and call queue data

---

## 🚀 Sprint 1: CRM + Dialer MVP (Weeks 1–2)

### Sprint Theme
Integrate CRM, basic dialing engine, and core call queue features.

### Goals
- Enable user login and team setup
- Sync CRM contacts to local DB
- Build functional auto-dialer with preview/progressive mode
- Log call outcomes and notes

### Epics Covered
- EPIC 1: Authentication & Teams
- EPIC 2: CRM Integration (partial)
- EPIC 3: Dialer Functionality (basic)
- EPIC 5: Call Logging

### Tasks

#### `@frontend-agent`
- [ ] Build login/signup form with role-based access
- [ ] Display contact queue and preview panel
- [ ] Basic dialer controls (Start, Skip, Pause)

#### `@backend-agent`
- [ ] Implement user auth & token middleware
- [ ] Build contact import + call queue endpoints
- [ ] Save call logs and notes to DB

#### `@crm-agent`
- [ ] OAuth CRM connection (Salesforce)
- [ ] Sync lead/contact list on schedule
- [ ] Map contact fields to local schema

#### `@telephony-agent`
- [ ] Connect Twilio SDK
- [ ] Implement outbound call trigger
- [ ] Setup call wrap-up handler

#### `@qa-agent`
- [ ] Write tests for user login and call API
- [ ] Simulate call queue and log coverage

#### `@pm-agent`
- [ ] Review story point velocity and update backlog
- [ ] Coordinate QA staging test case coverage

### Deliverables
- Login → CRM connect → Contact queue → Dialer UI
- Successful outbound call and log back to system
- First functional MVP loop

---

## 🚀 Sprint 2: Logging + Analytics + DNC Compliance (Weeks 3–4)

### Sprint Theme
Enhance tracking, reporting, and compliance for production readiness.

### Goals
- Add call dispositions, notes, and sync to CRM
- Generate team performance dashboards
- Implement Do-Not-Call suppression logic
- Improve error handling and UX polish

### Epics Covered
- EPIC 2: CRM Integration (complete)
- EPIC 5: Call Logging
- EPIC 6: Analytics
- EPIC 7: Compliance
- EPIC 8: Smart Queueing (starter logic)

### Tasks

#### `@frontend-agent`
- [ ] Call disposition + notes modal
- [ ] Basic analytics dashboard (calls/day, answer rate)
- [ ] DNC warning banner in dialer view

#### `@backend-agent`
- [ ] DNC list management (import + match)
- [ ] Disposition tagging + note saving
- [ ] Aggregate reporting endpoint (org/team/user)

#### `@crm-agent`
- [ ] Push call results & notes back to CRM
- [ ] Sync log status per contact update

#### `@telephony-agent`
- [ ] Add retry logic + webhook fallbacks
- [ ] Trigger whisper/barging stub endpoint (if supported)

#### `@qa-agent`
- [ ] Full regression test suite
- [ ] CRM sync test coverage (mock API + sandbox)

#### `@pm-agent`
- [ ] Draft release checklist
- [ ] Coordinate demo walkthroughs with team

### Deliverables
- Contact DNC-aware dialing flow
- Agent activity report by user/team/org
- Logged calls synced back to CRM
- Fully tested, demoable MVP v1

---

## 🎯 Post-MVP (Sprint 3+ Roadmap)

| Feature                  | Epic        |
|--------------------------|-------------|
| Whisper/Monitor/Barge    | EPIC 3      |
| Smart dial prioritization| EPIC 8      |
| Multi-language support   | EPIC 7      |
| SMS follow-ups           | EPIC 8      |
| AI-generated call notes  | EPIC 5/8    |
| Campaign segmentation    | EPIC 9      |
| Role-based dashboards    | EPIC 6/9    |

---

## ✅ Acceptance Criteria

- Users can sign in, sync CRM, and auto-dial a real contact
- Each call is logged with outcome, notes, and contact history
- All contacts are checked against DNC list before dialing
- Managers can view activity dashboards for their teams

---

## 🧠 Windsurf Agent Notes

- `@frontend-agent` should use modular Tailwind + HeadlessUI
- `@backend-agent` to structure API with async jobs for queueing
- `@crm-agent` handles sync retries + failure flags
- `@telephony-agent` should isolate vendor logic in adapter layer
- `@qa-agent` should use schema mocks + snapshot tests
