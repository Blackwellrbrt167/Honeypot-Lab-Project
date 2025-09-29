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

## Step 5: Install Wazuh Manager
**Action:** Install the Wazuh Manager package 

**Command** 
```bash

sudo apt-get install wazuh-manager -y
```
<img width="890" height="727" alt="Installing the Wazuh manager_1 " src="https://github.com/user-attachments/assets/6030b1f0-b024-44bf-a080-f86ceac573f8" />

<img width="831" height="417" alt="56_fresh_install_Manager" src="https://github.com/user-attachments/assets/111978f1-ead3-4bc5-b756-190dc1f0bad1" />

## Step 6: Verify Wazuh Manager Service 
**Actions:** Ensure the service is running 

**Commands** 
```bash
sudo systemctl status wazuh-manager

```
<img width="841" height="500" alt="57_manager_running" src="https://github.com/user-attachments/assets/4dc0ab5c-d3b7-4dff-a759-8246d21d8451" />

## Step 7: Cleanup of Old or Broken Packages (If you hit errors) 
**Actions:** Remove stuck/broken agent/manager installs, purges leftovers, verify clean state. 

**Commands** 
```bash
# What’s installed?
dpkg -l | grep wazuh

# Try removing agent (ignore failures)
sudo apt-get purge wazuh-agent -y || true
sudo dpkg --remove --force-remove-reinstreq wazuh-agent || true
sudo dpkg --purge --force-all wazuh-agent || true

# Remove broken maintainer scripts & leftover systemd units (if present)
sudo rm -f /var/lib/dpkg/info/wazuh-agent.*
sudo rm -f /etc/systemd/system/wazuh-agent.service
sudo rm -f /lib/systemd/system/wazuh-agent.service
sudo rm -f /usr/lib/systemd/system/wazuh-agent.service
sudo systemctl daemon-reexec
sudo systemctl daemon-reload

# Purge manager if you need a fresh re-install
sudo apt-get purge wazuh-manager -y
sudo apt autoremove -y

# Verify clean
dpkg -l | grep wazuh || echo "No wazuh packages installed."
 ```

<img width="832" height="71" alt="Step 1_Checking Installed Packages " src="https://github.com/user-attachments/assets/ed55eea3-c126-4f42-8e28-55016fe26117" />

<img width="837" height="402" alt="Step 2_Attempt Purge " src="https://github.com/user-attachments/assets/ddb31d04-8a4d-44f8-ac9a-107b5cacf399" />

<img width="813" height="177" alt="Force removal fails " src="https://github.com/user-attachments/assets/99c9fb87-8896-48c6-b314-86abdea2fec3" />

<img width="816" height="132" alt="step 4_Delete Broken maintainer scripts" src="https://github.com/user-attachments/assets/5d5513c0-478f-419a-8338-3dfe486b678d" />

<img width="822" height="107" alt="Step 5_Remove leftover systemd units " src="https://github.com/user-attachments/assets/05dc7699-bf82-4f05-9e1f-cb4ae14a1770" />

<img width="787" height="68" alt="retry purge " src="https://github.com/user-attachments/assets/b0d227f0-c09a-4f0d-9273-6450321571b7" />

<img width="883" height="63" alt="Final check of Wazuh removal " src="https://github.com/user-attachments/assets/96d092f9-9f49-4fe7-9f04-ba5140e32d68" />

<img width="787" height="227" alt="54_purge_manager" src="https://github.com/user-attachments/assets/483df2a0-e1ac-4518-ad38-a30a3996f651" />

<img width="687" height="107" alt="54_purge_manager_2 " src="https://github.com/user-attachments/assets/629cf590-70a7-4324-8f68-8ed6726750fe" />

<img width="557" height="27" alt="55_verify_clean" src="https://github.com/user-attachments/assets/87c72674-a497-451f-9a35-d435cb695782" />


## Step 8: Reinstall Wazuh Manager (Clean path) 
**Action:** Install a fersh manager after cleanup 

**Commands** 
```bash 

sudo apt-get install wazuh-manager -y

```

<img width="831" height="417" alt="56_fresh_install_Manager" src="https://github.com/user-attachments/assets/2f854877-e42e-41a2-a93b-cae80296390c" />

## Step 9: Install Wazuh Indexer (Optional) 
**Action:** Install Indexer if you're building components separately 

**Commands** 

```bash
sudo apt-get install wazuh-indexer -y

```
<img width="832" height="422" alt="Installing Wazuh indexer_step 1" src="https://github.com/user-attachments/assets/21e3de27-2b15-4237-bfd8-3f5d9f141ea5" />

## Step 10: Fix Indexer Permissions (If you see cert/perm errors) 
**Actions:** Resolve root-ca.pem/permission errors by correcting ownership and perms. 

**Commands:** 

```bash

sudo chown -R wazuh-indexer:wazuh-indexer /etc/wazuh-indexer /var/lib/wazuh-indexer
sudo chmod -R 750 /etc/wazuh-indexer /var/lib/wazuh-indexer
ls -ld /etc/wazuh-indexer /var/lib/wazuh-indexer

```
<img width="855" height="613" alt="Log cluster file denoting Permission error" src="https://github.com/user-attachments/assets/b1130bfb-0898-4e8e-8c9c-5f409bddf85f" />

<img width="825" height="580" alt="Wazuh cliuster log showing root cause to non start " src="https://github.com/user-attachments/assets/18e67957-a016-495e-be72-129d4ea62cdc" />

<img width="817" height="87" alt="Permission given to Wazuh Configuration Directory and Confirmation" src="https://github.com/user-attachments/assets/1692bc9a-2063-4918-8344-0eedc0ced2a1" />

<img width="835" height="122" alt="Permission and confirmation of Wazuh data directory " src="https://github.com/user-attachments/assets/6dd6970c-11f7-47bb-acb6-6d479dcbf7ab" />

## Step 11: Assisted All-in-One Installer (Optional) 
**Action:** Install Manager + Indexer + Dashboard via helper script 

**Commands:** 

```bash

curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
sudo ./wazuh-install.sh -a -o

```






































