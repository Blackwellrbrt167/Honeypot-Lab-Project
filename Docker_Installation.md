# Docker Installation (Lab Documentation)

This document provides a **complete walkthrough** of installing **Docker Engine** on **Ubuntu 24.04 (Honeypot-VM)**.  
It includes the **exact commands used** during installation and the **screenshots** that visually demonstrate each step.  
This setup forms the foundation for deploying the **Shuffle SOAR (Security Orchestration, Automation, and Response)** platform in a controlled lab environment.

---

## What is Docker?

According to [Docker.com](https://www.docker.com/), **Docker** is an open platform for developing, shipping, and running applications.  
Docker uses **containerization technology** to separate applications from the underlying system, ensuring that they run consistently across different environments.

In simple terms, a **container** is an isolated environment that includes everything needed to run an application—code, runtime, libraries, and dependencies.  
This isolation ensures that the host system’s resources are not directly impacted and that each application runs independently of others.

For the purposes of this project, Docker is being used to deploy **Shuffle SOAR**. Containers serve two primary roles in this security automation context:

1. **Data Structures for Security Events** – Containers help structure and process incident data in isolated environments.
2. **Self-Contained Deployment Environments** – Each component of the SOAR platform (e.g., APIs, dashboards, integrations) runs in its own containerized environment.

In short, Docker enables scalable, reliable, and secure deployment of cybersecurity automation tools like Shuffle.

**Reference:**  
[Sysdig: Understanding Container Orchestration and Architecture](https://www.sysdig.com/learn-cloud-native/orchestration-containerized-architecture#:~:text=Container%20orchestration%20platforms%2C%20like%20Kubernetes,%2C%20deploy%2C%20and%20manage%20containers.)

---

## Step 1: System Preparation

**Action:** Update the package list to ensure all repositories are current.

**Command:**
```bash
sudo apt update
```
<img width="725" height="293" alt="Docker_Installation_Step 1" src="https://github.com/user-attachments/assets/46985a1d-bd8d-4b62-b83c-48483758480b" />

## Step 2: Install Prerequisite Packages 
**Action:** Install necessary dependencies to allow secure repository access and package management.  

**Command:** 
```bash
sudo apt install apt-transport-https ca-certificates curl software-properties-common -y
```
<img width="1280" height="816" alt="Docker_Installation_Step 2 " src="https://github.com/user-attachments/assets/fb8a06a4-91a2-47a2-936b-ccec72ed4def" />

## Step 3: Add Docker's Official GPG Key 
**Action:** Add Docker's trusted signing key for verifying package authenticity. 

**Command:** 
```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \ sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```
<img width="1290" height="385" alt="Docker_Installation_Step 3 " src="https://github.com/user-attachments/assets/99d283d7-521e-444b-903e-3f7bf951bda8" />

## Step 4: Add the Docker Repository 
**Action:** Add Docker's stable repository to APT sources. 

**Command:** 
```bash
echo \ :deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] \ https://download.docker.com/linux/ubuntu \ $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
<img width="983" height="610" alt="Docker_Installation_Step 4 " src="https://github.com/user-attachments/assets/aedc2487-5a9f-4587-9a04-3922897ec269" />

## Step 5: Refresh and Upgrade Packages 
**Action:** Update system repositories and upgrade installed packages.

**Command:** 
```bash
sudo apt update
sudo apt upgrade -y
```
<img width="1215" height="692" alt="Docker Installation_Step 5_1" src="https://github.com/user-attachments/assets/1343a71b-7351-450b-ad1f-97c21438095b" />

<img width="1211" height="638" alt="Docker_Installation_Step 5_2 " src="https://github.com/user-attachments/assets/6a34937d-8d9d-4e2d-8684-cec5cb1aea10" />

<img width="1212" height="272" alt="Docker_Installation_Step 5_3" src="https://github.com/user-attachments/assets/228eaf66-d677-4b8c-996d-4e0cb4097e17" />

## Step 6: Install Docker Engine, CLI, and Components 
**Action:** Install Docker Engine, Socker CLI, the container runtime, and additional plugins for Buildx and Compose. 

**Command:** 
```bash
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
```

<img width="1212" height="307" alt="Docker Installation_Step 6" src="https://github.com/user-attachments/assets/71eedb2c-6ad0-4120-a47e-e9104419638f" />

## Step 7: Verify Docker Installation
**Action:** Verify Docker installation by running the sample test container hello-world

**Command:** 
```bash
sudo docker run hello-world
```
<img width="888" height="568" alt="Docker Installation_Step 7 " src="https://github.com/user-attachments/assets/7f7ccd0e-de2b-4b7b-80ab-b160284624d7" />









