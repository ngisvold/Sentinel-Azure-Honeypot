# Azure Sentinel Honeypot Monitoring Project

<h2>🛡️Project Summary</h2>

Set up Azure Sentinel (SIEM) to actively monitor a virtual machine honeypot, capturing live RDP Brute Force attack data from global sources. This project leverages a custom PowerShell script to fetch the geo-location of attackers and dynamically plots them on the Azure Sentinel Map for real-time threat visualization.

<h2>Powershell for VM</h2>

The Powershell script in this repository is responsible for parsing out Windows Event Log information for failed RDP attacks and using a third party API to collect geographic information about the attackers location.

The script is used in this project where I setup Azure Sentinel (SIEM) and connect it to a live virtual machine acting as a honey pot. We will observe live attacks (RDP Brute Force) from all around the world. I will use a custom PowerShell script to look up the attackers Geolocation information and plot it on an Azure Sentinel Map!

- PowerShell: Extract RDP failed logon logs from Windows Event Viewer - <a href='https://github.com/ngisvold/Sentinel-Azure-RDP-Attack/blob/main/Security_Log_Exporter.ps1'>Security_Log_Exporter.ps1</a>

<h2>API</h2>
- IP Address to Geolocation API - https://ipgeolocation.io 

<h4>Project Credits</h4>
Thank you Josh Madakor on YouTube for inspiring this project.
