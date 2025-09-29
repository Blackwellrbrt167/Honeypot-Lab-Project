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

<img width="818" height="158" alt="Step 1_Wazuh Installation_Installing Dependencies_" src="https://github.com/user-attachments/assets/fb61fe52-1811-42df-8c4e-a67fcec1c42a" />

<img width="846" height="498" alt="Step 1b_wazuh installation_installing dependencies_2" src="https://github.com/user-attachments/assets/38a020ec-ebf1-4204-a6f3-712a33fbe46b" />

<img width="812" height="531" alt="Updating system in preparation for Wazuh Dashboard_Indexer_Manager_Step 1 " src="https://github.com/user-attachments/assets/8e620a2c-39f9-442b-b355-578eb9ac9ee9" />






