# Azure Live Traffic SOC & Honeynet Project
![Cloud Honeynet / SOC](https://i.imgur.com/6zgfR5R.png)

## Introduction

Within this project, I have developed a compact honeynet using Azure, where I integrate log sources from various origins into a dedicated Log Analytics workspace. This workspace serves as the foundation for Microsoft Sentinel, allowing the construction of attack maps, activation of alerts, and the generation of incidents. To assess the security aspects of the vulnerable environment, I gathered security metrics over a 24-hour period. After that, I implemented specific security controls to fortify the environment and evaluated the metrics for an additional 24 hours. The findings are presented below with the following metrics:

1. SecurityEvent - Windows Event Logs
2. Syslog - Linux Event Logs
3. SecurityAlert - Log Analytics Alerts Triggered
4. SecurityIncident - Incidents generated by Sentinel
5. AzureNetworkAnalytics_CL - Identified Malicious Flows permitted into our honeynet.

The architecture of the mini honeynet in Azure has the following components:

1. Virtual Network (VNet)
2. Network Security Group (NSG)
3. Virtual Machines (2 Windows, 1 Linux)
4. Log Analytics Workspace
5. Azure Key Vault
6. Azure Storage Account
7. Microsoft Sentinel

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/j9rsRIH.png)

Initially, for the "BEFORE" metrics, all resources were deployed and directly exposed to the internet. Both Virtual Machines had unrestricted Network Security Groups and open built-in firewalls, while other resources were set up with public endpoints, lacking the utilization of Private Endpoints.

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/iMhHSHA.png)

In contrast, for the "AFTER" metrics, significant enhancements were implemented. The Network Security Groups were fortified by blocking ALL traffic except for that originating from my admin workstation. Additionally, all other resources were fortified with their respective built-in firewalls and were safeguarded through the use of Private Endpoints.

## Attack Maps Before Hardening / Security Controls
![NSG Allowed Inbound Malicious Flows](https://i.imgur.com/XjOmjl9.jpg)<br> <br>
![Windows RDP/SMB Auth Failures](https://i.imgur.com/V5r4Vst.jpg)<br> <br>
![Linux Syslog Auth Failures](https://i.imgur.com/KEMHHmO.jpg) <br>

## Metrics Before Hardening / Security Controls

During a 24-hour period in our insecure environment, we gathered the following metrics:

- Start Time: 2023-07-12 08:51:28
- Stop Time: 2023-07-13 08:51:28

| Metric                   | Count |
| ------------------------ | ----- |
| SecurityEvent            | 3186  |
| Syslog                   | 967   |
| SecurityAlert            | 1     |
| SecurityIncident         | 253   |
| AzureNetworkAnalytics_CL | 1094  |

These metrics reflect the data we collected while exploring the vulnerable environment over the span of a day.

## Attack Maps After Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

Below is the information detailing the metrics obtained from our environment for another 24-hour duration, but this time after implementing security controls:

- Start Time: 2023-07-18 08:37:38
- Stop Time: 2023-07-19 08:37:38

| Metric                   | Count |
| ------------------------ | ----- |
| SecurityEvent            | 658   |
| Syslog                   | 0     |
| SecurityAlert            | 0     |
| SecurityIncident         | 0     |
| AzureNetworkAnalytics_CL | 0     |

## Conclusion

Throughout this project, we successfully built a mini honeynet in Microsoft Azure and seamlessly integrated log sources into a Log Analytics workspace. Employing Microsoft Sentinel allowed us to promptly activate alerts and generate incidents based on the collected logs. We meticulously assessed the metrics within the insecure environment prior to implementing security controls, and then once more after applying the necessary measures. The results showcased a remarkable reduction in security events and incidents following the implementation of these security controls, affirming their effectiveness.

It is essential to recognize that if the network resources were extensively used by regular users, it is plausible that more security events and alerts might have been triggered during the 24-hour period following the security control implementation.<br>
