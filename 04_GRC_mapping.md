# GRC Mapping (NIST CSF)

This document connects each stage of the honeypot → SIEM → incident response workflow to relevant NIST Cybersecurity Framework (CSF) functions, categories, and subcategories. The goal is to demonstrate how hands-on detection and response align with compliance and governance.

---

## Step 1: Deploy Honeypot (Detection)
- **Lab Action:** Installed and configured Cowrie SSH honeypot to capture malicious login attempts.  
- **NIST CSF Mapping:**  
  - **DE.CM-7 (Security Continuous Monitoring):** The network is monitored to detect potential cybersecurity events.  
- **Why It Fits:** Honeypot provides continuous visibility into unauthorized access attempts.

📸 Screenshot: [Insert honeypot running screenshot](../evidence/honeypot_running.png)

---

## Step 2: SIEM Alert Triggered (Identification)
- **Lab Action:** Forwarded Cowrie logs into Wazuh/Splunk; created alert rule for brute-force activity.  
- **NIST CSF Mapping:**  
  - **DE.DP-4 (Detection Processes):** Event detection information is communicated to appropriate parties.  
- **Why It Fits:** SIEM alerts transform raw log data into actionable security events.

📸 Screenshot: [Insert SIEM alert screenshot](../evidence/siem_alert.png)

---

## Step 3: Containment & Isolation (Response)
- **Lab Action:** Simulated isolating the honeypot VM / blocking malicious IP.  
- **NIST CSF Mapping:**  
  - **RS.MI-1 (Mitigation):** Activities are performed to prevent expansion of an event and to resolve the incident.  
  - **RS.CO-2 (Response Communication):** Incidents are reported consistent with established response processes.  
- **Why It Fits:** Containment actions reduce impact while following defined response steps.

📸 Screenshot: [Insert containment action screenshot](../evidence/containment_action.png)

---

## Step 4: Attack Analysis (Response)
- **Lab Action:** Analyzed honeypot logs to confirm repeated brute-force attempts and attacker IP.  
- **NIST CSF Mapping:**  
  - **RS.AN-1 (Analysis):** Notifications from detection systems are investigated.  
- **Why It Fits:** Reviewing logs and alert data aligns with incident analysis requirements.

📸 Screenshot: [Insert attack analysis screenshot](../evidence/attack_analysis.png)

---

## Step 5: Mitigation & Recovery
- **Lab Action:** Applied simulated hardening steps (disable root login, enforce key-based auth, firewall rules).  
- **NIST CSF Mapping:**  
  - **RC.IM-1 (Improvements):** Recovery planning and processes are improved by incorporating lessons learned.  
- **Why It Fits:** Documenting improvements ensures the organization adapts and strengthens resilience after incidents.

📸 Screenshot: [Insert mitigation/config screenshot](../evidence/mitigation_steps.png)

---

## Summary
- **Detect:** Honeypot provided visibility into unauthorized SSH access attempts.  
- **Respond:** SIEM alerts, containment, and analysis simulated incident response.  
- **Recover:** Mitigation steps and lessons learned showed organizational resilience.  

This lab demonstrates how **technical Blue Team activities** (honeypot + SIEM + incident handling) can be mapped to **governance frameworks** (NIST CSF), providing both security value and compliance alignment.


