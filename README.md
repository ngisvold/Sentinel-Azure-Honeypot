# Azure Sentinel Honeypot Monitoring Project

<p align="center">
<img src="https://nathangisvold.com/static/img/siem/AttackMap.png" height="80%" width="80%" alt="Firewall *"/>
</p>

<h2>🛡️Project Summary</h2>

Set up Azure Sentinel (SIEM) to actively monitor a virtual machine honeypot, capturing live RDP Brute Force attack data from global sources. This project leverages a custom PowerShell script to fetch the geo-location of attackers and dynamically plots them on the Azure Sentinel Map for real-time threat visualization.

<h3>Azure Sentinel Honeypot Project Steps:</h3>

1. Initialize VM: Begin by configuring the fundamental settings of the VM Windows 10/11 Image.

2. Intentionally Vulnerable Configuration: In a deliberate deviation from best cybersecurity practices, configure the VM to be as exposed as possible for the purpose of this experiment. This involves:

- Opening the network firewall to accept all incoming connections.
- Disabling the Windows VM Defender Firewall.

<p align="center">
<img src="https://nathangisvold.com/static/img/siem/firewall.jpg" height="80%" width="80%" alt="Firewall *"/>
</p>
  
*Warning: This atypical setup is intentionally designed to test the capabilities of Azure Sentinel SIEM and should not be replicated for production or sensitive environments.

<h3>Setting Up Log Analysis and Data Collection:</h3>

1. Establish a Log Analytics Workspace: Begin by creating a Log Analytics Workspace in Azure. This workspace will be crucial for ingesting logs using Sentinel.

<p align="center">
<img src="https://nathangisvold.com/static/img/siem/2_log-analytics.png" height="80%" width="80%" alt="Log Analytics Workspace"/>
</p>

2. Configure Microsoft Defender for Cloud:

- Navigate to Microsoft Defender for Cloud within Azure.
- Access the Environment Settings and ensure that only the "Servers" option is enabled.
- Proceed to the Data Collection section. Here, select "All Events" specific to the vulnerable VM we configured earlier.

<p align="center">
<img src="https://nathangisvold.com/static/img/siem/3_Data-Collection.png" height="80%" width="80%" alt="All Events"/>
</p>

- Connect the Data Log to the Workspace.

<p align="center">
<img src="https://nathangisvold.com/static/img/siem/4_Connect-Data_log.png" height="80%" width="80%" alt="All Events"/>
</p>

<h3>Integrating Azure Sentinel:</h3>

1. Add Azure Sentinel to the Workspace:
- Navigate to your previously created Log Analytics Workspace in Azure.
- From within the workspace, select Azure Sentinel.
- Click on the Add button to integrate Azure Sentinel with the workspace, enabling it to ingest and analyze the collected data.

  <p align="center">
<img src="https://nathangisvold.com/static/img/siem/5_Create-Sentinel.png" height="80%" width="80%" alt="All Events"/>
</p>

<h2>Powershell for VM</h2>

The Powershell script in this repository is responsible for parsing out Windows Event Log information for failed RDP attacks and using a third party API to collect geographic information about the attackers location.

The script is used in this project where I setup Azure Sentinel (SIEM) and connect it to a live virtual machine acting as a honey pot. We will observe live attacks (RDP Brute Force) from all around the world. I will use a custom PowerShell script to look up the attackers Geolocation information and plot it on an Azure Sentinel Map!

- PowerShell: Extract RDP failed logon logs from Windows Event Viewer - <a href='https://github.com/ngisvold/Sentinel-Azure-RDP-Attack/blob/main/Security_Log_Exporter.ps1'>Security_Log_Exporter.ps1</a>

<h2>API</h2>
- IP Address to Geolocation API - https://ipgeolocation.io 

<h4>Project Credits</h4>
Thank you Josh Madakor on YouTube for inspiring this project.
