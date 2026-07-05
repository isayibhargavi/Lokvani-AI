# LokVani AI - Multilingual Community Grievance Intelligence Platform

A production-ready, AI-powered platform for Indian citizens to report civic issues in any Indian language via text, voice, or image. AI automatically detects duplicates, estimates population impact, calculates risk scores, routes complaints to government representatives, and highlights high-risk cases for immediate action.

## Features

### Citizen Features
- **Multilingual complaint submission** in 16+ Indian languages
- **Text, voice, and image** input modes
- **AI-generated descriptions** from uploaded media (Gemini Vision integration ready)
- **Live AI preview** of risk score, severity, urgency, and priority
- **Smart validation** with spam detection and meaningful-character counting
- **Complaint tracking** with status timelines and official replies
- **Duplicate detection** - similar complaints are auto-merged with support count increase

### Government Official Features
- **Analytics dashboard** with trend charts, category breakdowns, and district comparisons
- **Critical complaints section** - complaints with Risk >= 85% are pinned to the top with red alert styling
- **Smart search** - natural language queries like "Show water problems in Hyderabad"
- **Sorting** by risk, priority, population, duplicate count, newest, oldest, department, district
- **Representative assignment** - assign complaints to government officials
- **Escalation** - mark complaints as emergency or escalate to higher authority
- **Email routing** - complaints auto-forwarded to the right representative

### Admin Features
- **User management** with role assignment (citizen, official, admin)
- **Complaint moderation** with delete capability
- **Representative management** - view all government contacts
- **Platform-wide statistics** and analytics

### AI Capabilities
- **Duplicate detection** using n-gram text similarity, title similarity, voice transcript similarity, GPS proximity, and category matching (90% threshold for auto-merge)
- **Risk prediction** considering duplicate count, category, population, nearby schools/hospitals, road traffic, complaint age, and historical patterns
- **Population estimation** using duplicate count, district density, category baseline, and user estimates
- **Department routing** - auto-assigns complaints to the correct government department
- **Suggested actions** and estimated resolution times per category
- **Summarization** and title generation
- **Translation** across 7 Indian languages with script-based detection

## Tech Stack

- **Frontend**: Next.js 13.5 (App Router), TypeScript, TailwindCSS, ShadCN UI, Framer Motion, Recharts
- **Backend**: Supabase (PostgreSQL, Auth, RLS, Edge Functions)
- **AI**: In-browser n-gram vectorization, cosine similarity, keyword-weighted risk scoring (Gemini API ready)
- **Email**: Edge function with Nodemailer (SMTP/Gmail API ready)

## Getting Started

### Prerequisites
- Node.js 20+
- npm or yarn

### Installation

```bash
npm install
npm run dev
```

Open [http://localhost:3000](http://localhost:3000)

### Demo Accounts

- **Citizen**: `citizen@lokvani.gov.in` / `LokVaniDemo2024!`
- **Official**: `official@lokvani.gov.in` / `LokVaniDemo2024!`
- **Admin**: `admin@lokvani.gov.in` / `LokVaniDemo2024!`

## REST API

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/complaints` | POST | Submit a new complaint with full AI pipeline |
| `/api/analyze-media` | POST | Analyze uploaded media and return description + risk |
| `/api/generate-description` | POST | Generate complaint description from media |
| `/api/check-duplicate` | POST | Check for duplicate complaints |
| `/api/send-email` | POST | Queue email to a representative |
| `/api/dashboard` | GET | Aggregated dashboard analytics |
| `/api/high-risk` | GET | Complaints with risk_score >= 85 |
| `/api/statistics` | GET | Platform-wide statistics |
| `/api/representatives` | GET | List government representatives |
| `/api/ai/analyze` | POST | AI analysis of complaint text |
| `/api/ai/duplicates` | POST | Duplicate detection |
| `/api/ai/search` | POST | Smart natural-language search |
| `/api/ai/translate` | POST | Translation |

## Database Schema

### Core Tables
- `profiles` - User accounts with roles (citizen, official, admin)
- `categories` - Complaint categories (road, water, electricity, etc.)
- `complaints` - Core complaint records with AI metadata, location, routing
- `complaint_images` - Image attachments
- `voice_files` - Voice recordings with transcripts
- `translations` - Multilingual translations
- `merged_complaints` - Duplicate merge records
- `status_history` - Status change timeline
- `risk_analysis` - AI risk/severity/urgency scores
- `notifications` - In-app notifications
- `official_replies` - Government representative replies
- `audit_logs` - Admin action audit trail

### Phase 2 Tables
- `representatives` - Government official contacts (name, department, district, email, phone)
- `email_log` - Email dispatch audit trail
- `complaint_assignments` - Representative assignment history

### Complaint Table Fields
`id, user_id, category_id, title, description, generated_description, original_text, original_language, translated_text, status, priority, severity, risk_score, urgency, affected_population, ai_summary, ai_confidence, support_count, duplicate_count, is_merged, merged_into, latitude, longitude, location_text, district, city, area, landmark, state, pincode, citizen_name, citizen_phone, is_emergency, department, suggested_action, estimated_resolution_hours, representative_id, representative_email, created_at, updated_at`

## Docker

```bash
docker-compose up --build
```

## Environment Variables

All Supabase credentials are pre-configured. For production email sending, configure SMTP secrets:
- `SMTP_HOST`
- `SMTP_PORT`
- `SMTP_USER`
- `SMTP_PASS`

## High-Risk Visual Alert System

Complaints with `risk_score >= 85` are automatically:
- Displayed with a **red border** and **light red background**
- Badged with a bold red **"HIGH RISK"** label
- Pinned to the **top of the dashboard** in a dedicated "Critical Complaints" section
- Animated with a **subtle pulsing indicator** to draw attention
- Refreshed automatically when new complaints cross the threshold

## License

Government of India Digital Service - Demo Project
