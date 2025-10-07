# Shuffle SOAR Installation and Troubleshooting  
### Integration with Wazuh SIEM on Ubuntu 22.04 LTS VM  

---

## Objective
Deploy and configure **Shuffle SOAR** within an existing **Wazuh SIEM** environment.  
Resolve OpenSearch port conflicts and verify both systems running concurrently inside a single virtual machine.

---

## Step 1 — Update and Prepare the System

**Action:** Ensure all system packages are updated and Docker is installed and active.

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y docker.io docker-compose git curl
sudo systemctl enable docker
sudo systemctl start docker

```
<img width="1227" height="752" alt="Shuffle Installation_Update_Upgrade System Packages_Step 1 " src="https://github.com/user-attachments/assets/34a086d4-7832-4655-a52e-c7ae2280b075" />

## Step 2 - Clone the Shuffle Repository 
**Action:** Clone Shuffle's official Github repository to the VM and navigate into the project directory.

```bash
git clone https://github.com/frikky/Shuffle.git
cd Shuffle
```
<img width="898" height="216" alt="Shuffle_Installation_Clone Shuffle Github Repository_Step 2" src="https://github.com/user-attachments/assets/8a049338-face-4d23-9ee3-c78055b58666" />

## Step 3 - Install Docker Compose 
**Action:** Install Docker Compose

```bash
sudo apt install docker-compose -y

```
<img width="1227" height="445" alt="Shuffle Installation_Docker Compose Installation" src="https://github.com/user-attachments/assets/64e9a9da-6d50-4a72-8ac7-23ac49f671e1" />

## Step 4 - Attempt the initial Shuffle Deployment 
**Action:** Ran Shuffle for the first time using Docker Compose 

```bash
sudo docker compose up -d

**Error** 

driver failed programming external connectivity on endpoint shuffle-opensearch:
failed to bind host port for 0.0.0.0:9200/tcp: address already in use

```
<img width="1267" height="240" alt="Problem with shuffle " src="https://github.com/user-attachments/assets/bd0862d5-9176-4135-8bbc-0e04ae1ec7a6" />

<img width="1245" height="391" alt="Shuffle problem_2 " src="https://github.com/user-attachments/assets/d415dd1f-d456-4685-9993-055115c03f45" />

**This show the exact error message revelaing a port binding conflict on port 9200**

## Step 5 - Diagnose the Port Conflict 
**Error indicated that port 9200 was already in use.**
**Action:** Identified the active process using that port

```bash
sudo ss -ltnp | grep -E ':(9200|9300)'

```
**Result:** Wazuh's Opensearch service was already listening on 9200 and 9300.  This confirmed that Shuffle and Wazuh were attempting to share the same Opensearch ports.  

## Step 6 - Edit the Docker Compose Configuration 
**Action:** Rather than shutting down Wazuh, I remapped Shuffle's Opensearch ports to avoid overlap then Opened the Docker's Compose file: 

```bash
sudo nano docker-compose.yml
```
**Action 2:** Located the opensearch service and modify:

```bash
ports:
  - "19200:9200"
  - "19300:9300"
```
<img width="1197" height="645" alt="Shuffle_Installation_Opensearch Port change " src="https://github.com/user-attachments/assets/172be55e-c46b-41d1-bd6c-cf906cd92ce0" />

## Step 7 - Rebuild and Restart Shuffle 
**Action:** Rebuilt and redeployed the Shuffle containers with the new port configuration..

```bash
sudo docker compose down
sudo docker compose up -d

```
<img width="905" height="183" alt="Shuffle Installtion_Shuffle Started" src="https://github.com/user-attachments/assets/db18ac91-f1a7-466c-aa19-6bfd656b9528" />

<img width="1128" height="121" alt="Shuffle_Installation_Container Status" src="https://github.com/user-attachments/assets/06b8c9cb-de4d-4295-8f5f-a8c79819a9ce" />

## Step 8 - Verify Active Containers and Ports 
**Action:** Verified that both Wazuh and Shuffle containers are running on separate ports. 

```bash
sudo docker ps --format '{{.Names}}\t{{.Ports}}'
sudo ss -ltnp | grep -E ':(9200|9300|19200|19300)'

```

**Expected Results:** Wazuh: 9200/9300 | Shuffle 19200/19300 

<img width="1128" height="121" alt="Shuffle_Installation_Container Status" src="https://github.com/user-attachments/assets/4b911e15-85ee-42e8-8186-d99c8645f6fd" />

<img width="1260" height="146" alt="Shuffle_Installation_Problem fixed_confirmation " src="https://github.com/user-attachments/assets/be4fe352-f79b-43f0-a9ca-51981e000577" />








