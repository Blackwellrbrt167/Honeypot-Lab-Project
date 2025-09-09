# Incident Response

This document captures the simulated incident response workflow after a honeypot alert was triggered in the SIEM. The goal is to walk through containment, analysis, mitigation, and lessons learned.

---

## Step 1: Alert Review
**Action:** Reviewed the triggered SIEM alert for details.  
- Source IP: [Insert IP here]  
- Attack Type: SSH brute force attempt  
- Event Count: [Insert count]  

📸 Screenshot: [Insert SIEM alert details screenshot](../evidence/alert_details.png)

---

## Step 2: Containment (Simulated)
**Action:** Simulated isolating the affected system.  
- In lab: paused/snapshotted VM, blocked IP, or disabled network adapter.  
- In real-world: would involve quarantining endpoint, blocking traffic at firewall, or isolating subnet.  

📸 Screenshot: [Insert screenshot of containment action, e.g., VM paused or firewall rule](../evidence/containment_action.png)

---

## Step 3: Log & Evidence Collection
**Action:** Gathered relevant logs from honeypot and SIEM.  
- Honeypot log path: `cowrie/var/log/cowrie/cowrie.log`  
- SIEM event log/export  

📸 Screenshot: [Insert snippet of log file showing attacker attempts](../evidence/incident_logs.png)

---

## Step 4: Attack Analysis
**Action:** Analyzed the event for root cause and attacker behavior.  
- Attack Vector: Weak credentials / brute force  
- Impact: Unauthorized access attempt detected, no real system compromise (lab-controlled)  
- Observed Attacker Actions: [Insert details, e.g., login attempts, commands entered]  

📸 Screenshot: [Insert screenshot of log analysis or SIEM timeline](../evidence/attack_analysis.png)

---

## Step 5: Mitigation Steps
**Action:** Applied changes to prevent recurrence.  
- Updated SSH configs (disable root login, enforce key-based auth)  
- Adjusted firewall rules to block repeated failed attempts  
- Added SIEM rule tuning for faster detection  

📸 Screenshot: [Insert screenshot of config or SIEM rule updates](../evidence/mitigation_steps.png)

---

## Step 6: Lessons Learned
**Action:** Reflected on incident handling process.  
- What worked well: Early detection, clear logging.  
- What could improve: Faster containment, more automated alerts.  
- Compliance tie-in: Maps to NIST CSF **Respond (RS)** and **Recover (RC)** functions.  

📸 Screenshot: [Optional screenshot of final notes/summary dashboard](../evidence/lessons_learned.png)

---

## Summary
- Reviewed SIEM alert details and attacker source.  
- Simulated containment of affected system in lab environment.  
- Collected logs and performed basic attack analysis.  
- Applied mitigation steps to strengthen defenses.  
- Documented lessons learned and mapped to NIST CSF controls.  

**Next Step:** Create GRC Mapping (`04_GRC_Mapping.md`) to align this incident with NIST CSF functions and controls.

