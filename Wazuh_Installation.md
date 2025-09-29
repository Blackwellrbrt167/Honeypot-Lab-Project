# Wazuh Installation (Lab Documentation)

This document captures the step-by-step process of installing and configuring Wazuh as part of the honeypot lab environment. The Wazuh Manager, Dashboard, and Agent setup will allow monitoring and log collection from Cowrie and other systems.

---

## Step 1: System Preparation
**Action:** Update system packages and dependencies.  

**Commands:**
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install curl apt-transport-https unzip wget -y
---

## Step 2
