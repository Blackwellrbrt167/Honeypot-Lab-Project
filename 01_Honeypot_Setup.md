This document will captures the step-by-step process of setting up the honeypot environment, including VM creation, installation, configuration, and verifiction 

# Honeypot Setup (Cowrie Example)

This document captures the step-by-step process of setting up the honeypot environment, including VM creation, installation, configuration, and verification.

---

## Step 1: Virtual Machine Creation
**Action:** Created a new Ubuntu Server 22.04 VM in VirtualBox/VMware  
**Specs:** 2 CPU, 4 GB RAM, 20 GB disk  
**Network Mode:** Bridged or NAT with Port Forwarding  

<img width="1075" height="875" alt="HoneyPot_VM_Setup" src="https://github.com/user-attachments/assets/e1efdeb5-8fde-4799-8356-c43d88f621b6" />


---

## Step 2: Update & Install Dependencies
**Action:** Updated system and installed required packages  

**Commands:**
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install git python3-venv python3-pip -y

```
<img width="1148" height="767" alt="HoneyPot_VM_Packaage Install_Part 1 " src="https://github.com/user-attachments/assets/3ba6a630-8fd0-4d8b-88ec-c8daadcc2fe5" />

<img width="1203" height="753" alt="HoneyPot_VM_Package Install_Part 2 " src="https://github.com/user-attachments/assets/b1c224e1-6179-4512-aadb-6189dca46fc8" />

<img width="1223" height="701" alt="HoneyPot_VM_Package Install_Part 3" src="https://github.com/user-attachments/assets/7f7e129a-aa9e-49a0-a3f4-d5291cbbcd1d" />

<img width="1222" height="754" alt="HoneyPot_VM_Package Install_Part 4" src="https://github.com/user-attachments/assets/d9a5f965-cb14-4890-829c-31deafec3f02" />



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

<img width="822" height="576" alt="Cowrie Clone Installtion_Confrimation_1" src="https://github.com/user-attachments/assets/470e251d-e28f-4ac8-b879-10d55e087c1b" />



## Step 4: Configure Cowrie
**action:** Adjusted configuration file (cowrie.cfg) to set listening port (eg., 2222 for SSH)
File Path: cowrie/etc/cowrie.cfg

<img width="823" height="590" alt="Cowrie_Dependencies" src="https://github.com/user-attachments/assets/9cd67132-7c28-43df-8807-e4e3ff9c4b26" />

<img width="822" height="576" alt="Cowrie Clone Installtion_Confrimation_1" src="https://github.com/user-attachments/assets/6c5c66f9-ee93-4de1-892a-cef1214ea7ff" />

<img width="822" height="576" alt="Cowrie_virtual environment setup " src="https://github.com/user-attachments/assets/ac1b611d-5c4c-44c9-bd74-5aa42e4d3d5f" />

<img width="820" height="392" alt="Creation of Non privileged User " src="https://github.com/user-attachments/assets/6297992b-bc3e-4772-ae1e-162134a93e9a" />

<img width="817" height="466" alt="Cowrie_Activation of Virtual environment" src="https://github.com/user-attachments/assets/920a5073-e8b2-4f91-9e64-b27c40e4446a" />

<img width="895" height="242" alt="Cowrie DIrectory Access" src="https://github.com/user-attachments/assets/c41e00e3-692a-416c-afaa-b7122044c6d6" />

<img width="812" height="576" alt="Cowrie directory_confirmation " src="https://github.com/user-attachments/assets/c6c4cba3-dfa1-4c45-be14-2765aedf2e37" />

<img width="1252" height="757" alt="Update of Requirments file " src="https://github.com/user-attachments/assets/ccc39b42-d6f8-49de-8d7f-0f237459e9f2" />

<img width="1268" height="752" alt="Update of Requirements file_2" src="https://github.com/user-attachments/assets/11f38032-2bd1-41cb-a3a8-2363f35c7613" />




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

