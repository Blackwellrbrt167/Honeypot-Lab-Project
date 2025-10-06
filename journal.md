
# Security Lab Reflection Journal  

This journal captures my personal reflections, troubleshooting, and lessons learned while building and documenting my Cowrie honeypot lab environment.  

## 2025-09-09 – Honeypot Project Kickoff

### Raw Notes
With the raw notes in place and with the understanding of what I did today, you now know what was accomplished on Day One. I even took the time to research just what a honeypot is. See below:

- The purpose of a honeypot is to be used as a mechanism as an attack target to lure attackers away from their intended target.  

- Once the attacker is inside the honeypot will gather intelligence about the identity methods, and motivations of adversaries.  

- A honeypot can be modeled after any digital asset, this can include software applications, servers, or it can mimic the network itself. In laymen's terms the honeypot acts as a decoy.  

- A network of honeypots is defined as a honeynet. The design of a honeypot should mimic the network target an organization is trying to defend. Keep in mind that cybercriminals can also use honeypots as well.  

- The most common type of honeypot is the production honeypot.  

- Research honeypots are designed to collect information about the specific methods and techniques used by adversaries and what possible vulnerabilities exist.  

- Honeypots can be broken down into the type of activity I seek to detect.  

---

Just based upon my research and the relative simplicity, I will begin with Cowrie. The truth is that Dionaea was not that bad and I could understand what it was asking of me — that’s just because of education.  

As far as T-Pot was concerned, it was hard to understand anything. For them it was difficult to find the steps to set up the honeypot. Although I understood some of the material, I had to go through everything to attempt to locate where any documentation discussing the setup was found. The page was just so unorganized.  

---
## 09/10–09/12/2025 – Planning & Foundation  

**Work Completed:**  
- Sketched out the project concept: build a honeypot, capture alerts in a SIEM, practice isolating and analyzing, then tie the whole thing back to GRC frameworks like NIST CSF.  
- Researched honeypot options (Cowrie, Dionaea, T-Pot). Decided to lean toward Cowrie but hadn’t finalized it yet.  
- Structured GitHub repository plan: README.md for overview, Journal.md for reflections, folders for screenshots and documentation.  
- Committed to posting progress on LinkedIn — even though it feels uncomfortable — to build consistency and transparency.  

**Lessons Learned:**  
- I don’t have to do everything at once. Breaking this down into daily/weekly milestones is the only way this stays sustainable.  
- Sharing the journey feels awkward, but it forces accountability and might help someone else who’s in the same position.  
- A project like this is not just technical — it’s mindset, discipline, and building real habits.  

---

## 09/13/2025 – Project Kickoff & Research  

**Work Completed:**  
- Looked into honeypots and what they actually do — basically decoys to lure attackers, gather info, and either mimic an app, a server, or even a whole network. Learned about production vs. research honeypots and that a group of them is called a honeynet.  
- Read through docs for Cowrie, Dionaea, and T-Pot. T-Pot was a mess and hard to follow. Dionaea wasn’t bad but Cowrie’s docs just felt more straightforward, so I went with Cowrie to get moving.  
- Set up the GitHub skeleton (README.md, Journal.md, screenshot folders).  
- Sketched out the cycle I want to practice: honeypot → SIEM alert → isolation → analysis → breakdown → mitigation → compliance (mainly NIST CSF for now).  
- Decided this journal will be my raw thoughts, mistakes, and reflections, not polished case studies.  

**Lessons Learned:**  
- I get excited and want to rush, but I reminded myself speed isn’t the goal here — it’s about mastery and sticking with it.  
- Some documentation just isn’t beginner friendly (T-Pot). That’s not on me — it just means I need to pick tools I can realistically understand at my current level.  
- Setting up the repo first was the right call because now I have a place to drop my thoughts and screenshots without losing track.  
- Breaking this down into daily chunks makes the whole project less overwhelming, even if I end up working longer when I hit a flow state.  

---

## 09/14/2025 – Dependencies & Repo Setup  

**Work Completed:**  
- Installed required packages (`git`, `python3-pip`, `python3-venv`, etc.) after running into errors with missing dependencies.  
- Successfully cloned the Cowrie repository (`git clone http://github.com/cowrie/cowrie`).  
- Verified the repository by navigating into the folder (`cd cowrie`) and running `ls` to confirm the presence of expected files.  

**Lessons Learned:**  
- Always check which Python package manager (pip vs pip3) matches the environment to avoid confusion.  
- After cloning, confirm the repo contents before moving forward. Small confirmation steps prevent wasted time later.  
- Read error messages carefully — they usually point directly to what’s missing.  
- Installing in the wrong scope (system vs venv) will cause recurring headaches later.  

---

## 09/15/2025 – Virtual Environment, Config, & Permissions  

