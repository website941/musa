# 04. Cybersecurity Risk Assessment & UK Legal Frameworks
## Manchester University NHS Foundation Trust

### Security Philosophy & Industry Standards
The security of patient confidential data is paramount under UK law. The Trust complies with the UK General Data Protection Regulation (UK GDPR), Data Protection Act 2018, the Caldicott Principles, and the NHS Data Security and Protection Toolkit (DSPT). Stringent technical and organisational controls prevent patient record exfiltration, clinical disruption, and malicious cyber intrusion.

### Compliance Standards & Frameworks
- NHS Data Security and Protection Toolkit (DSPT) — Standards Met
- The Caldicott Principles (Caldicott 3 Review)
- UK General Data Protection Regulation (UK GDPR Article 9: Special Category Data)
- Data Protection Act 2018 (Section 170 Offences)
- Cyber Essentials Plus Certification (NHS Digital Audited)
- ISO/IEC 27001 Information Security Management

### Threat Risk Matrix
---------------------------------------------------------
### Threat 1: Ransomware & Malware Attacks on Hospital Systems
- **Risk Severity Level:** CRITICAL
- **Attack Vector:** Spear-phishing emails containing malicious PDF macros, vulnerable remote desktop ports (RDP), unpatched VPN gateway software.
- **Operational & Reputational Impact:** Malicious encryption of hospital databases and clinical scheduling systems could force ambulances to be diverted, delay cancer surgeries, and put patient lives at immediate physical risk (as seen during WannaCry in 2017).
- **Technical Mitigation Strategy:** Strict network segmentation separating clinical machinery from public web servers, Endpoint Detection and Response (EDR) software on all terminals, automated immutable backups, and mandatory employee cybersecurity awareness training.
- **Applicable UK Legal Statute:** Computer Misuse Act 1990 Section 3, Health and Social Care Act 2012.

---------------------------------------------------------
### Threat 2: Targeted NHS Patient Phishing & Smishing Scams
- **Risk Severity Level:** CRITICAL
- **Attack Vector:** SMS Sender ID spoofing, rogue telephone diallers, fraudulent web domain registrations (e.g. nhs-appointment-card.co.uk).
- **Operational & Reputational Impact:** Cybercriminals send fake SMS messages imitating the NHS (e.g. "You are eligible for a free health check - pay £1.99 postage for your kit"), stealing bank cards and personal identity data from vulnerable elderly patients.
- **Technical Mitigation Strategy:** National SMS Sender ID Registry protection with mobile operators, automated domain takedown via NCSC Protective DNS, and public warning banners on official NHS portals.
- **Applicable UK Legal Statute:** Fraud Act 2006, Privacy and Electronic Communications Regulations (PECR) 2003.

---------------------------------------------------------
### Threat 3: Unsafe Sharing & Unauthorised Browsing of Patient Records
- **Risk Severity Level:** HIGH
- **Attack Vector:** Misuse of legitimate privileged database access rights, shared user logins, unlocked clinical computers in hospital corridors.
- **Operational & Reputational Impact:** Clinical or administrative staff viewing medical histories of neighbours, celebrities, or colleagues without a direct clinical care relationship, violating patient confidentiality and statutory privacy rights.
- **Technical Mitigation Strategy:** Role-Based Access Control (RBAC), smartcard tap-to-authenticate readers that lock the screen upon removal, and automated machine-learning audit algorithms that flag suspicious out-of-ward record accesses.
- **Applicable UK Legal Statute:** Data Protection Act 2018 Section 170 (Unlawful obtaining of personal data — criminal offence), Caldicott Principles.

---------------------------------------------------------
### Threat 4: Insecure Web Forms & SQL Injection (SQLi)
- **Risk Severity Level:** HIGH
- **Attack Vector:** Unsanitized user input parameters passed directly to SQL query engines in older legacy web modules.
- **Operational & Reputational Impact:** Vulnerabilities in public appointment booking forms or prescription renewal request forms could allow attackers to bypass authentication and dump entire patient tables.
- **Technical Mitigation Strategy:** Enforcement of parameterized SQL queries and Object-Relational Mappers (ORMs), Web Application Firewall (WAF) pattern inspection, and strict client and server-side data sanitization.
- **Applicable UK Legal Statute:** UK GDPR Article 32 (Security of Processing), OWASP Top 10 A03:2021 Injection.

---------------------------------------------------------
### Threat 5: Distributed Denial of Service (DDoS) on Appointment Portals
- **Risk Severity Level:** HIGH
- **Attack Vector:** Volumetric botnet UDP/HTTP traffic targeted at patient portal web servers.
- **Operational & Reputational Impact:** Flooding the patient appointment booking portal prevents patients from viewing their surgical instructions, confirming pre-op assessments, or checking A&E wait times.
- **Technical Mitigation Strategy:** Cloudflare Magic Transit DDoS scrubbing, geo-blocking non-UK traffic during crisis periods, rate limiting per IP address, and high-availability multi-region load balancers.
- **Applicable UK Legal Statute:** Computer Misuse Act 1990 Section 3.


### NCSC 5-Stage Incident Response Plan
The NHS Trust Cyber Incident Response Plan adheres to NHS England Cyber Security Operations Centre guidelines. In the event of a verified breach: 1) Clinical Gold Command is established immediately; 2) Affected network segments are severed to protect clinical devices; 3) The Department of Health and Social Care, NHS England, and the Information Commissioner’s Office (ICO) are notified within 72 hours; 4) Clinical business continuity procedures (paper-based backup charts) are activated; 5) Forensic recovery by accredited CREST incident responders.
