# Azure Sentinel Honeypot Monitoring Project

<h2>🛡️Project Summary</h2>

Set up Azure Sentinel (SIEM) to actively monitor a virtual machine honeypot, capturing live RDP Brute Force attack data from global sources. This project leverages a custom PowerShell script to fetch the geo-location of attackers and dynamically plots them on the Azure Sentinel Map for real-time threat visualization.

<h3>Azure Sentinel Honeypot Project Steps:</h3>

1. Initialize VM: Begin by configuring the fundamental settings of the VM Windows 10/11 Image.

2. Intentionally Vulnerable Configuration: In a deliberate deviation from best cybersecurity practices, configure the VM to be as exposed as possible for the purpose of this experiment. This involves:

- Opening the network firewall to accept all incoming connections.
- Disabling the Windows VM Defender Firewall.

<p align="center">
<img src="https://nathangisvold.com/static/img/siem/AttackMap.png" height="85%" width="85%" alt="Firewall *"/>
</p>
  
*Warning: This atypical setup is intentionally designed to test the capabilities of Azure Sentinel SIEM and should not be replicated for production or sensitive environments.

<h2>Powershell for VM</h2>

The Powershell script in this repository is responsible for parsing out Windows Event Log information for failed RDP attacks and using a third party API to collect geographic information about the attackers location.

The script is used in this project where I setup Azure Sentinel (SIEM) and connect it to a live virtual machine acting as a honey pot. We will observe live attacks (RDP Brute Force) from all around the world. I will use a custom PowerShell script to look up the attackers Geolocation information and plot it on an Azure Sentinel Map!

- PowerShell: Extract RDP failed logon logs from Windows Event Viewer - <a href='https://github.com/ngisvold/Sentinel-Azure-RDP-Attack/blob/main/Security_Log_Exporter.ps1'>Security_Log_Exporter.ps1</a>

<h2>API</h2>
- IP Address to Geolocation API - https://ipgeolocation.io 

<h4>Project Credits</h4>
Thank you Josh Madakor on YouTube for inspiring this project.
