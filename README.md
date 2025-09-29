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

- **VirtualBox** – virtualization platform for lab setup.
- **Windows 10** + Sysmon – endpoint telemetry generation.
- **Kali Linux** – attacker machine (Nmap, Metasploit, reverse shell payloads).
- **Splunk** – SIEM for log ingestion, search, and analysis.
- **Wireshark** – optional packet analysis for network visibility.
- **Sysmon** – provided detailed system and process logging.

## Video Walkthrough
  **Full end-to-end video walkthrough: `[Video Link Here soon]`.**
  
## Steps
The following steps document how I built and configured a secure home lab environment using VirtualBox.  
This lab was designed to safely test tools, simulate attacks, and generate telemetry for analysis within a SIEM. 

1) **Download Windows 10 ISO**  
<img width="640" height="640" alt="1" src="https://github.com/user-attachments/assets/725eb126-de0b-4b0f-b3c6-94411dfbc284" />
<img width="640" height="640" alt="1 1" src="https://github.com/user-attachments/assets/89582e0e-1f48-4e3f-88aa-155539f6b299" />

*Ref 1:* Grab the official Windows 10 installation media to use as the VM installer.

2) **Download & Verify VirtualBox**  
 <img width="640" height="640" alt="2" src="https://github.com/user-attachments/assets/f209f4e8-d5ed-49cf-a4dd-edb75a10d002" />
<img width="640" height="640" alt="3" src="https://github.com/user-attachments/assets/2f16dbf2-f9f7-4346-bd59-e415f2ea393a" />
<img width="640" height="640" alt="4" src="https://github.com/user-attachments/assets/ead9c876-3e4f-41b4-86bb-e80db79e4fce" />

*Ref 2:* Download VirtualBox for Windows, then verify the installer hash matches the vendor’s published hash to confirm integrity.

3) **Install VirtualBox**  
<img width="640" height="640" alt="5" src="https://github.com/user-attachments/assets/77aa15b3-be49-4b25-a34e-f8d680b48cbe" />
 
*Ref 3:* Run the VirtualBox installer with default options and confirm the application launches.

4) **Create Windows 10 VM (attach ISO)**  
<img width="640" height="640" alt="6" src="https://github.com/user-attachments/assets/7eaf520d-683c-4bbc-a175-749c71b9b2fb" />

*Ref 4:* Create a new VM in VirtualBox and attach the Windows 10 ISO as the startup disk.

5) **Create Kali Linux VM**  
<img width="640" height="640" alt="8" src="https://github.com/user-attachments/assets/79f36981-d5d2-4125-953b-9127ac78701f" />
*Ref 5:* Create a Kali Linux VM following the same steps as previous.


6) **Isolate Both VMs on an Internal Network**  
<img width="640" height="640" alt="6" src="https://github.com/user-attachments/assets/86bb7042-b847-4148-88e7-78e16275e795" />

*Ref 6:* In each VM’s Network settings, select **Internal Network** so the machines can talk to each other but not the internet/host.

7) **Assign Static IP in Kali**  
 <img width="640" height="695" alt="10" src="https://github.com/user-attachments/assets/4265c7c0-0390-4059-9411-2d5cebbd7069" />
<img width="640" height="640" alt="11" src="https://github.com/user-attachments/assets/b4366061-8c1c-43b9-b912-29507f46a47b" />
*Ref 7:* In Kali → Wired Connection → IPv4, assign a static IP in your chosen subnet (e.g., `192.168.20.0/24`).

8) **Assign Static IP in Windows**  
<img width="640" height="640" alt="12" src="https://github.com/user-attachments/assets/f2e3aadd-c2d4-4eca-b7df-4e0d232cbfd0" />
<img width="640" height="640" alt="13" src="https://github.com/user-attachments/assets/e6f21d87-5db8-4c92-9a5e-cc5cf9d4aaf6" />
*Ref 8:* Windows → Settings → Network & Internet → Change adapter options → Ethernet → Properties → IPv4 → Properties, set a static IP in the same subnet.

9) **Verify Connectivity with Ping (Both Directions)**  
<img width="640" height="640" alt="14" src="https://github.com/user-attachments/assets/78fc90c8-6e5e-4ab2-8adc-0cb262b3a7d8" />

*Ref 9:* From Windows, ping Kali; from Kali, ping Windows. Confirm both succeed to verify internal connectivity.

10) **Enable Remote Desktop on Windows**  
  
*Ref 10:* Turn on **Remote Desktop** in Windows settings; port **3389** will be listening internally.

11) **Recon from Kali with Nmap**  
<img width="640" height="640" alt="15" src="https://github.com/user-attachments/assets/66d41464-eb01-419f-8b76-874adb1cad45" />

