# Wazuh Installation (Lab Documentation)

This document captures the step-by-step process of installing and configuring Wazuh as part of the honeypot lab environment. The Wazuh Manager, Dashboard, and Agent setup will allow monitoring and log collection from Cowrie and other systems.

---

## Step 1: System Preparation
**Action:** Update system packages and dependencies.  

**Commands:**
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install curl apt-transport-https unzip wget -y
```
<img width="818" height="158" alt="Step 1_Wazuh Installation_Installing Dependencies_" src="https://github.com/user-attachments/assets/b31dda1e-7ce0-4a6c-8283-784d93b082c1" />

<img width="846" height="498" alt="Step 1b_wazuh installation_installing dependencies_2" src="https://github.com/user-attachments/assets/010a7952-54e4-48bb-a543-9ce01b286aa3" />

<img width="812" height="531" alt="Updating system in preparation for Wazuh Dashboard_Indexer_Manager_Step 1 " src="https://github.com/user-attachments/assets/300abc17-c3ba-4acf-8e91-51071044889a" />


## Step 2: Verify and Expand Disk Partition 
**Action:** Confirm space, extend the partition, and resize the filesystem 

**Commands** 

```bash
lsblk
sudo growpart /dev/sda 2
sudo resize2fs /dev/sda2
df -h
```
<img width="741" height="417" alt="16_lsblk_before" src="https://github.com/user-attachments/assets/233ae94d-2509-41a0-a2e9-3908c6fc7349" />

<img width="822" height="70" alt="17_growpart_sda2" src="https://github.com/user-attachments/assets/04c76ece-ebd9-4bad-bef3-9c678b38d2fe" />

<img width="687" height="118" alt="18_resize2fs_sda2" src="https://github.com/user-attachments/assets/cf127f71-9d39-4a04-9e9b-7200772d9afc" />

<img width="536" height="128" alt="19_df_after_resize" src="https://github.com/user-attachments/assets/9326df32-8479-4ff3-bc24-c1e98fdd2116" />

## Step 3: Install GnuPG and HTTPS Transport 

**Commands**

```bash
sudo apt-get install gnupg apt-transport-https -y

```
<img width="830" height="485" alt="Installation of two packages_GNU Privacy Guard and Apt transport " src="https://github.com/user-attachments/assets/8805eda4-9019-4054-97e3-453556021138" />

## Step 4: Add Wazuh Repository and GPG Key 
**Action:** Import Wazuh's GPG key, add the apt repo, update metadata 

**Commands:** 
```bash
wget -O - https://packages.wazuh.com/key/GPG-KEY-WAZUH | \
  sudo gpg --dearmor -o /usr/share/keyrings/wazuh.gpg

echo "deb [signed-by=/usr/share/keyrings/wazuh.gpg] https://packages.wazuh.com/4.x/apt stable main" | \
  sudo tee /etc/apt/sources.list.d/wazuh.list

sudo apt-get update
```
<img width="912" height="283" alt="Importing Wazuh repository's GPG signing key into the system " src="https://github.com/user-attachments/assets/6ebc8883-1ec9-4d56-8f19-bd8116711848" />

<img width="832" height="327" alt="Adding the Wazun repository " src="https://github.com/user-attachments/assets/e8cca129-5429-4f8b-bc67-32f7260e6778" />
















