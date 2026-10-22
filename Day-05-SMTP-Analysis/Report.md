# Day 05 - SMTP Analysis: Cleartext Credentials & User Enumeration

**Analyst:** Qasim516
**Date:** 22 Oct 2026
**File:** smtp.pcap
**Tools:** Wireshark, Base64 Decoder

## 1. Summary
Analyzed SMTP traffic on Port 25. Found two critical security issues: credentials sent in cleartext (Base64) and user enumeration attempt.

## 2. Findings

### Finding 1: Cleartext Credentials [CRITICAL]
- **Evidence:** `AUTH LOGIN` with `U2VjcmV0MTIzIQ==`
- **Decoded:** Password is `Secret123!` | User is `qasim@example.com`
- **Risk:** Anyone on network can steal password using Wireshark. Account takeover possible.
- **MITRE:** T1078

### Finding 2: Email Enumeration [MEDIUM]
- **Evidence:** 
    - `RCPT TO: friend@example.org` -> `250 OK` (Valid User)
    - `RCPT TO: nobody@invalid.test` -> `550 User Unknown` (Invalid User)
- **Conclusion:** The `nobody@invalid.test` attempt is from attacker side. He is trying to find which emails are real.
- **Risk:** Valid emails found will be used for future phishing.
- **MITRE:** T1087

## 3. What is Alert and How it Works?
Alert is an automatic rule in SIEM (Splunk/Wazuh). We write a rule once, then SIEM automatically checks all traffic. Example: "If you see AUTH LOGIN on port 25, create RED alert". No manual Wireshark needed after that.

## 4. Port 25 vs 587/465
- **Port 25:** No encryption, password visible (What we saw in pcap)
- **Port 587 (STARTTLS) & 465 (SSL/TLS):** Encrypted, Wireshark shows only `TLS Encrypted Data`, password not visible.
- **Fix:** In Outlook/Gmail App settings, change SMTP Port from 25 to 587 with STARTTLS. Gmail website already uses secure ports.

## 5. SIEM Detection Rules
**Rule 1:** `dest_port=25 AND smtp.auth = true -> Alert "Cleartext SMTP Creds from SRC_IP"`
**Rule 2:** `count(550 User Unknown) > 5 from same IP in 5 min -> Alert "Possible Email Enumeration"`

## 6. Remediation
1. Disable AUTH on Port 25
2. Force Port 587/465 with TLS
3. Reset password for qasim@example.com
4. Block IP doing enumeration

## Evidence
- Add screenshot of Wireshark showing AUTH LOGIN
- Add screenshot of Base64 decoded password
