# CCPAY — Digital Coupon System (Archive)

## Overview
CCPAY is a web-based digital coupon system developed for CC CUP, a large-scale school event at SMA Kolese Kanisius Jakarta.

The system replaces traditional paper coupons with a centralized digital platform, similar in concept to an e-wallet (e.g. GoPay), allowing users to store and use coupons securely and efficiently.

---

## ⚠️ Repository Status
This repository serves as an **archival version** of the project.

The original development repository (including full commit history) is no longer available.  
This repo was recreated to document the system architecture, implementation, and key learnings from the project.

---

## Project Scale
- 👥 ~1600 internal users  
- 🧾 ~1300 registrants  
- 💰 ~USD 50,000 in transactions  
- ⚡ Peak usage: hundreds of concurrent users  
- 📅 Duration: 7 days (live deployment)

---

## Features
- Digital coupon balance system (e-wallet style)
- QR-based transactions (top-up & payment)
- Google OAuth authentication
- Role-based access (Admin & User)
- Transaction logging system
- Admin panel for monitoring and issue handling

---

## Tech Stack
**Frontend**
- React.js (main system)
- HTML + Jinja (registration)

**Backend**
- Express.js (CCPAY core)
- Flask (registration service)

**Database**
- PostgreSQL

**Infrastructure**
- Heroku (hosting)

**Authentication**
- Google OAuth (JWT-based session)

---

## System Design (Simplified)
User → Frontend (React) → Backend (Express) → Database (PostgreSQL)

- Authentication handled via Google OAuth
- Transactions processed through backend API
- Logs recorded for monitoring and auditing

---

## Security & Reliability Notes

During development and deployment, several important system considerations were identified:

### Input Validation
A vulnerability was discovered where negative input values could incorrectly modify user balance.

**Fix:**
- Implemented stricter validation rules
- Ensured all transaction values follow logical constraints

---

### Logging & Monitoring
All transactions were logged and used for:
- Debugging
- Anomaly detection
- Transaction tracing

Example case:
- Detection of incorrect transaction value (Rp 35 instead of Rp 35,000) via log tracing

---

### Session Control
- JWT-based authentication
- Single-device session limitation to reduce misuse

---

### Platform Constraints
- Heroku request timeout (30s) affected image uploads during registration
- Identified and mitigated during live deployment

---

## QA & Testing Approach

Testing was performed manually with a focus on **real-world user behavior simulation**, including:

- Normal user interaction
- Edge cases
- Potential misuse scenarios

This approach helped identify critical vulnerabilities and improve system robustness before and during deployment.

---

## Lessons Learned
- Input validation is critical in financial-like systems
- Logging is essential for debugging and security auditing
- Real-world usage reveals issues not visible during development
- QA plays a key role in system security, not just functionality

---

## Credits
Developed by the Digital Infrastructure Team — CC CUP

Special mention:
- Aric Hartono (Quality Assurance & Bug Testing)
