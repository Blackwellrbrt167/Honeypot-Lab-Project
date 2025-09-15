This document will captures the step-by-step process of setting up the honeypot environment, including VM creation, installation, configuration, and verifiction 

# Honeypot Setup (Cowrie Example)

This document captures the step-by-step process of setting up the honeypot environment, including VM creation, installation, configuration, and verification.

---

## Step 1: Virtual Machine Creation
**Action:** Created a new Ubuntu Server 22.04 VM in VirtualBox/VMware  
**Specs:** 2 CPU, 4 GB RAM, 20 GB disk  
**Network Mode:** Bridged or NAT with Port Forwarding  

<img width="1075" height="875" alt="HoneyPot_VM_Setup" src="https://github.com/user-attachments/assets/e1efdeb5-8fde-4799-8356-c43d88f621b6" />

<img width="630" height="407" alt="HoneyPot_VM_Network Check_Port Forwarding Rules " src="https://github.com/user-attachments/assets/367308b0-ea04-419d-81f8-9fc98b61a306" />


---

## Step 2: Update & Install Dependencies
**Action:** Updated system and installed required packages  

**Commands:**
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install git python3-venv python3-pip -y

```
<img width="1148" height="767" alt="HoneyPot_VM_Packaage Install_Part 1 " src="https://github.com/user-attachments/assets/3ba6a630-8fd0-4d8b-88ec-c8daadcc2fe5" />

<img width="823" height="590" alt="Cowrie_Dependencies" src="https://github.com/user-attachments/assets/af8bafd6-bce7-48e4-b26d-722297226dfd" />


## Step 3: Clone & Install Cowrie
**Action:** Cloned Cowrie repository and set up virtual environment  

**Commands:**
```bash
git clone https://github.com/cowrie/cowrie
cd cowrie
python3 -m venv cowrie-env
source cowrie-env/bin/activate
pip install --upgrade pip
pip install -r requirements.txt
```

<img width="822" height="576" alt="Cowrie Clone Installtion_Confrimation_1" src="https://github.com/user-attachments/assets/43d37963-413f-4127-a6d5-69f922f709ae" />

<img width="895" height="242" alt="Cowrie DIrectory Access" src="https://github.com/user-attachments/assets/6b3e79f6-1340-4911-805a-445c88c57222" />

<img width="817" height="466" alt="Cowrie_Activation of Virtual environment" src="https://github.com/user-attachments/assets/578824a9-f111-4ff4-8231-eb35c69d401d" />


## Step 4: Configure Cowrie
**action:** Adjusted configuration file (cowrie.cfg) to set listening port (eg., 2222 for SSH)
File Path: cowrie/etc/cowrie.cfg


## Step 5: Start Cowrie Service
**Action:** Launched honeypot  

**Command:**
```bash
bin/cowrie start
```

Screenshot: Insert terminal output showing Cowrie started


## Step 6: Test Honeypot Locally
**Action:** Attempted SSH connection from host to honeypot  

**Command (from host machine):**
```bash
ssh -p 2222 root@<honeypot_IP>
```

**Expected Result:** Connection accepted, login attempts logged shell simulated

Screenshot: Insert terminal showing SSH attempt to honeypot


## Step 7: Verify Logs
**Action:** Checked honeypot logs for captured attempt
Log Path: cowrie/var/log/cowrie/cowrie.log

Screenshot: Insert log snippet of captured attempt 

## Summary
- VM created and Ubuntu installed  
- Cowrie cloned, configured, and started successfully  
- Verified login attempts are captured in logs  
- Evidence stored in `/evidence` folder  

Next step: Forward logs to SIEM for alert generation.

