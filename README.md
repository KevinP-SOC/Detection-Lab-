# SOC Detection Lab-

## Objective

The SOC Detection Lab was created to build a safe, virtualized environment for simulating cyber attacks and practicing defensive monitoring techniques. The project focused on configuring Windows 10 and Kali Linux virtual machines, generating malicious and suspicious activity, and collecting telemetry with Sysmon and Splunk. The goal was to understand how attacks appear in logs, develop detection strategies, and strengthen practical SOC analyst skills.

### Skills Learned

- Gained practical experience configuring and managing a virtualized SOC environment in VirtualBox.
- Installed and tuned Sysmon to capture detailed Windows telemetry for security monitoring.
- Ingested, parsed, and analyzed logs in Splunk, applying SIEM concepts to real-world scenarios.
- Practiced interpreting event logs to identify Indicators of Compromise (IoCs), attack patterns, and signatures.
- Strengthened understanding of network protocols, vulnerabilities, and adversary behaviors through simulated attacks.
- Developed detection queries and alerts to monitor suspicious activity.
- Improved critical thinking and problem-solving skills while investigating simulated incidents.

### Tools Used

- VirtualBox – virtualization platform for lab setup.
- Windows 10 + Sysmon – endpoint telemetry generation.
- Splunk – SIEM for log ingestion, search, and analysis.
- Kali Linux – attacker machine (Nmap, Metasploit, reverse shell payloads).
- Wireshark – optional packet analysis for network visibility.

## Steps
The following steps document how I built and configured a secure home lab environment using VirtualBox.  
This lab was designed to safely test tools, simulate attacks, and generate telemetry for analysis within a SIEM.  

Step 1: Download Windows 10 ISO

Downloaded the official Windows 10 installation media to prepare the Windows VM for VirtualBox.
Ref 1: Windows 10 Media Creation Tool


Step 2: Download and Verify VirtualBox

Downloaded VirtualBox for Windows, then verified the installer integrity by comparing SHA-256 hashes. This ensured the file was not tampered with.
Ref 2: VirtualBox Hash Verification




Step 3: Install VirtualBox

Installed Oracle VirtualBox 7.2.0 on the host system, preparing the environment for VM deployment.
Ref 3: VirtualBox Installer


Step 4: Download Kali Linux VM

Downloaded the pre-built Kali Linux VirtualBox image from the official Kali website for attacker machine setup.
Ref 4: Kali VM Download


Step 5: Create Windows and Kali Virtual Machines

Used the Windows 10 ISO to create a Windows VM.

Imported the Kali Linux .vbox file for the attacker VM.

Configured both in VirtualBox and confirmed proper installation.
Ref 5: VirtualBox VM Setup


Step 6: Configure Networking (Internal Network Mode)

Adjusted VM settings to Internal Network, isolating both VMs from the internet to ensure safe malware testing and attack simulation.
Ref 6: VirtualBox Network Settings


Step 7: Assign Static IPs

Manually assigned IP addresses to each VM so they could communicate directly:

Windows VM: 192.168.20.10

Kali VM: 192.168.20.11

Ref 7: Kali IP Configuration




Step 8: Verify Connectivity

Confirmed that the Windows and Kali VMs were successfully communicating by pinging between machines.
Ref 8: Network Verification
