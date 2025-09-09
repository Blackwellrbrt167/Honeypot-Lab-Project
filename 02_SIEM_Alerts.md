# SIEM Alerts

This document captures how Cowrie honeypot logs were integrated into a SIEM and how alerts were triggered, reviewed, and analyzed.

---

## Step 1: Configure Log Forwarding
**Action:** Forwarded Cowrie logs into SIEM (Wazuh or Splunk).  
**Config File(s):** [Insert path/file here]  

📸 Screenshot: [Insert screenshot of forwarding config file](../evidence/log_forwarding_config.png)

---

## Step 2: Verify Logs in SIEM
**Action:** Confirmed Cowrie logs appeared in SIEM log index.  
**Command / SIEM UI:**  
- For Splunk: Search `index=cowrie`  
- For Wazuh: Check log collector status  

📸 Screenshot: [Insert SIEM dashboard showing Cowrie logs](../evidence/siem_logs.png)

---

## Step 3: Create Detection Rule
**Action:** Built a detection rule/alert for repeated failed SSH attempts.  
**Rule Type:** Threshold alert (≥ 5 failed attempts in 1 minute).  

📸 Screenshot: [Insert SIEM alert rule configuration](../evidence/alert_rule_config.png)

---

## Step 4: Simulate Attack
**Action:** Attempted multiple SSH logins against honeypot to trigger alert.  
**Command (attacker simulation):**
```bash
for i in {1..10}; do ssh -p 2222 root@<honeypot_IP>; done
```

Screenshot: Insert terminal showing brute-force attempts

## Step 5: Alert Triggered 
**Action:** SIEM alert fired based on detection rule 
Alert Message Example:

Multiple failed SSH login attempts detected from 192.168.1.50
Event Count: 10 in 60 seconds

Screenshot: Insert SIEM alert Dashboard screenshot 

## Step 6: Document Findings 
**Action: Captured the SIEM workflow from raw logs - detection rule - alert.

Screenshot: Insert final summary dashboard or log timeline
