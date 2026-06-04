Here is the detailed, demo-ready UI/UX specification and user journey for the **Specialist Experience**. This is structured specifically for your UX/UI and frontend teams to build wireframes and prototypes for tomorrow’s presentation.

---

# 1. The Specialist UX Philosophy 
**"Zero-Friction Collaboration"**

External specialists are busy and suffer from "portal fatigue." They will not create, remember, or reset passwords for our platform. The entire experience must be powered by **context-aware secure magic links** and **OTP (One-Time Password)** authentication. 

When a specialist clicks a link about *Patient A*, they should land directly on *Patient A's* record after authenticating, while retaining the ability to step back and view their entire queue.

---

# 2. Detailed Specialist User Journey

**Scenario:** Dr. Carl (External Cardiologist) receives a referral for a patient, John Doe.

### Step 1: The Notification
*   Dr. Carl’s practice manager receives an email and SMS: *"Urgent: New Cardiology Referral from [Your Health System] for John D. Securely view and accept this referral: [Magic Link]"*
*   **UX Note:** The link is unique, encrypted, and expires in 7 days.

### Step 2: Frictionless Authentication
*   The practice manager clicks the link and is taken to the secure portal on their desktop or mobile browser.
*   The screen greets them: *"Welcome, Dr. Carl's Office. Please verify your identity."*
*   They select whether they want the 6-digit OTP sent to their registered Email or Phone.
*   They receive the code, type it in, and the system authenticates them.

### Step 3: Contextual Landing (Deep Linking)
*   Because they clicked a link specifically for John Doe, the system bypasses the generic dashboard and drops them **directly into John Doe's Referral Detail View**.
*   This immediate context prevents them from having to search for the patient they were just notified about.

### Step 4: Triage & Action
*   The practice manager reviews John's demographics, insurance, and the referring provider's notes.
*   They click a prominent **"Accept Referral"** button.
*   A modal pops up asking to confirm, and allows them to optionally log an appointment date/time right there.

### Step 5: Global View Navigation
*   After handling John Doe, the practice manager clicks a subtle "View All Active Referrals" button in the breadcrumb navigation.
*   They are taken to a workspace showing 3 other pending referrals they need to process.

### Step 6: Closing the Loop (The New Feature)
*   Two weeks later, John Doe is seen by Dr. Carl.
*   The practice manager logs back into the portal (via a saved bookmark or previous link, using OTP again).
*   They open John Doe's referral, click **"Upload Documents & Close Loop,"** and drag-and-drop Dr. Carl's PDF consultation notes and EKG lab results.
*   The referral is marked "Completed," instantly alerting the internal primary care provider.

---

# 3. Screen-by-Screen UI/UX Specifications

For tomorrow's demo, the design team should mock up the following screens:

## Screen 1: The OTP Request Screen
*   **Purpose:** Initiate the secure login process.
*   **Visual Layout:** Clean, minimalist, white background, centralized card. System logo at the top.
*   **Key Text:** *"Secure Referral Access for [Specialist Practice Name]"*
*   **Available Actions:** 
    *   Radio buttons to choose: "Send code to (***) ***-1234" OR "Send code to doc****@clinic.com".
*   **Primary Button:** *"Send Verification Code"*
*   **UX Detail:** Obfuscate the phone number and email for security, showing only the last few characters.

## Screen 2: The OTP Verification Screen
*   **Purpose:** Input the code.
*   **Visual Layout:** Centralized card. 
*   **Key UI Elements:** 
    *   Six large, distinct input boxes for the 6-digit code.
    *   Auto-advance logic (when the user types a number, focus automatically jumps to the next box).
*   **Primary Button:** *"Verify & Login"* (Disabled until all 6 digits are entered).
*   **Secondary Action:** *"Didn't receive a code? Resend in 0:59"* (Countdown timer to prevent spamming).

## Screen 3: Context-Aware Referral Detail (The Deep Link Target)
*   **Purpose:** Allow the specialist to evaluate a specific patient immediately.
*   **Visual Layout:** 
    *   Top: A "Back to All Referrals" breadcrumb.
    *   Left Column (60% width): Patient Demographics (Name, MRN, DOB, Phone, Insurance) and the "Reason for Referral" (Primary Care Notes).
    *   Right Column (40% width): Status Tracker (Visual timeline) and Action Panel.
*   **Action Panel Buttons:**
    *   **Primary CTA (Green):** *"Accept Referral"*
    *   **Secondary CTA (Red/Outline):** *"Decline..."* (Opens a modal to select a reason: Not in Network, No Capacity, etc.)
    *   **Tertiary CTA (Blue/Outline):** *"Schedule Appointment"*
*   **The "Upload Documents" Section (New Feature - See detailed breakdown below).**

## Screen 4: Specialist Workspace ("All Referrals")
*   **Purpose:** A master queue for the specialist’s administrative staff.
*   **Visual Layout:** A data table/grid.
*   **Key Columns:** 
    *   Patient Name
    *   Date Received
    *   Referring Doctor
    *   Status Badges (e.g., `New`, `Accepted`, `Scheduled`, `Completed`).
*   **UX Detail:** Unread/New referrals should be bolded with a subtle "New" indicator dot to draw attention.
*   **Filters:** Quick-filter tabs at the top: `Action Needed (3)`, `Scheduled (12)`, `Completed (45)`.

---

# 4. Deep Dive: Document Upload Experience (New Feature)

To ensure internal doctors get the diagnostic data they need, the upload experience must feel modern and foolproof.

### UI Element: The Upload Card (Located on the Referral Detail Screen)
*   **State 1: Empty State**
    *   A dashed-border dropzone area.
    *   **Text:** *"Drag and drop consultation notes, labs, or imaging reports here, or click to browse."*
    *   **Supported File Types text:** *"Supports PDF, JPG, PNG (Max 25MB)"*

*   **State 2: Active Upload / Categorization Modal**
    *   When a user drops a file (e.g., `Carl_Notes_Doe.pdf`), a modal appears.
    *   The system asks the specialist to categorize the document (Dropdown): 
        *   *Consultation Note*
        *   *Lab Results*
        *   *Imaging/Radiology*
        *   *Other*
    *   **Primary Button:** *"Upload & Attach to Patient Record"*

*   **State 3: Success & Loop Closure**
    *   A green progress bar fills.
    *   The document appears as a polished tile with a PDF icon, file name, timestamp, and the category badge.
    *   A Toast Notification appears at the bottom: *"Document shared securely with referring provider."*
    *   **Smart Prompt:** If the referral status is currently "Scheduled" or "Seen", uploading a document triggers a smart prompt: *"Would you like to mark this referral as 'Completed'?"* -> `Yes, Close Referral` | `Not Yet`.

---

# 5. UX Edge Cases to Prep for the Demo

If stakeholders ask "What happens if...", your UX team should have these answers ready:

*   **What if the magic link expires?**
    *   **UX:** The user lands on a screen saying *"This secure link has expired for your protection."* with a button: *"Email me a new secure link."*
*   **What if the specialist tries to upload a massive file (e.g., 100MB MRI video)?**
    *   **UX:** The drag-and-drop zone turns red. Error message: *"File exceeds 25MB limit. Please upload a PDF summary instead."*
*   **What if the specialist logs in but has no active referrals?**
    *   **UX:** A friendly empty state on the Workspace screen. An illustration of a clean desk. Text: *"You're all caught up! There are no pending referrals from [Health System Name] at this time."*

