# Product Summary: Referral Management Platform (refs app)

## Key Users & Endpoints

| Persona | Endpoint | Primary Need |
|--------|----------|--------------|
| Internal Staff / Referral Coordinator | `/admin` | Track, reassign, report, and prevent bottlenecks across 10+ facilities |
| External Specialist (e.g., Dr. Carl) | `/specialist` | Quickly triage referrals, accept/decline, upload consult notes, without yet another login |
| Patient | `/patient` | Know next steps, see specialist details, confirm appointments, and close the loop |

## Core Referral Lifecycle (Happy Path)

**Referral Created** → **Sent to Specialist** → **Viewed** → **Accepted** → **Appointment Scheduled** → **Patient Seen** → **Consultation Completed / Notes Shared** → **Closed**

### Exceptions Handled in UX
- Denied, Insurance not accepted, Unable to contact patient, Out of network, Referral expired, Reassigned by admin

## Key UX Decisions Made So Far

### For Specialists (Zero-Friction Philosophy)
- **No passwords** – OTP + magic link only
- Deep linking: click on a patient notification → authenticate → land directly on that patient’s referral detail
- Action panel: Accept, Decline (with reason), Schedule Appointment, Upload Documents

### For Patients (Magic-Link Experience)
- **Option C selected** (over one-way SMS or full account creation)
- Patient receives SMS → taps link → verifies with DOB → sees read-only tracking page
- **Patient-driven loop**: they confirm if they booked, when, and optionally cancel with a reason (insurance, distance, wait time)
- Post-visit: they can upload documents (photo of paper summary) for their primary doctor

### For Internal Admins (Control & Exceptions)
- Dashboard widgets: aging referrals, bottlenecks, top specialists by volume
- Core workspace: table queue with filters and bulk actions (e.g., “Send reminder to specialists”)
- Monthly reporting: leakage reasons, provider performance metrics, specialty demand

## Screens & Navigation Summary

| Role | Key Screens | Navigation Style |
|------|-------------|------------------|
| Admin | Dashboard, Referral Queue, Detail Drawer, Providers, Patients, Reports | Sidebar (Dashboard, Referrals, Providers, Patients, Reports, Settings) |
| Specialist | OTP Login, Referral Detail (deep link), Workspace (all referrals), Completed | Top nav (My Referrals, Completed, Clinic Profile) |
| Patient | Magic Link Auth, Referral Hub (with progress bar), Update Modals, Upload Screen | No menu – single-page, scroll-only |

## Notifications Strategy

- **Admin**: Daily digest email + in-app bell for exceptions
- **Specialist**: Email + SMS for new referrals, overdue reminders, admin messages
- **Patient**: SMS at referral creation, acceptance, and appointment scheduled; gentle reminders if pending >3 days

## New Feature Deep Dive (Document Upload for Specialists)

Designed as a **drag-and-drop or browse experience**:
1. Empty state with dashed dropzone
2. After file drop → modal to categorize (Consultation Note, Lab Results, Imaging, Other)
3. Success → document tile with badge, timestamp
4. Smart prompt: if status is “Scheduled” or “Seen”, ask *“Mark this referral as Completed?”*

## Phase Plan

### MVP (Immediate spreadsheet replacement)
- Manual referral creation, basic queue, status filters
- Specialist OTP + accept/reject/complete
- Patient one-way SMS (Option A – not yet magic link)
- Core statuses only

### Phase 2 (Post-stabilization)
- Full patient magic-link portal with visual timeline
- EHR integration (HL7/FHIR)
- AI-driven specialist matching (zip code, insurance, response time)
- Patient self-scheduling
- Secure bi-directional messaging between admin and specialist

## Key Differentiators vs. Traditional Portals

| Traditional EHR Portal | This Platform |
|------------------------|----------------|
| Password fatigue | Magic link + OTP |
| Patient must create account | DOB verification only |
| Specialist sees no patient context | Deep link to exact referral |
| No patient-driven updates | Patient confirms booking/cancellation |
| No document upload from patient | Photo upload of post-visit summary |
| No specialist performance analytics | Provider performance matrix in admin |

## Security & Compliance (HIPAA)

- PHI encrypted at rest and in transit
- Magic links contain **no PHI** – only a generic hash
- Secondary verification (DOB for patients, OTP for specialists) before data display
- Full audit logging (timestamp, user ID, IP, action) visible to admins
- RBAC: specialist sees *only* patients referred to their clinic
