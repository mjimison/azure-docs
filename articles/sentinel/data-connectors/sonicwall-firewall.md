---
title: "SonicWall Firewall connector for Microsoft Sentinel"
description: "Learn how to install the connector SonicWall Firewall to connect your data source to Microsoft Sentinel."
author: cwatson-cat
ms.topic: how-to
ms.date: 02/23/2023
ms.service: microsoft-sentinel
ms.author: cwatson
---

# SonicWall Firewall connector for Microsoft Sentinel

Common Event Format (CEF) is an industry standard format on top of Syslog messages, used by SonicWall to allow event interoperability among different platforms. By connecting your CEF logs to Microsoft Sentinel, you can take advantage of search & correlation, alerting, and threat intelligence enrichment for each log.

## Connector attributes

| Connector attribute | Description |
| --- | --- |
| **Log Analytics table(s)** | CommonSecurityLog (SonicWall)<br/> |
| **Data collection rules support** | [Workspace transform DCR](../../azure-monitor/logs/tutorial-workspace-transformations-portal.md) |
| **Supported by** | [SonicWall](https://www.sonicwall.com/support/) |

## Query samples

**All logs**
   ```kusto

CommonSecurityLog

   | where DeviceVendor == "SonicWall"

   | where DeviceProduct has_any ("firewall","TZ 670","TZ 600","TZ 600P","NSv 270","TZ 570","TZ 570W","TZ 570P","TZ 500","TZ 500W","TZ 270","TZ 270W","TZ 370W","TZ 470W","TZ 350W","TZ 350","TZ 370","TZ 470","TZ 300W","TZ 300P","TZ 300","TZ 400W","TZ 400","SOHO 250","SOHO 250W","NSa 2700","NSv 470","NSv 870","NSa 3700","NSa 2600","NSa 2650","NSa 3600","NSa 3650","NSa 4650","NSa 5650","NSa 5700","NSa 6650","NSa 9250","NSa 9450","NSa 9650","NSsp 12400","NSsp 12800","NSsp 15700","NSv 10","NSv 25","NSv 50","NSv 100","NSv 200","NSv 300","NSv 400","NSv 800","NSv 1600") 

   
   | sort by TimeGenerated
   ```

**Summarize by destination IP and port**
   ```kusto

CommonSecurityLog

   | where DeviceVendor == "SonicWall"

   | where DeviceProduct has_any ("firewall","TZ 670","TZ 600","TZ 600P","NSv 270","TZ 570","TZ 570W","TZ 570P","TZ 500","TZ 500W","TZ 270","TZ 270W","TZ 370W","TZ 470W","TZ 350W","TZ 350","TZ 370","TZ 470","TZ 300W","TZ 300P","TZ 300","TZ 400W","TZ 400","SOHO 250","SOHO 250W","NSa 2700","NSv 470","NSv 870","NSa 3700","NSa 2600","NSa 2650","NSa 3600","NSa 3650","NSa 4650","NSa 5650","NSa 5700","NSa 6650","NSa 9250","NSa 9450","NSa 9650","NSsp 12400","NSsp 12800","NSsp 15700","NSv 10","NSv 25","NSv 50","NSv 100","NSv 200","NSv 300","NSv 400","NSv 800","NSv 1600") 

            
   | summarize count() by DestinationIP, DestinationPort, TimeGenerated
            
   | sort by TimeGenerated
   ```

**Show all dropped traffic from the SonicWall Firewall**
   ```kusto

CommonSecurityLog

   | where DeviceVendor == "SonicWall"

   | where DeviceProduct has_any ("firewall","TZ 670","TZ 600","TZ 600P","NSv 270","TZ 570","TZ 570W","TZ 570P","TZ 500","TZ 500W","TZ 270","TZ 270W","TZ 370W","TZ 470W","TZ 350W","TZ 350","TZ 370","TZ 470","TZ 300W","TZ 300P","TZ 300","TZ 400W","TZ 400","SOHO 250","SOHO 250W","NSa 2700","NSv 470","NSv 870","NSa 3700","NSa 2600","NSa 2650","NSa 3600","NSa 3650","NSa 4650","NSa 5650","NSa 5700","NSa 6650","NSa 9250","NSa 9450","NSa 9650","NSsp 12400","NSsp 12800","NSsp 15700","NSv 10","NSv 25","NSv 50","NSv 100","NSv 200","NSv 300","NSv 400","NSv 800","NSv 1600") 
 
   | where AdditionalExtensions contains "fw_action='drop'"
   ```



## Vendor installation instructions

1. Linux Syslog agent configuration

Install and configure the Linux agent to collect your Common Event Format (CEF) Syslog messages and forward them to Microsoft Sentinel.

> Notice that the data from all regions will be stored in the selected workspace

1.1 Select or create a Linux machine

Select or create a Linux machine that Microsoft Sentinel will use as the proxy between your security solution and Microsoft Sentinel this machine can be on your on-prem environment, Azure or other clouds.

1.2 Install the CEF collector on the Linux machine

Install the Microsoft Monitoring Agent on your Linux machine and configure the machine to listen on the necessary port and forward messages to your Microsoft Sentinel workspace. The CEF collector collects CEF messages on port 514 TCP.

> 1. Make sure that you have Python on your machine using the following command: python -version.

> 2. You must have elevated permissions (sudo) on your machine.

   Run the following command to install and apply the CEF collector:

   sudo wget -O cef_installer.py https://raw.githubusercontent.com/Azure/Azure-Sentinel/master/DataConnectors/CEF/cef_installer.py&&sudo python cef_installer.py {0} {1}

2. Forward SonicWall Firewall Common Event Format (CEF) logs to Syslog agent

Set your SonicWall Firewall to send Syslog messages in CEF format to the proxy machine. Make sure you send the logs to port 514 TCP on the machine's IP address.

 Follow Instructions . Then Make sure you select local use 4 as the facility. Then select ArcSight as the Syslog format.

3. Validate connection

Follow the instructions to validate your connectivity:

Open Log Analytics to check if the logs are received using the CommonSecurityLog schema.

>It may take about 20 minutes until the connection streams data to your workspace.

If the logs are not received, run the following connectivity validation script:

> 1. Make sure that you have Python on your machine using the following command: python -version

>2. You must have elevated permissions (sudo) on your machine

   Run the following command to validate your connectivity:

   sudo wget -O cef_installer.py https://raw.githubusercontent.com/Azure/Azure-Sentinel/master/DataConnectors/CEF/cef_troubleshoot.py&&sudo python cef_troubleshoot.py  {0}

4. Secure your machine 

Make sure to configure the machine's security according to your organization's security policy


[Learn more >](https://aka.ms/SecureCEF)



## Next steps

For more information, go to the [related solution](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/sonicwall-inc.sonicwall-networksecurity-azure-sentinal?tab=Overview) in the Azure Marketplace.