**Work Completed:**  
- Created and activated Python virtual environment (`python3 -m venv cowrie-env && source cowrie-env/bin/activate`).  
- Realized that being inside the virtual environment doesn’t mean I was in the right directory — confirmed using `pwd`.  
- Copied `cowrie.cfg.dist` to `cowrie.cfg` inside `~/cowrie/etc`. Initially hit “permission denied” until running `sudo`.  
- Attempted to start Cowrie but ran into log file permission errors. Fixed by creating the log directory `/var/log/cowrie/` and assigning proper ownership and permissions:  
  - `sudo mkdir -p /var/log/cowrie/`  
  - `sudo chmod -R 755 /var/log/cowrie/`  
  - `sudo chown -R vboxuser:vboxuser /var/log/cowrie/`  

**Lessons Learned:**  
- Being “inside” the virtual environment is not the same as being in the correct directory. Both must align.  
- Using `pwd` is a simple but powerful command for orientation inside the filesystem.  
- Always `cd` into the correct subdirectory before attempting file operations.  
- Use `ls -l` to inspect file permissions instead of guessing.  
- Cowrie cannot and should not be run as root — permissions need to be aligned with the intended user.  
- It also impressed upon me to make sure the respective file I am attempting to download or use has the correct permissions required. Thus it should always start with a simple check of what permissions are required before attempting changes.
  

---

## 2025-09-20 — Decision to Add a SIEM

After successfully building a honeypot using Cowrie, I realized it was important to add a SIEM to my lab environment. This would enable me to interpret the data patterns of the simulated attacks targeting the honeypot. While I could have chosen to analyze the logs manually, I felt that as a student it was better to practice using a SIEM to mirror the daily workflow of a SOC analyst.

Even though my ultimate career focus is in GRC, I believe it’s critical to build a technically driven background. Since I am already learning the technical side through my education, expanding into the SOC environment felt like the right next step. GRC also carries a strong consulting perspective, and I want to fully understand the technical realities behind the policies and frameworks.

I know this journey will be frustrating at times, especially as someone who tends toward perfectionism and often digs deeply into the weeds of problem-solving. But it is a journey worth embracing—one that will have a lasting impact as I push forward toward lifelong mastery.

---

### 2025-10-06 — Docker Installation and the Importance of Preparation

After the challenges I faced during the Wazuh installation, I learned one of the most valuable lessons in my technical journey so far: **preparation determines success.** During that setup, I spent hours resolving errors caused by missing dependencies and permissions — mistakes that were not the result of carelessness, but of inexperience. It was a necessary part of the learning curve. I realized then that every successful deployment, no matter how complex, is built upon a foundation of understanding system requirements and environment dependencies before typing the first command.

That experience changed how I approach every new lab. So when it came time to install Docker — a prerequisite for deploying Shuffle as part of my SOAR environment — I refused to rush. I read the official documentation line by line, verified that Ubuntu had the necessary packages installed, and reviewed each step before executing it. Because of that, the installation went smoothly from start to finish. No permission issues, no broken configurations, no wasted time — just clean, intentional progress. 

This reinforced something I’ve been slowly internalizing as I move deeper into cybersecurity: **mastery doesn’t come from speed; it comes from deliberate understanding.** I now take pride in slowing down, in documenting every detail, and in ensuring I truly know *why* each step matters. Docker’s installation was not just about getting a container engine to run — it was about proving to myself that I can build and manage my environments responsibly.

From a learning perspective, Docker has also deepened my appreciation for containerization in cybersecurity. Reading through Docker’s and Sysdig’s documentation, I came to understand that Docker is far more than a developer tool — it’s a foundational technology for how modern security operations are structured. Containers provide isolated environments that allow systems and applications to run without impacting the host. In the context of a Security Orchestration, Automation, and Response (SOAR) platform like Shuffle, containers are essential. They enable scalable, repeatable, and secure deployment of workflows — helping automate and orchestrate incident response in a controlled way.

This concept resonates deeply with how I now see Blue Team work. Security is no longer just about defending a single system; it’s about architecting reliable environments that can adapt, detect, and respond with precision. Docker represents that flexibility — the ability to isolate, replicate, and automate defenses just as developers automate code deployments. 

The `hello-world` verification was simple on the surface, but meaningful to me. Seeing that confirmation message — “Hello from Docker!” — was symbolic of something larger. It was a quiet reminder that technical success comes not from guessing, but from growth through repetition, study, and reflection.

If the Wazuh setup taught me humility, the Docker installation taught me confidence. I didn’t just install a piece of software — I solidified a mindset. Going forward, I will continue to document not only the commands I run but the reasoning behind them. Because understanding why something works is the only true foundation for mastery.

---

**Reference:**  
Docker Official Documentation – [https://www.docker.com/resources/what-container/](https://www.docker.com/resources/what-container/)  
Sysdig – [https://www.sysdig.com/learn-cloud-native/orchestration-containerized-architecture](https://www.sysdig.com/learn-cloud-native/orchestration-containerized-architecture)


