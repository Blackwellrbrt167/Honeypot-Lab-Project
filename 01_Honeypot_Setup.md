This document will captures the step-by-step process of setting up the honeypot environment, including VM creation, installation, configuration, and verifiction 

# Honeypot Setup (Cowrie)

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

<img width="1203" height="753" alt="HoneyPot_VM_Package Install_Part 2 " src="https://github.com/user-attachments/assets/be2cd4ef-5537-4286-926b-084db188e7af" />

<img width="1223" height="701" alt="HoneyPot_VM_Package Install_Part 3" src="https://github.com/user-attachments/assets/a21a78ac-6665-4fb3-9609-78a6dd61ed08" />

<img width="1217" height="750" alt="HoneyPot_VM_Python Package Install" src="https://github.com/user-attachments/assets/b60d82b9-149b-4c53-a7a0-7e63a7016b51" />


<img width="823" height="590" alt="Cowrie_Dependencies" src="https://github.com/user-attachments/assets/af8bafd6-bce7-48e4-b26d-722297226dfd" />


## Step 3: Install Cowrie system dependencies
**Action:** Installed system-wide support for python virtual environments and other dependencies  Actual Python packages are installed later. This includes the requirements update.


**Commands:**
```bash
sudo apt-get install git python3-pip python3-venv libssl-dev libffi-dev build-essential libpython3-dev python3-minimal authbind

python -m pip install --upgrade -r requirements.txt 
```

<img width="823" height="590" alt="Cowrie_Dependencies" src="https://github.com/user-attachments/assets/d9505f73-d3b4-4ffb-9c8d-677b18c6e870" />

<img width="1252" height="757" alt="Update of Requirments file " src="https://github.com/user-attachments/assets/781d01ea-fc74-4593-9107-188fd8dd4ec2" />

<img width="1268" height="752" alt="Update of Requirements file_2" src="https://github.com/user-attachments/assets/7c38e0d0-2fd0-49f7-afca-caa5e601cc27" />


## Step 4: Create a user account 
**Action:** Created a dedicated non-root user id: 

**Commands**
```bash
sudo adduser --disabled-password cowrie

sudo su - cowrie
```
<img width="820" height="392" alt="Creation of Non privileged User " src="https://github.com/user-attachments/assets/abbb7b03-9e97-4e6f-a1cd-9788d27a4c2c" />


## Step 5: Clone and Install Cowrie

**Action:** Cloning and installing are required to get Cowrie running because it is an open-source project hosted on GitHub, not a standard software package. In the respective screenshot I was moving so fast and forgot to copy the original input of the command so I simply chose to reenter as a means to check to make sure I was able to install. 

**Commands**
```bash
git clone http://github.com/cowrie/cowrie

cd cowrie

cd ~/cowrie
ls 
```

<img width="822" height="576" alt="Cowrie Clone Installtion_Confrimation_1" src="https://github.com/user-attachments/assets/8cc788d1-1c54-40c8-8ddf-710a50c3b44f" />

<img width="895" height="242" alt="Cowrie DIrectory Access" src="https://github.com/user-attachments/assets/cb0091c0-aeae-4fcb-97e8-d6d1b62fecd3" />


## Step 6: Setup Virtual Environment 

**Action:** Creation of the Virtual Environment for Cowrie for dependency management and isolation

**Command**
```bash
pwd
python3 -m venv cowrie-env
```
<img width="822" height="576" alt="Cowrie_virtual environment setup " src="https://github.com/user-attachments/assets/ff786300-0bad-44f3-b74c-823ed318cc9d" />


## Step 6a: Activating Virtual Environment and Install Packages 
**Action:** Acivating the virtual environment to isolate its python dependencies to ensure tha tthe honeypot functions correctly and avoids coflicts with other projects on the system. 

**Command**
```bash
source cowrie-env/bin/activate
```
<img width="817" height="466" alt="Cowrie_Activation of Virtual environment" src="https://github.com/user-attachments/assets/85f1c650-b346-4e6f-836f-2f528a9ad292" />


## Step 7: Installation of Cowrie Configuration File 

**action:** The configuration is stored in cowrie.cfg.dist and cowrie.cfg.  these files will be read on startup. the entries from the cowrie.cfg file will take precedence in this regard. 

**Command**
```bash

cd ~/cowrie/etc
ls -l cowrie.cfg.dist
sudo cp cowrie.cfg.dist cowrie.cfg
```
<img width="897" height="248" alt="Cowrie Configuration Install " src="https://github.com/user-attachments/assets/aa1193eb-6953-4bac-bee9-7f6168f0fe82" />


## Step 8: Cowrie Log file setup (Pre-Cowrie Start) 

**Action:** The goal here was to provide the permissions and directory creation necessary so that Cowrie can function how it is suppose to function 
```bash
sudo mkdir -p var/log/cowrie
sudo mkdir -p var/run 
sudo chmod -R 766 var/log/cowrie
sudo chown -R vboxuser:vboxuser var/log/cowrie
sudo chown -R vboxuser:vboxuser var/run 
```
<img width="1235" height="690" alt="Cowrie File permission install_1" src="https://github.com/user-attachments/assets/285fb064-606d-4942-8a2b-18bc19c27ee7" />

<img width="1213" height="97" alt="Cowrie File permission install_2 " src="https://github.com/user-attachments/assets/5237a506-1c5f-479e-beec-5f66e0476200" />


## Step 9: Start Cowrie Service
**Action:** Launched honeypot  for confirmation of installation 

**Command:**
```bash
bin/cowrie start
```

<img width="1227" height="140" alt="Cowrie Start Confirmation " src="https://github.com/user-attachments/assets/adc9f6e1-9317-4390-805b-e0cc7115c6c0" />


## Step 10: Test Honeypot Locally
**Action:** Attempted SSH connection from host to honeypot  

**Command (from host machine):**
```bash
ssh -p 2222 root@<honeypot_IP>
```

**Expected Result:** Connection accepted, login attempts logged shell simulated

Screenshot: Insert terminal showing SSH attempt to honeypot


## Step 11: Verify Logs
**Action:** Checked honeypot logs for captured attempt
Log Path: cowrie/var/log/cowrie/cowrie.log

Screenshot: Insert log snippet of captured attempt 

## Summary
- VM created and Ubuntu installed  
- Cowrie cloned, configured, and started successfully  
- Verified login attempts are captured in logs  
- Evidence stored in `/evidence` folder  

Next step: Forward logs to SIEM for alert generation.

