Here is the UX specification and user journey for the Admin Experience,
specifically optimized for the "15-minute daily triage" constraint.

As a Principal Product Manager, when designing for a time-poor clinician or
coordinator, we must abandon the traditional "analytical dashboard" (which
encourages browsing) and instead design an "Inbox Zero" Action Hub. The system
must do the thinking, surfacing only the exceptions that require human
intervention.

1. The Admin UX Philosophy: "Exception-Driven Triage"

  - The "Inbox Zero" Goal: When the Admin logs in, they should not see perfectly
    progressing referrals. They should only see what is broken, stuck, or
    completed and awaiting final review.
  - Batch Over Single: If 10 referrals are stuck at the same external clinic,
    the Admin should be able to nudge them all with one click, not ten.
  - Contextual Slide-Outs: Page reloads kill momentum. All deep-dives must
    happen in a slide-out drawer so the Admin never loses their place in the
    queue.

2. The 15-Minute Daily Journey (Scenario Walkthrough)

Scenario: Sarah, a busy clinical coordinator, grabs her coffee at 8:00 AM and
logs into the portal for her daily referral management sprint.

Minute 0–2: The Landing & Assessment

  - Sarah logs in. She bypasses standard charts and is greeted by the Action Hub
    Dashboard.
  - She sees three prominent, color-coded "Triage Buckets":
      - 🔴 Critical Exceptions: 4 Referrals (Denied, OON, Patient Cancelled).
      - 🟡 Stuck/Aging: 12 Referrals (Unread by Specialist > 72 hours).
      - 🟢 Closed Loop / Review: 3 Referrals (Specialist uploaded notes, ready to
        close).

Minute 3–5: Batch Processing (The Yellow Bucket)

  - Sarah clicks the Stuck/Aging bucket. The view filters to a list of 12 aging
    referrals.
  - She selects a master checkbox at the top of the grid to highlight all 12.
  - She clicks a floating action button: "Bulk Nudge Specialists".
  - The system fires off automated OTP SMS/Email reminders to those specific
    clinics. 12 items cleared in 3 clicks.

Minute 6–10: Exception Handling (The Red Bucket)

  - Sarah clicks the Critical Exceptions bucket. She sees John Doe was "Denied"
    by Dr. Carl due to "Insurance Not Accepted."
  - She clicks John's row. A right-side Detail Drawer slides out.
  - At the very top of the drawer, a red banner screams the context: Exception:
    Dr. Carl rejected - Out of Network.
  - Sarah clicks "Reassign", selects a new in-network cardiologist from a
    dropdown, and clicks "Send."
  - The drawer closes, John Doe disappears from the triage list. 1 item
    resolved.

Minute 11–15: Closing the Loop (The Green Bucket) & Outbound

  - Sarah clicks the Closed Loop bucket. She reviews the 3 PDFs uploaded by
    external specialists yesterday.
  - She downloads the PDFs to route to the internal EHR, and clicks
    "Archive/Complete" for each.
  - Before logging out, she clicks the persistent "+ New Referral" button in the
    top nav to quickly input two new priority referrals requested by doctors
    that morning.
  - Inbox Zero achieved. She logs out at 8:15 AM to go see patients.

3. Screen-by-Screen UI/UX Specification

Screen 1: The "Action Hub" Dashboard

  - Purpose: Tell the Admin exactly what to do right now. No vanity metrics.
  - Visual Layout: Clean, widget-based top row, with a unified priority queue
    below.
  - The Triage Widgets (Top):
      - Large clickable cards displaying a number and label.
      - Card 1 (Red): "Action Required: 4" (Bounced, denied, errors)
      - Card 2 (Yellow): "Aging > 72h: 12" (Bottlenecks)
      - Card 3 (Green): "Ready to Close: 3" (Docs uploaded, patient seen)
  - The "To-Do" Feed (Bottom):
      - A chronological list of the exceptions from the widgets above.

Screen 2: The Focused Referral Queue

  - Purpose: Rapid, spreadsheet-like manipulation.
  - Default View: Filtered automatically to "Requires Admin Action."
  - Key Columns: Patient, Specialty, Assigned To, Days Aging, Status/Blocker.
  - Micro-Interactions (Hover States): When the Admin hovers over a row,
    quick-action icons appear directly in the row (e.g., a "Reassign" icon, a
    "Remind" bell icon, a "Cancel" X icon). This prevents them from having to
    open the referral to take basic actions.

Screen 3: The Detail Drawer (Slide-out from Right)

  - Purpose: Provide full context without losing the queue view.
  - UI Hierarchy:
      - The Context Banner (Top): Always highlights the current state. If stuck,
        it says "Waiting on Dr. Smith for 4 Days." If denied, it shows the exact
        reason provided by the specialist.
      - Patient Card: Mini demographic view.
      - Audit Trail: A clear, vertical timeline showing exactly what happened.
        (e.g., Monday: Sent -> Tuesday: Patient Texted -> Thursday: Specialist
        Denied).
  - Primary Action Footer: Sticky footer at the bottom of the drawer with
    context-aware buttons (e.g., if the status is Denied, the primary button is
    "Reassign Referral").

4. UX Metrics (Measuring Efficiency & Engagement)

To ensure this app is actually solving the business problem without creating a
new administrative burden, we will track these 4 specific metrics.

Metric 1: "Time to Inbox Zero" / Average Admin Session Length

  - What it measures: Admin efficiency.
  - How to track: Timestamp from Admin login to the moment all "Critical
    Exception" and "Ready to Close" queues are empty.
  - Target: Under 15 minutes per day. If this creeps up to 45+ minutes, our UI
    is too cluttered or our automated reminders aren't working.

Metric 2: Specialist Time-to-Accept (TTA)

  - What it measures: Specialist engagement and the effectiveness of the OTP
    magic-link design.
  - How to track: Time elapsed from the system sending the magic link to the
    specialist, to the moment they hit "Accept".
  - Target: >70% of referrals accepted within 48 hours. This proves our "zero
    friction" thesis is working.

Metric 3: Patient-Driven Loop Closure Rate

  - What it measures: Patient engagement and offloading Admin work.
  - How to track: Percentage of referrals where the status was moved to
    "Appointment Booked" or "Completed" by the patient via their mobile link,
    rather than by the Admin or Specialist.
  - Target: >40%. Every percentage point here represents minutes saved for the
    Admin persona.

Metric 4: Referral Salvage Rate (Leakage Prevention)

  - What it measures: System health and exception-handling success.
  - How to track: The percentage of referrals that hit a "Critical Exception"
    (e.g., Denied, Out of Network) but are successfully reassigned by the Admin
    and eventually reach "Completed".
  - Target: >80% salvage rate. This proves the "Morning Triage" is actively
    preventing patients from falling through the cracks when their first
    referral bounces.
