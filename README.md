# Wazuh-SIEM-deployment-lab
Your full Guideline on how to install, deploy and use the Wazuh SIEM tool for newbies.



# Ubuntu Desktop (Single-Node Architecture)

## Overview

This project documents the full deployment and configuration of a Wazuh SIEM platform on an Ubuntu 22.04 Desktop virtual machine using VirtualBox.
The goal of this lab is to simulate a real-world Security Operations Center (SOC) environment by deploying a centralized log monitoring and threat detection solution.
This lab serves as Phase 1 of a complete Home SOC Lab, forming the security monitoring backbone for future integrations (Windows endpoint monitoring, log forwarding, attack simulations, etc.).


## Setup Architecture

<img width="730" height="457" alt="Untitled Diagram drawio" src="https://github.com/user-attachments/assets/1782c810-30e0-4783-a580-ae2144d84777" />




## Project Objectives

* Deploy a centralized SIEM server using Wazuh

* Understand Wazuh architecture and core components

* Configure networking for dashboard access

* Validate services and ensure proper indexing

* Prepare the environment for endpoint onboarding

* Build foundational Blue Team operational skills


## What is Wazuh?

#### Wazuh is an open-source security monitoring platform that provides:

* Log analysis

* Intrusion Detection (HIDS)

* File Integrity Monitoring (FIM)

* Vulnerability detection

* Threat intelligence integration

* Security configuration assessment

* Compliance monitoring (PCI DSS, HIPAA, GDPR, etc.)

#### Wazuh is widely used in SOC environments to detect suspicious activity and security incidents in real time.


## Wazuh Architecture (Single-Node Deployment)

#### This lab uses a single-node deployment, meaning all core components run on the same server.

## Core Components**

### 1. Wazuh Manager

* Collects logs from agents

* Performs rule-based analysis

* Generates alerts

* Detects intrusions and anomalies

### 2️. Wazuh Indexer

* Stores and indexes processed logs

* Based on OpenSearch

* Enables fast search and data retrieval

### 3️. Wazuh Dashboard

* Web-based interface

* Visualizes alerts and logs

* Provides investigation tools

* Used for SOC monitoring

### 4️. Wazuh Agent

* Installed on endpoints (Windows/Linux)

* Sends logs and telemetry to the Manager

#### In this deployment, Manager + Indexer + Dashboard are installed together in a single VM.

## Lab Environment

### Component	Specification

* Host OS	Windows 11
* Hypervisor	VirtualBox
* Guest OS	Ubuntu 22.04 Desktop
* RAM Allocated	4GB
* CPU Cores	2
* Disk Space	50GB
* Network Mode	NAT
* Port Forwarding	Host 8443 → Guest 443
  
#### System Requirements (Recommended Minimum)



#### To successfully deploy Wazuh in a single-node setup:

✅ 4GB RAM (allocated to VM)

✅ 2 CPU cores

✅ 50GB disk space

✅ Stable internet connection

✅ VirtualBox installed on host

✅ Ubuntu 22.04 Desktop ISO



## ⚠️ Performance Note:
The Wazuh Indexer (OpenSearch-based) is resource-intensive.
Close unnecessary applications on the host machine during installation.



## 🛠️ Troubleshooting Tips
### 🔹 Dashboard Not Loading

* Verify port forwarding settings
* Ensure dashboard service is running
* Confirm no firewall blocking port 8443

### 🔹 Indexer Fails to Start

* Check available RAM
* Review logs:
     sudo journalctl -u wazuh-indexer

### 🔹 High CPU Usage

* Normal during indexing
* Allow system to stabilize for 5–10 minutes



### 🔐 Security Considerations

* This lab uses NAT for isolation

* Self-signed certificates are used by default

* Production deployments should:

* Use TLS certificates

* Harden firewall rules

* Implement role-based access control



## 🚀 Future Enhancements (Next Phase)

* Deploy Windows 11 endpoint

* Install Wazuh Agent

* Simulate attacks (Brute force, PowerShell abuse, etc.)

* Integrate Sysmon logs

* Create custom detection rules

* Build SOC alert triage workflow



## 📚 Skills Demonstrated

* SIEM Deployment

* Virtualization

* Linux System Administration

* Network Configuration

* Service Management (systemctl)

* SOC Architecture Understanding



## 🏁 Conclusion


### This lab successfully establishes a fully functional SIEM environment using Wazuh in a single-node configuration.


#### It provides the foundation for:

* Real-world security monitoring

* Threat detection practice

* Blue Team skill development

* SOC analyst preparation
