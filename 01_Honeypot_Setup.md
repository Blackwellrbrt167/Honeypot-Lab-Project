This document will captures the step-by-step process of setting up the honeypot environment, including VM creation, installation, configuration, and verifiction 

# Honeypot Setup (Cowrie Example)

This document captures the step-by-step process of setting up the honeypot environment, including VM creation, installation, configuration, and verification.

---

## Step 1: Virtual Machine Creation
**Action:** Created a new Ubuntu Server 22.04 VM in VirtualBox/VMware  
**Specs:** 2 CPU, 4 GB RAM, 20 GB disk  
**Network Mode:** Bridged or NAT with Port Forwarding  

📸 Screenshot: [Insert VM Settings screenshot](../evidence/vm_setup.png)

---

## Step 2: Update & Install Dependencies
**Action:** Updated system and installed required packages  

**Commands:**
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install git python3-venv python3-pip -y

```

Screenshot: [Insert terminal after update/install]


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

Screenshot: Insert terminal showing successful clone + install


## Step 4: Configure Cowrie
**action:** Adjusted configuration file (cowrie.cfg) to set listening port (eg., 2222 for SSH)
File Path: cowrie/etc/cowrie.cfg

Screenshot: Insert config snippet showing port settings


## Step 5: Start Cowrie Service
**Action:** Launched honeypot  

**Command:**
```bash
bin/cowrie start
```

Screenshot: Insert terminal output showing Cowrie started


## Step 6: Test Honeypot Locally
**Action:** Attempted SSH connection from host to honeypot
**Command**
```bash
ssh -p 2222 root@<honeypot_IP>

**Expected Result:** Connection accepted, login attempts logged shell simulated
```
Screenshot: Insert terminal showing SSH attempt to honeypot


## Step 7: Verify Logs
**Action:** Checked honeypot logs for captured attempt
Log Path: cowrie/var/log/cowrie/cowrie.log

Screenshot: Insert log snippet of captured attempt 
