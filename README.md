# Honeypot → SIEM → GRC Lab Project

This repository documents my step-by-step journey building a Blue Team lab environment. The goal is to simulate how a Security Analyst detects, investigates, and responds to malicious activity, then tie those actions back to Governance, Risk, and Compliance (GRC) frameworks like the NIST Cybersecurity Framework (CSF).

---

## Project Objectives
- Deploy a honeypot to capture malicious activity.  
- Forward honeypot logs into a SIEM for detection.  
- Trigger and investigate alerts in a simulated SOC workflow.  
- Document incident response actions (containment, analysis, mitigation).  
- Map each step to NIST CSF functions and categories.  
- Maintain daily reflections to track learning and progress.  

---

## Project Flow
1. **Honeypot Setup** – Deploy and configure Cowrie SSH honeypot.  
2. **SIEM Alerts** – Forward logs, build detection rule, simulate brute-force attempt.  
3. **Incident Response** – Contain, analyze, mitigate, and document.  
4. **GRC Mapping** – Align lab activities with NIST CSF (Detect, Respond, Recover).  

---

## Documentation
Each phase of the lab is documented in detail with screenshots and evidence:

- [01_Honeypot_Setup.md](01_Honeypot_Setup.md)  
- [02_SIEM_Alerts.md](02_SIEM_Alerts.md)  
- [03_Incident_Response.md](03_Incident_Response.md)  
- [04_GRC_Mapping.md](04_GRC_Mapping.md)  

All raw screenshots and log snippets are stored in the [/evidence](evidence) folder.

---

## Lab Journal
In addition to the technical documentation, I am maintaining a **Lab Journal** where I record daily reflections, challenges, lessons learned, and next steps.  

This journal is being updated as I work through the lab — it is not pre-filled. It captures my authentic learning process.  

 [View the Lab Journal](journal.md)

---

## Status
- **Day 1:** Repository created, skeleton documentation prepared, and project flow defined.  
- **Next Step:** Build Ubuntu VM and install Cowrie dependencies.  

---

## Notes
This project is for educational purposes only and is being conducted in a controlled lab environment.
