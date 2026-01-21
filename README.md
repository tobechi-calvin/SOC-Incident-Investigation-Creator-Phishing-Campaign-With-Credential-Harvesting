# SOC Incident Investigation – Creator Phishing Campaign With Credential Harvesting

## 📌 Overview
This repository documents a hands-on Security Operations Center (SOC) investigation of a phishing campaign targeting content creators.  
The attack leveraged a fake collaboration offer and a multi-step onboarding workflow that ultimately redirected victims to a **look-alike Google sign-in page** designed to harvest credentials.

The investigation focuses on evidence-based analysis, redirect-chain validation, credential-harvesting confirmation, MITRE ATT&CK mapping, and impact assessment using standard SOC methodologies.

---

## Incident Summary

- **Incident Type:** Phishing – Credential Harvesting (OAuth / Google Impersonation)  
- **Detection Source:** Manual review of suspicious inbound email  
- **Severity:** Medium  
- **Date Observed:** 2026-01-20  
- **Status:** No Successful Compromise Observed  

---

## Affected Assets

- **Mailbox:** inquiry[@]mydfir[.]com  
- **Environment:** Public-facing business email inbox  

---

## Threat Actor Details

- **Initial Delivery Infrastructure:** Free consumer email provider (libero[.]it)  
- **Lure Domain:** sweep-invite[.]digital  
- **Credential Harvesting Domain:** sweep-auth[.]app  
- **Threat Type:** Social engineering with credential access objective  

**Reputation / OSINT Summary:**  
The infrastructure shows characteristics consistent with phishing campaigns, including recently registered domains, brand impersonation, and separation of lure and credential-harvesting stages. No malware delivery was observed.

---

## Investigation Timeline (UTC)

| Time (UTC) | Event |
|------------|------|
| 2026-01-20 | Phishing email received offering paid creator collaboration |
| Shortly after | Analyst accessed lure link in controlled environment |
| During analysis | Multi-step creator profiling workflow observed |
| Final stage | Redirect to fake Google sign-in page (credential harvesting) |
| Post-analysis | No credentials submitted; no compromise occurred |

---

## Investigation Details

The phishing email advertised participation in an “international creator event” with compensation ranging from **$2,600–$12,000**, including “50% upfront payment.”

Upon accessing the attacker-provided link in a controlled environment, the following behavior was observed:

- A professional-looking creator onboarding workflow designed to:
  - Profile YouTube creators
  - Build trust through branding and social proof
- No exploit delivery or malware execution
- Final redirect to a **fake Google authentication page** hosted outside legitimate Google infrastructure

### Credential Harvesting Confirmation
The final redirect led to a look-alike Google OAuth login page hosted on `sweep-auth[.]app`, impersonating Google sign-in functionality and attempting to capture user credentials under the pretense of YouTube channel verification.

No legitimate Google authentication endpoints (`accounts.google.com`) were used.

---

## Tools & Techniques Used

- **Analysis Type:** Manual phishing analysis & controlled browser detonation  
- **Techniques:** Redirect-chain analysis, UI impersonation validation  
- **Artifacts Reviewed:** Email content, URLs, web workflows, authentication pages  

---

## MITRE ATT&CK Mapping

| Technique ID | Technique Name |
|--------------|----------------|
| T1566 | Phishing |
| T1078 | Valid Accounts |
| T1036 | Masquerading |

---

## Impact Assessment

- **Credential Harvesting Attempt:** Yes  
- **Credentials Submitted:** No  
- **Account Compromise:** No  
- **Persistence Observed:** No  
- **Lateral Movement:** No  

**Assessment Summary:**  
While the attack did not result in a confirmed compromise, it represents a high-risk credential-harvesting attempt capable of leading to Google / YouTube account takeover if successful. Early detection and analysis prevented impact.

---

## Indicators of Compromise

### Domains
- sweep-invite[.]digital — phishing lure / creator profiling  
- sweep-auth[.]app — fake Google login (credential harvesting)  
- libero[.]it — legitimate provider abused for delivery  

### URLs
- hxxps://sweep-invite[.]digital/connect-creator  
- hxxps://sweep-auth[.]app/?continue=hxxps://myaccount[.]google[.]com/  

### Email Addresses
- modash_partners[@]libero[.]it  
- collab[.]modash[@]libero[.]it  

---

## Recommendations

- Educate creators on verifying OAuth login domains
- Block phishing domains at email and web gateways
- Flag creator-collaboration emails for manual review
- Require domain validation before any authentication workflows
- Reinforce awareness that Google login should only occur on `accounts.google.com`

---

## Key Takeaways

- Phishing campaigns increasingly avoid malware and rely on trust abuse
- Multi-step onboarding workflows can be weaponized
- Credential harvesting often occurs after legitimacy is established
- Following the entire redirect chain is critical for accurate assessment

---

##  About This Portfolio

This repository is part of my SOC analyst portfolio, showcasing hands-on incident investigations, structured analysis, and alignment with real-world SOC workflows.
