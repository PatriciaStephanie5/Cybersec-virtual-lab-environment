# Building a Virtual Cybersecurity Lab Environment

## Objective
The objective of this project was to design, deploy, and configure an isolated virtual cybersecurity home lab environment using Oracle VM VirtualBox. The lab consists of an attacker platform (Kali Linux) and a target platform (Windows 10) configured on a dedicated virtual network to enable safe penetration testing, traffic analysis, and vulnerability assessment exercises.

---

## Technical Architecture & Specifications

* **Hypervisor:** Oracle VM VirtualBox & VirtualBox Extension Pack
* **Host Operating System:** Windows 11
* **Attacker Node (Guest):** Kali Linux (2026.2)
* **Target Node (Guest):** Windows 10 Pro (22H2)
* **Networking Mode:** Internal / NAT Network (Isolated Subnet)

---

## Implementation Steps

### Step 1: Hypervisor Setup & Extension Pack Installation
1. Downloaded and installed Oracle VM VirtualBox hypervisor on the Windows 11 host system.
2. Installed the matching **Oracle VM VirtualBox Extension Pack** to enable enhanced system features including USB 2.0/3.0 device support, VirtualBox Remote Desktop Protocol (VRDP), and disk encryption.
 

---

### Step 2: Windows 10 Target VM Deployment
1. Downloaded the official Windows 10 22H2 ISO via Microsoft's Media Creation Tool.
2. Created a new Virtual Machine with hardware parameters optimized for stability (4 GB RAM, 2 vCPUs, 50 GB Virtual Hard Disk).
3. Booted from the ISO, formatted the virtual storage drive, completed the Windows Out-of-Box Experience (OOBE) setup, and verified initial desktop login.


---

### Step 3: Kali Linux Attacker VM Deployment
1. Downloaded the official Kali Linux VirtualBox image / ISO.
2. Provisioned a virtual machine instance allocated with system resources suitable for security tooling.
3. Booted into Kali Linux, set up account credentials, and validated shell access and core security suite installation.

---

### Step 4: Virtual Network Configuration
1. Created and assigned a virtual network adapter mode (NAT Network / Internal Network) to both the Kali Linux and Windows 10 VMs.
2. Verified that both host nodes operate on the same private virtual subnet and can communicate directly with each other while preventing unauthorized outbound traffic to the production local network.

### Step 5: Baseline Snapshot Creation
1. Powered down or paused both virtual machines following baseline deployment.
2. Took a clean state **Snapshot** for both the Kali Linux and Windows 10 virtual instances titled `Baseline - Clean Install`.

## Key Takeaways & Lab Concepts

### 1. How to Reset the Environment After Experiments
When conducting malware analysis, exploit development, or intrusive network scanning, system configurations and files become altered or compromised. To reset the environment:
* Power off the targeted VM.
* Select the machine in VirtualBox Manager and navigate to the **Snapshots** menu.
* Select the `Baseline - Clean Install` snapshot and click **Restore**.
* The VM will instantly revert to its exact pre-test clean state in seconds without requiring a full OS reinstallation.

### 2. Importance of Snapshots During Testing
* **Safe Sandbox Experimentation:** Allows destructive security testing (e.g., executing malware samples or aggressive misconfiguration tests) with zero permanent risk to the OS setup.
* **Point-in-Time Rollbacks:** Enables branching test scenarios by capturing state changes before and after applying specific defensive patches, firewall rules, or exploit payloads.

### 3. Virtual Networking
* Virtual networking abstracts physical network hardware into software-defined switches and adapters within the hypervisor.
* By placing both Kali Linux and Windows 10 on a dedicated virtual network adapter mode (such as Internal Network or NAT Network), both nodes can route packets to each other locally, enabling realistic attack-and-defense traffic simulation.

### 4. Lab Isolation
* **Host Protection:** Isolating the lab network ensures that security tools, port scans, and potential malware samples cannot escape into your host machine or your home/work physical network.
* **Containment:** Proper isolation prevents accidental traffic interception or network disruption on live external network devices.
