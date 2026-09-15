# 05. User Experience Flow Architecture
## Manchester University NHS Foundation Trust - Scenario: Outpatient Hospital Appointment Booking & NHS Login Verification Flow

**Objective:** Illustrate the secure digital journey of an NHS patient receiving a referral, authenticating via NHS Login (OAuth 2.0 / OIDC), selecting a specialist clinic time, and synchronising with hospital Electronic Patient Records.

### End-to-End Step-by-Step Architecture
#### Step 1: Patient Receives Hospital Referral & Opens Portal
- **Actor:** User
- **User Action:** Patient clicks secure link from SMS/letter or navigates to mft.nhs.uk/appointments.
- **Technical Execution & API Responses:** Frontend loads accessible NHS design system layout, providing instant font-scaling controls and high-contrast toggle.


#### Step 2: Authentication via National NHS Login Gateway
- **Actor:** API Gateway
- **User Action:** Redirects patient to access.login.nhs.uk using OpenID Connect authorization code grant flow with PKCE.
- **Technical Execution & API Responses:** User enters email/password and passes biometric / SMS two-factor authentication (2FA). Returns signed JWT identity token.
- **Exception Handling Path:** If authentication fails, patient is offered manual phone booking via the Hospital Booking Team.

#### Step 3: Query Patient Administration System (PAS) via FHIR API
- **Actor:** Backend Service
- **User Action:** MFT backend sends authenticated FHIR query to /fhir/r4/Slot?schedule.actor=Cardiology.
- **Technical Execution & API Responses:** HSCN network proxy translates request to internal Electronic Patient Record (EPR) system and retrieves available 20-minute clinic slots.


#### Step 4: Patient Selects Clinic Slot & Submits Accessibility Needs
- **Actor:** Client Frontend
- **User Action:** Patient chooses Friday 10:30 AM at Manchester Royal Infirmary and requests British Sign Language (BSL) interpreter.
- **Technical Execution & API Responses:** Client-side form validates input, encapsulates BSL requirement tag, and submits JSON payload via HTTPS POST.


#### Step 5: Atomic Database Transaction & Slot Lock
- **Actor:** Database / External
- **User Action:** Microsoft SQL Server executes ACID transaction locking the clinic slot to prevent double-booking.
- **Technical Execution & API Responses:** Transaction updates appointment status to BOOKED, records patient NHS number hash, and logs audit record with clinical staff ID.
- **Exception Handling Path:** If slot was taken concurrently, rolls back transaction and offers next available alternative timeslot.

#### Step 6: Confirmation SMS/Email Dispatch & Calendar Sync
- **Actor:** Backend Service
- **User Action:** Dispatches secure confirmation token via NHS Notify service and generates downloadable .ics calendar file.
- **Technical Execution & API Responses:** Sends encrypted SMS with appointment reference number (e.g. MFT-CARD-82910) and parking/fasting directions.


