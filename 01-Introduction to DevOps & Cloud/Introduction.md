# Introduction to DevOps & Cloud

## 🎯 Core Principles & Mission
- **Mission:** To take India forward in the IT sector by improving employability and taking it higher.
- **Core Principle (The Golden Circle):**
  - **Why? (Intent / Niyat):** To learn, upskill, switch jobs, and build strong fundamentals (90 Days Challenge).
  - **What? (Kya):** Go in-depth into DevOps, Cloud, AI, Kubernetes, and Docker.
  - **How? (Kaise):** Through consistency, live learning (asking doubts), notes, assignments, projects, and live mock interviews/scenario-based questions.

## 🚀 What is DevOps?
**DevOps** is a culture or mindset where Development and Operations teams collaborate to increase efficiency and accelerate delivery (SDLC).
- **History:** Coined in 2009 by Patrick Debois.
- **Why Does it Exist?** End users want fast solutions. Tech companies (FinTech, EdTech, etc.) need fast automation and scaling.
- **The Old Way (90s - 2000s):** The traditional Agile/Sprint model caused silos. Developers would write code, compress it (zip), and pass it to operations (System Admins -> Network Admins -> Database Admins -> QA/Testers). This resulted in a massive waste of time ("Samay Khoti").
- **The DevOps Way:**
  - **Reduce Time to Market:** Accelerate software delivery to end users.
  - **Collaboration:** Using effective tools like Git, Slack, and Jira to bridge the gap between Dev and Ops.
  - **Automation:** Reducing repetitive tasks using scripting (Python, Bash/Shell), GitHub Actions, and Jenkins.
  - **Scaling:** Transitioning from on-premise infrastructure to Cloud and Kubernetes.

## 🛡️ Reliability & SRE
Site Reliability Engineering (SRE) ensures that systems remain functional and robust.
- **Observability & Reliability:** Utilizing tools like OpenTelemetry (OTel), Prometheus, and Grafana.
- **Durable Execution System:** Building systems that ask, "What if nothing fails?"
> *"Everything fails all the time."* — Werner Vogels (Amazon CTO)
> This famous quote emphasizes that failure in complex systems is inevitable. Designers must build resilience, redundancy, observability, and fault tolerance (FT) into their systems.

## 🐧 Open Source Software (OSS) & Linux
OSS is not just about free software. It's a culture of learning, building, contributing, and running tools locally ("Learn in public").
- **Why Linux?** Over 90% of applications run on Linux. It is open-source, fast, secure, and widely distributed.
- **Learning Path:** Learn Linux -> Learn Git/GitHub -> Learn OSS Tools.

## 🏗️ System Foundations & Architecture

### 1. "Onion" Layered Architecture
Linux operates in layers, communicating from the user down to the physical hardware:
- **Users** interact with the -> **Shell**, which communicates with the -> **Kernel**, which manages the -> **Physical Hardware**.

### 2. "Upside-Down Tree" File System
Unlike Windows, Linux uses a single starting point called **Root (`/`)** for all files and hardware.
| Directory | Purpose |
| :--- | :--- |
| **`/etc`** | System Configuration files |
| **`/var/log`** | System and Application Error Logs |
| **`/bin`** | Essential User Binaries/Programs |

## 🗺️ Phase-Wise Learning (Divide & Conquer)
*A 90DaysOfDevOps challenge requires daily tasks, hands-on practice, and uploading work to GitHub.*

### Phase 1: Basics & Rhythm (1 Month)
- Understanding the *What, Why, and How*
- Linux & Networking fundamentals
- Git and GitHub
- Docker & Basic Projects

### Phase 2: Core DevOps (1 - 1.5 Months)
- **Automation:** Scripting (Bash, Python), GitLab, GitHub Actions, Jenkins.
- **Scaling:** Cloud platforms, Kubernetes (K8s).
- **Time to Market Reduction:** Terraform, Ansible.

### Phase 3: Advanced
- Diving into deeper architectural concepts and advanced integrations.
