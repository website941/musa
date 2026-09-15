# 03. Web Architecture Specification (UK Level 3 Computing)
## Manchester University NHS Foundation Trust

### Architectural Model
The NHS Trust web architecture must adhere to the highest UK public health data governance standards. Built with the open-source NHS digital design system, the web application integrates seamlessly with the national NHS Spine, electronic patient records (EPR), and regional Health and Social Care Networks (HSCN) while rigorously isolating confidential patient data from public-facing content.

### Data Pipeline Flow
Public Internet Client -> WAF & Cloudflare CDN -> NHS Digital Design System (React SSR) -> API Gateway with NHS Login (OIDC OAuth2) -> FHIR / HL7 Middleware -> Secure Internal HSCN Network -> Epic Electronic Patient Record (EPR) & SQL Server Database clusters.

### Detailed Component Analysis (Grading Criteria)
---------------------------------------------------------
### 1. HTML5 Semantic Markup & NHS Digital Design System
- **Technology Stack:** Semantic HTML5, NHS Frontend Components, WAI-ARIA 1.2, WCAG 2.2 AAA
- **Technical Role & Function:** In healthcare, accessibility is a matter of patient safety. The NHS Trust website uses NHS Frontend markup ensuring clear landmarks (<main>, <nav>, <header>), high-contrast callout boxes, and descriptive button labels (e.g., "Confirm and book cardiology appointment" rather than vague "Click here"). This guarantees patients with motor impairments, visual loss, or dyslexia can navigate vital medical resources.
- **BTEC Level 3 Assessment Focus:** Level 3 Assessment Note: NHS websites must meet WCAG 2.2 AA at minimum, with key patient journeys targeting AAA standards under the Equality Act 2010.

```
<div class="nhsuk-warning-callout" role="alert">
  <h3 class="nhsuk-warning-callout__label"><span role="text"><span class="nhsuk-u-visually-hidden">Important: </span>Fasting Instructions</span></h3>
  <p>Do not eat or drink anything except water for 6 hours prior to your surgical procedure.</p>
</div>
```