*Ref 11:* Run `nmap -A 192.168.20.10 -Pn` against the Windows host; confirm **3389/tcp open** (RDP) is detected.

12) **Build Payload with msfvenom**  
<img width="640" height="640" alt="16" src="https://github.com/user-attachments/assets/618a2aee-155a-4b6a-a72f-59432892a7f8" />

*Ref 12:* Use `msfvenom -l payloads` to choose a payload, then generate it (include the exact command and the “payload created” output).

13) **Start Metasploit Handler & Host the Payload**  
 <img width="640" height="640" alt="17" src="https://github.com/user-attachments/assets/b2e2cac8-1717-4904-bf16-fcd37369144b" />
 <img width="640" height="640" alt="18" src="https://github.com/user-attachments/assets/afc1fc04-92e4-4c58-a84e-1ebbd1f8d199" />

*Ref 13:* Configure the Metasploit handler for the payload and start a simple Python HTTP server in Kali so Windows can download the file.

14) **(Lab-Only) Disable Defender & Download Payload on Windows**  
<img width="640" height="640" alt="19" src="https://github.com/user-attachments/assets/3439e44d-06e9-4813-b280-e044d04e5aad" />
 <img width="640" height="640" alt="20" src="https://github.com/user-attachments/assets/ef7fb70f-36d5-401c-a189-0a9bf26add29" />
<img width="640" height="640" alt="21" src="https://github.com/user-attachments/assets/7b3aafee-489e-4844-a638-df3315ba0c43" />

*Ref 14:* Temporarily disable Windows Defender (lab only), browse to Kali’s `IP:PORT`, download the payload, acknowledge the browser warning, and run it.

15) **Confirm Callback (Windows ↔ Kali)**
<img width="640" height="640" alt="22" src="https://github.com/user-attachments/assets/f80a01b8-2347-4857-95b6-346cad516512" />
<img width="640" height="640" alt="23" src="https://github.com/user-attachments/assets/d3a5181d-f987-438d-b90f-6c21ac19d15a" />
<img width="640" height="640" alt="25" src="https://github.com/user-attachments/assets/64e2817b-2199-4d81-87ca-a7b62aa3333c" />
<img width="640" height="640" alt="24" src="https://github.com/user-attachments/assets/9b59ada1-6d1f-4e12-b56b-3d18000daec3" />

*Ref 15:* On Windows, show `netstat -ano` and the matching PID in Task Manager; on Kali, show the Metasploit handler receiving the session and an interactive shell.

16) **Post-Exploitation Basics (Enumeration)**  
 <img width="640" height="640" alt="26" src="https://github.com/user-attachments/assets/1937c826-2e04-48bc-a638-470e09535f1a" />

*Ref 16:* Run basic enumeration (e.g., `whoa

17) **Ensure Sysmon + Splunk Ingestion**  
<img width="640" height="640" alt="27" src="https://github.com/user-attachments/assets/11457ced-1e88-4190-9a45-d9ec38fe7fec" />
<img width="640" height="640" alt="28" src="https://github.com/user-attachments/assets/8ede1e0a-7d80-468d-ae75-10a540455129" />
<img width="640" height="640" alt="29" src="https://github.com/user-attachments/assets/a6a24d25-8794-4264-834a-910cadfebb93" />
<img width="640" height="640" alt="30" src="https://github.com/user-attachments/assets/743b1794-86f2-4048-a049-ef26c066d52f" />

*Ref 17:* Confirm Sysmon is installed on Windows and Splunk is running. Create the **endpoint** index (matching your inputs config) and verify events are being ingested.

18) **Hunt in Splunk: IP, Ports, Process Trees**  
<img width="640" height="640" alt="31" src="https://github.com/user-attachments/assets/c2831fa8-8dfe-4c64-84aa-3a788c53897e" />
<img width="640" height="640" alt="32" src="https://github.com/user-attachments/assets/ad52806c-1fc6-4184-9560-333eb8fe04f7" />
<img width="640" height="640" alt="33" src="https://github.com/user-attachments/assets/c210aa08-e7b2-41f4-90e1-0195642d387d" />
<img width="640" height="640" alt="34" src="https://github.com/user-attachments/assets/14b451cf-ca7e-4b91-b9c2-b74f9fa138eb" />
<img width="640" height="640" alt="35" src="https://github.com/user-attachments/assets/d23ed986-9da5-45a3-91a5-0f86188613fd" />

*Ref 18:*  
- Query Kali’s IP: `index=endpoint 192.168.20.12` and review `dest_port` activity.  
- Investigate **EventCode=1** (process creation) to see parent/child relationships.  
- Pivot using **ProcessGuid** to reconstruct the process tree and commands executed by the payload.  
- (Optional) Clean up SPL and add a small table/chart for clarity.

