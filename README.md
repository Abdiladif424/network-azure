<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create a resource group and virtual machines
- Observe ICMP Traffic
- Configuring a Firewall (Network Security Group)
- Observing different types of network traffic

<h2>Actions and Observations</h2>

1. Create a resource group within Microsoft Azure

<img width="2559" height="1439" alt="Screenshot 2025-07-22 115455" src="https://github.com/user-attachments/assets/c5410b16-3ae4-41fa-9371-c15301840963" />

2. Create a Windows 10 and Linux Virtual Machine
- Make sure both VMs are on the same resource group and virtual network/subnet (the virtual network was created while creating Windows 10 VM because it was the first one that was done)

<img width="2559" height="1439" alt="Screenshot 2025-07-22 121437" src="https://github.com/user-attachments/assets/8d6b8e82-9d3a-4fc5-b794-9b4e0f093c53" />

3. Within your Windows 10 Virtual Machine, Install Wireshark

<img width="2559" height="1439" alt="Screenshot 2025-07-22 122723" src="https://github.com/user-attachments/assets/689ab102-0d10-45d0-981d-1c530d6bff89" />

4. Open Wireshark and start packet capture
- Within Wireshark, filter for ICMP traffic only
- Then, retrieve the private IP address of the Ubuntu VM (linux-vm) and attempt to ping it from within the Windows 10 VM 
- Observe ping requests and replies within Wireshark

<img width="2559" height="1439" alt="Screenshot 2025-07-22 130508" src="https://github.com/user-attachments/assets/16f64c57-f841-4629-8787-e5994b0c21fd" />

5. Open the Network Security Group your Ubuntu VM is using and disable incoming (inbound) ICMP traffic

<img width="2559" height="1439" alt="Screenshot 2025-07-22 130843" src="https://github.com/user-attachments/assets/1ef0a613-01a5-4766-b354-8c8bb530099f" />

6. Back in the Windows 10 VM, observe the ICMP traffic in Wireshark and the command-line Ping activity
- You will see that the ping request timed out because of the blocked ICMP traffic

<img width="2559" height="1439" alt="Screenshot 2025-07-22 131019" src="https://github.com/user-attachments/assets/f3f73d98-e236-4150-a7a7-ccaadde21436" />

7. Re-enable ICMP traffic for the Network Security Group that your Ubuntu VM is in
- Back in the Windows 10 VM, observe the ICMP traffic in Wireshark and the command line Ping activity (should start working)

<img width="2559" height="1439" alt="Screenshot 2025-07-22 131256" src="https://github.com/user-attachments/assets/75339873-2d3a-4375-8bbf-53403d04fbd5" />

8. Back in Wireshark, start a packet capture within the Windows 10 VM
- Filter for SSH traffic only
- Open PowerShell, and type: ssh labuser@<private IP address>
- This will allow you to log in to the Linux VM

 <img width="2559" height="1439" alt="Screenshot 2025-07-22 132627" src="https://github.com/user-attachments/assets/37ad1390-2c12-455b-8f1c-8d6eaf889f05" />

9. Back in Wireshark, filter for DNS traffic only
- From your Windows 10 VM within a command line, use nslookup to see what Disney.com’s IP addresses are, for example
- Observe the DNS traffic being shown in Wireshark

<img width="2559" height="1439" alt="Screenshot 2025-07-22 134626" src="https://github.com/user-attachments/assets/79ff40f0-213a-437f-bce9-7219e576ce08" />

10. Back in Wireshark, filter for RDP traffic only (tcp.port == 3389)
- Observe the immediate non-stop spam of traffic
- However, there is non-stop spamming traffic instead of only showing traffic when you do an activity.
- This is because the RDP (protocol) is constantly showing you a live stream from one computer to another; therefore, traffic is always being transmitted

<img width="2559" height="1439" alt="Screenshot 2025-07-22 135211" src="https://github.com/user-attachments/assets/580bef39-a846-4460-b140-eb71577fe943" />











