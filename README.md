# Failed RDP Lookup IP Geolocation Information

<h2>🛡️</h2>

The Powershell script in this repository is responsible for parsing out Windows Event Log information for failed RDP attacks and using a third party API to collect geographic information about the attackers location.

The script is used in this project where I setup Azure Sentinel (SIEM) and connect it to a live virtual machine acting as a honey pot. We will observe live attacks (RDP Brute Force) from all around the world. I will use a custom PowerShell script to look up the attackers Geolocation information and plot it on an Azure Sentinel Map!


<h2>Languages</h2>
- PowerShell: Extract RDP failed logon logs from Windows Event Viewer - <a href='https://github.com/ngisvold/Sentinel-Azure-RDP-Attack/blob/main/Security_Log_Exporter.ps1'>Security_Log_Exporter.ps1</a>

<h2>API</h2>
- IP Address to Geolocation API - https://ipgeolocation.io 