---------------------------------------------------------
### 2. Cascading Style Sheets (CSS3 & NHS Design Tokens)
- **Technology Stack:** CSS3, NHS Design System SASS, Focus Indicators, Print Stylesheets
- **Technical Role & Function:** CSS enforces the internationally recognised NHS Blue (#005EB8) colour palette, which instils immediate patient trust. Crucially, yellow-and-black 4px high-visibility focus rings are applied to every interactive link and form field for keyboard navigation. Bespoke print media stylesheets format appointment confirmations onto standard A4 paper without headers or banners.
- **BTEC Level 3 Assessment Focus:** Level 3 Assessment Note: High-contrast focus outlines allow patients unable to use a computer mouse to navigate through appointment forms using only keyboard TAB and ENTER keys.

```
a:focus, button:focus {
  outline: 4px solid #ffeb3b;
  outline-offset: 0;
  background-color: #212b32;
  color: #ffffff;
}
```

---------------------------------------------------------
### 3. JavaScript & Client-Side Accessibility Controls
- **Technology Stack:** TypeScript, React 19, Vanilla JS fallbacks, Font-Resizer Engine, High Contrast Toggle
- **Technical Role & Function:** JavaScript provides dynamic features including hospital clinic search filters, department search autocompletion, and an accessible font-size scaling toolbar. In strict adherence to progressive enhancement, if JavaScript fails to execute, standard HTML forms still submit cleanly to server endpoints via HTTP POST.
- **BTEC Level 3 Assessment Focus:** Level 3 Assessment Note: Client-side validation checks NHS numbers using the Modulus 11 mathematical checksum algorithm before transmitting requests over the network.

```
// Validating 10-digit NHS Number using Modulus 11 algorithm
function validateNHSNumber(nhsNo: string): boolean {
  if (!/^\d{10}$/.test(nhsNo)) return false;
  const weights = [10, 9, 8, 7, 6, 5, 4, 3, 2];
  const sum = nhsNo.slice(0, 9).split("").reduce((acc, digit, idx) => acc + Number(digit) * weights[idx], 0);
  const remainder = sum % 11;
  const checkDigit = remainder === 0 ? 0 : 11 - remainder;
  return checkDigit !== 10 && checkDigit === Number(nhsNo[9]);
}
```

---------------------------------------------------------
### 4. Application Programming Interfaces (APIs & HL7/FHIR)
- **Technology Stack:** Fast Healthcare Interoperability Resources (FHIR) JSON APIs, RESTful Endpoints, NHS Spine MESH
- **Technical Role & Function:** Healthcare systems rely on international FHIR standards to safely transmit appointment dates, doctor notes, and prescription tokens. FHIR represents clinical concepts (Patient, Observation, Encounter, MedicationRequest) in standardized JSON structures, preventing misinterpretation between GP surgery software and acute hospital databases.
- **BTEC Level 3 Assessment Focus:** Level 3 Assessment Note: FHIR REST APIs use OAuth2 Bearer tokens with strict role-based scopes (e.g., patient/*.read), preventing unauthorized staff from viewing medical records outside their clinical ward.

```
GET /fhir/r4/Appointment?patient=9434765919
Authorization: Bearer nhs-token-f89a742
Accept: application/fhir+json
```

---------------------------------------------------------
### 5. Content Management System (CMS)
- **Technology Stack:** Wagtail / Umbraco Headless CMS, NHS England Syndication API
- **Technical Role & Function:** Hospital clinic details, consultant bios, ward telephone numbers, and public health guidelines are maintained in an enterprise headless CMS. Clinical content authors must undergo strict clinical governance approval before any health guidance page is published to the live public server.
- **BTEC Level 3 Assessment Focus:** Level 3 Assessment Note: Four-eyes principle: Clinical information must be drafted by a medical communications officer and approved by a Consultant Physician before publication.

```
CMS Publication Gate: Draft Created -> Medical Peer Review -> Clinical Governance Lead Sign-off -> Automated Staging Build -> Live Site Deployment.
```

---------------------------------------------------------
### 6. Database Architecture & Secure Data Storage
- **Technology Stack:** Microsoft SQL Server Enterprise, Azure Cosmos DB, Encrypted TDE, Audit Logging
- **Technical Role & Function:** Patient appointment bookings and hospital department directories are stored in highly secure, fault-tolerant Microsoft SQL Server clusters hosted in UK-sovereign data centres. Transparent Data Encryption (TDE) protects data at rest using AES-256 bit keys. Immutable audit tables record every single database SELECT query with user ID, timestamp, and patient identifier.
- **BTEC Level 3 Assessment Focus:** Level 3 Assessment Note: The Data Protection Act 2018 legally requires comprehensive audit trails so that any unauthorised browsing of celebrity or family patient records can be prosecuted.

```
SELECT appointment_id, clinic_code, slot_time FROM outpatient_bookings WHERE nhs_number_hash = @hash AND status = 'CONFIRMED';
```

---------------------------------------------------------
### 7. Cloud & Hybrid Hosting Infrastructure
- **Technology Stack:** Microsoft Azure UK South (London) & UK West (Cardiff), Health and Social Care Network (HSCN)
- **Technical Role & Function:** The public-facing website is hosted on Microsoft Azure UK sovereign cloud regions, which meet the NHS Cloud Security Principles. The infrastructure connects via dedicated encrypted leased lines to the Health and Social Care Network (HSCN), ensuring clinical backend traffic never traverses the public internet without IPsec encapsulation.
- **BTEC Level 3 Assessment Focus:** Level 3 Assessment Note: Dual-zone UK hosting ensures data sovereignty—patient personal identifiable information (PII) never leaves United Kingdom legal jurisdiction.

```
Azure Virtual Network Peering with Network Security Groups (NSGs) restricting ingress traffic exclusively to port 443 via Azure Application Gateway WAF.
```

---------------------------------------------------------
### 8. Content Delivery Network (CDN) & Edge Security
- **Technology Stack:** Cloudflare UK Public Sector Edge, Fastly CDN, Anycast DNS
- **Technical Role & Function:** Static medical guides, hospital parking maps, and clinical guidelines are cached across UK edge nodes. When health campaigns (such as winter flu vaccinations or pandemic advisories) drive millions of simultaneous visitors, the edge CDN absorbs the surge, protecting hospital clinical databases from crashing.
- **BTEC Level 3 Assessment Focus:** Level 3 Assessment Note: CDN caching is strictly disabled for any authenticated patient portal pages via Cache-Control: private, no-store, no-cache headers.

```
Cache-Control: no-store, no-cache, must-revalidate, proxy-revalidate
Pragma: no-cache
Expires: 0
```

---------------------------------------------------------
### 9. HTTPS, TLS 1.3 & Encrypted Web Forms
- **Technology Stack:** TLS 1.3 with ECDHE key exchange, AES-GCM 256-bit encryption, DNSSEC
- **Technical Role & Function:** All web traffic is encrypted using TLS 1.3. Patient contact forms, appointment requests, and prescription queries are encrypted in transit. Form fields sanitize inputs against SQL injection and cross-site scripting before encrypting payloads with public key cryptography for database storage.
- **BTEC Level 3 Assessment Focus:** Level 3 Assessment Note: Prevents packet sniffing on public hospital Wi-Fi networks where patients and visitors frequently access the portal from bedside devices.

```
Content-Security-Policy: default-src 'self'; form-action 'self' https://portal.mft.nhs.uk;
X-Content-Type-Options: nosniff;
```

---------------------------------------------------------
### 10. Authentication & NHS Login Integration
- **Technology Stack:** NHS Login (OIDC / OAuth 2.0), FIDO2 Biometrics, Two-Factor Authentication (2FA)
- **Technical Role & Function:** Patients authenticate using the national NHS Login service. NHS Login validates patient identity to Level 3 (high) proofing using passport/driving licence photo matching. Once verified, cryptographic OIDC tokens grant access to view hospital outpatient appointments and clinical letters.
- **BTEC Level 3 Assessment Focus:** Level 3 Assessment Note: Two-factor authentication (SMS OTP or authenticator app) is mandatory for patients accessing sensitive clinical letters, adhering to Caldicott Principle 7.

```
GET /authorize?client_id=mft-portal&response_type=code&scope=openid+profile+nhs_number&redirect_uri=https://mft.nhs.uk/auth/callback
```

---------------------------------------------------------
### 11. Real-Time Health System Monitoring & SIEM
- **Technology Stack:** Microsoft Sentinel SIEM, Azure Monitor, Splunk, NHS Cyber Associates Network Alerts
- **Technical Role & Function:** The Trust’s Cyber Security Operations Centre operates 24/7 Security Information and Event Management (SIEM). Automated correlation rules detect anomalous patient data access, repeated failed authentication attempts, and unrecognised API calls across all hospital networks.
- **BTEC Level 3 Assessment Focus:** Level 3 Assessment Note: Threshold alerts trigger automated account lockout if more than 5 failed login attempts occur within 10 minutes.

```
Sentinel KQL Query: SecurityEvent | where EventID == 4625 | summarize FailedLogins=count() by TargetAccount, bin(TimeGenerated, 10m) | where FailedLogins > 5
```

---------------------------------------------------------
### 12. Disaster Recovery, Automated Backups & Ransomware Resilience
- **Technology Stack:** Immutable Cloud Backups, Azure Site Recovery, Air-Gapped Off-Site Vaulting
- **Technical Role & Function:** Learning critical lessons from the 2017 global WannaCry ransomware incident, all database backups are immutably locked and mirrored to air-gapped secondary storage vaults. Automated failover tests run quarterly to verify that outpatient clinics can operate uninterrupted even if primary hospital data centres lose power.
- **BTEC Level 3 Assessment Focus:** Level 3 Assessment Note: RTO (Recovery Time Objective) is under 15 minutes for clinical triage; RPO (Recovery Point Objective) is under 60 seconds of transaction logs.

```
Automated geo-redundant backup executed every 15 minutes with cryptographic checksum verification and SHA-256 hash validation.
```

