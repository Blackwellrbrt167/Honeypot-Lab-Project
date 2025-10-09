# Suricata IDS Installation and Configuration (Ubuntu Honeypot-VM)

### Overview
This walkthrough documents the complete installation and validation of **Suricata IDS/IPS/NSM** on an Ubuntu-based virtual machine.  
It forms part of my **Blue-Team Home Lab** that integrates with **Wazuh** and **Docker** for host and network-level visibility.

---

## Step 1 – Update and Prepare the System
**Action:** Updated the package lists and ensure required utilities are present.

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install software-properties-common -y

<img width="814" height="167" alt="suricata_installation_Step 1 " src="https://github.com/user-attachments/assets/a6a8a6b7-c2c5-435d-9371-dd91519cf754" />
```

## Step 2 - Add the Official Suricata PPA 
**Action:** Add the OISF stable repository to pull Suricata's latest supported version. 

```bash
sudo add-apt-repository ppa:oisf/suricata-stable
```
<img width="807" height="532" alt="Suricata_Installation_Step 2" src="https://github.com/user-attachments/assets/6b3b729a-19d5-4a8a-99cd-b80e428f924c" />

## Step 3 - Install Suricata and jq 
**Action:** Installed the IDS engine and dependencies including jq for JSON log parsing. 

```bash
sudo apt install suricata jq -y
```
<img width="650" height="178" alt="Suricata_Installation_Step 3 " src="https://github.com/user-attachments/assets/d78ec3c2-138e-4b05-b86e-a46474f857f0" />

<img width="1200" height="270" alt="Suricata_Installation_Step 4" src="https://github.com/user-attachments/assets/753ec9fd-4f0e-47f6-b910-b5c66967e8e8" />

## Step 4 - Fix Log Directory Permissions 
**Action:** Ensured Sricata has ownership of its log directory to prevent startup errors 

```bash
sudo chown -R suricata:suricata /var/log/suricata
sudo chmod -R 755 /va/log/suricata
```
<img width="815" height="102" alt="Suricata_Installation_Step 4_ Directory Ownership " src="https://github.com/user-attachments/assets/c5a55065-4049-4e4c-9798-02339e7c51b0" />

<img width="812" height="88" alt="Suricata_Installation_Step 4_ Ownership relation to others in directory" src="https://github.com/user-attachments/assets/3a700bb9-e603-4f83-86b8-d5e58f5f00cc" />

<img width="815" height="233" alt="Suricata_Installation_Step 4_Indirect Proof" src="https://github.com/user-attachments/assets/9c739f5b-da24-4f5e-8eb6-ddcf32b1e070" />

## Step 5 - Enable Suricata at Boot 
**Action:** Enable Suricata torun automatically on VM startup 

```bash
sudo systemctl enable suricata
```
<img width="1217" height="267" alt="Suricate Installation_Last Step " src="https://github.com/user-attachments/assets/21573ee9-12f7-43e8-bd41-53dad223a0f1" />

<img width="1042" height="108" alt="Suricata_Installation_Step 5_Active Systemd Link used to start Suricata at boot " src="https://github.com/user-attachments/assets/ae489eeb-c483-40b5-80a3-07983ee34708" />

<img width="811" height="87" alt="Suricata_Installation_Step 5_Autoconfiguration Confirmation " src="https://github.com/user-attachments/assets/12f0a088-674f-4182-9a72-2364dfd4a748" />

<img width="895" height="321" alt="Suricata_Installation_Step 5_Summary of all Lab critical services " src="https://github.com/user-attachments/assets/90cecd29-8aac-4c7c-874a-ab77ea262b6a" />






