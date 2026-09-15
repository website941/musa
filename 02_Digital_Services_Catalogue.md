# 02. Digital Services Catalogue & Technical Delivery
## Manchester University NHS Foundation Trust

### 1. Patient Portal & Outpatient Appointment Booking
- **Category:** Patient Administration
- **Target Audience:** Referred NHS patients and authorised family carers.
- **Description:** View upcoming hospital appointments, reschedule clinic dates, access appointment letter PDFs, and receive SMS reminder notifications.
- **Technical Delivery Pipeline:** Secure REST API integration connecting the front-end patient portal to the Trust’s central Patient Administration System (PAS) via NHS login.

### 2. Electronic Prescription Service (EPS) & Pharmacy Renewal
- **Category:** Clinical Medication
- **Target Audience:** Outpatients on ongoing clinical care regimens.
- **Description:** Track hospital-dispensed medications, submit repeat prescription requests, and route approved electronic tokens directly to local community pharmacies.
- **Technical Delivery Pipeline:** Compliant with NHS England Spine Electronic Prescription Service API with end-to-end cryptographic digital signatures.

### 3. Emergency Department (A&E) Live Wait-Time Tracker
- **Category:** Urgent Care
- **Target Audience:** Public seeking urgent medical care and ambulance routing services.
- **Description:** Real-time estimated triage and wait-time indicators for adult and paediatric emergency departments across Manchester hospital sites.
- **Technical Delivery Pipeline:** Aggregated queue metrics pushed via Server-Sent Events (SSE) every 5 minutes from Symphony clinical triage systems.

### 4. Verified Clinical Health Information & Advice
- **Category:** Public Health Guidance
- **Target Audience:** Patients preparing for surgery and the general public.
- **Description:** Evidence-based medical guides covering surgical procedures, disease management, fasting instructions, and post-operative recovery.
- **Technical Delivery Pipeline:** Content syndication consuming the national NHS.UK Content API, styled using the official NHS digital design system.

### 5. Hospital Ward Visitor Information & Chaplaincy Support
- **Category:** Family & Visitor Services
- **Target Audience:** Relatives, visitors, and patient transport drivers.
- **Description:** Visiting hour timetables, infection prevention protocols, hospital car parking maps, disabled access guides, and bereavement support.
- **Technical Delivery Pipeline:** Mobile-responsive, geolocation-aware interactive map interfaces using Leaflet and accessible SVG campus blueprints.

### 6. Clinical Trials & Medical Research Registration
- **Category:** Research & Innovation
- **Target Audience:** Patients and healthy volunteers interested in advancing clinical science.
- **Description:** Search open clinical research studies, check patient eligibility criteria, and register voluntary interest in academic medical trials.
- **Technical Delivery Pipeline:** Secure encrypted web forms routing anonymised screening questionnaires to the Manchester Clinical Research Facility.

