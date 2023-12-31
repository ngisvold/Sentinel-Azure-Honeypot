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
<img src="https://nathangisvold.com/static/img/siem/4_Connect-Data-Log.png" height="50%" width="50%" alt="Connect Data Log"/>
</p>

<h3>Integrating Azure Sentinel:</h3>

1. Add Azure Sentinel to the Workspace:
- Navigate to your previously created Log Analytics Workspace in Azure.
- From within the workspace, select Azure Sentinel.
- Click on the Add button to integrate Azure Sentinel with the workspace, enabling it to ingest and analyze the collected data.

  <p align="center">
<img src="https://nathangisvold.com/static/img/siem/5_Create-Sentinel.png" height="80%" width="80%" alt="All Events"/>
</p>

<h3>Simulating RDP Attack & Gathering Location Data:</h3>

1. Simulate a Failed RDP Logon:

- Log into the configured VM.
- Intentionally use an incorrect password for login. This will generate a failed RDP logon event that will appear in the Windows Event Viewer's Security Logs.

2. Install and Configure the PowerShell Script:

- Download and use the provided PowerShell script from this repository. This script is designed to extract information from the Windows Event Log related to failed RDP attacks.
 -  <a href='https://github.com/ngisvold/Sentinel-Azure-RDP-Attack/blob/main/Security_Log_Exporter.ps1'>Security_Log_Exporter.ps1</a>
 
-  Additionally, the script interfaces with a third-party API to retrieve geographical information pertaining to the attacker's location.

3. API Key Acquisition & Configuration:

- Obtain an API key for the IP address-to-geolocation service from IPGeolocation.
- IP Address to Geolocation API - https://ipgeolocation.io 
- Configure the PowerShell script with the obtained API key, which allows Azure Sentinel to visualize the source locations of the attacks.
  
4. Execute the PowerShell Script:

- Run the Security_Log_Exporter.ps1 script.
- After execution, a log file will be generated and stored at C:\ProgramData

5. Log File Management:

- Copy the generated log file and create a new one.
- Navigate to the Log Analytics workspace in Azure.
- Upload the new log file to the workspace and designate it as a custom log.

<h3>Extracting & Visualizing Attack Data:</h3>

1. Data Extraction:

- Once you've added the custom log to Azure, you'll now need to extract pertinent data like the location and IP.
- To achieve this, navigate to the workbook in Azure Sentinel where you intend to visualize the map.

2. Insert the Extraction Script:

- Paste the following Kusto Query Language (KQL) script to extract and structure the desired data from the logs:

```        
FAILED_RDP_WITH_GEO_CL 
| extend username = extract(@"username:([^,]+)", 1, RawData),
         timestamp = extract(@"timestamp:([^,]+)", 1, RawData),
         latitude = extract(@"latitude:([^,]+)", 1, RawData),
         longitude = extract(@"longitude:([^,]+)", 1, RawData),
         sourcehost = extract(@"sourcehost:([^,]+)", 1, RawData),
         state = extract(@"state:([^,]+)", 1, RawData),
         label = extract(@"label:([^,]+)", 1, RawData),
         destination = extract(@"destinationhost:([^,]+)", 1, RawData),
         country = extract(@"country:([^,]+)", 1, RawData)
| where destination != "samplehost"
| where sourcehost != ""
| summarize event_count=count() by latitude, longitude, sourcehost, label, destination, country
```

1. Visualization:
- After executing the script, Azure Sentinel's workbook will process the data and plot it on a map.
- You can now view and analyze the geographically pinpointed RDP attack attempts directly within Sentinel's visualization tools.

<p align="center">
<img src="https://nathangisvold.com/static/img/siem/AttackMap.png" height="80%" width="80%" alt="Firewall *"/>
</p>
