# Azure-SOC-Honeynet-Live-Traffic


## Introduction
![image alt](https://github.com/richurross/Azure-SOC-Honeynet-Live-Traffic-/blob/3a87e787047bd4e10c6d9ea0718f6f7e2da9bc94/1.gif)

This project involves the simulation of a mini honeynet and SOC within Azure. This environment is replicated through aggregated log data from various sources into a Log Analytics Workspace. Microsoft Sentinel then correlates this data to create attack maps, trigger custom alerts, and generate incident reports. Both an insecure and secure Azure environment are live for 24 hours to generate live attack traffic. A 24-hour assessment will take place where the two environments are statistically compared to measure the effectiveness of applied security controls and hardening. The measured statistics are contain the following:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)
  
## Project Stages
-_Honeynet Setup_: The intended targets I deployed were Linux and Windows virtual machines, as well as a public SQL server. The environment was made vulnerable by disabling the internal firewall, allowing all incoming ports and traffic, and settings weak user passwords. Afterwards, custom KQL queries were imported in order to trigger alerts for observation and remediation.

-_Observation and Analysis_: Logs from all vulnerable targets were aggregated into Microsoft Sentinel and Log Analytics Workspace for observation. Incoming traffic was analyzed to build comprehensive, geographical attack maps, precise alert triggering, and detailed incident reports.

-_Monitoring and Assessing Security Metrics_: The environment was left publicly live for 24 hours, allowing for anyone to leave behind traces of attacks. The environment was monitored for the above mentioned key security metrics, allowing for the establishment of a security baseline.

-_Resolving Security Issues_: By analyzing the insecure environment, I identified vulnerabilities and remediated Sentinel incidents according to severity level. Remediations and hardening were applied with best practices in mind from NIST SP 800-53 Rev 5 and NIST SP 800-61 Rev 2.

-_Post-Remediation Analysis_:  The envinroment was left live again for anothe 24 hours to review our key security metrics post-remediation and hardening. The new data was statistically weighed against the initial baseline for insightful comparative analysis.


## Architecture Before Hardening / Security Controls
![image alt](https://github.com/richurross/Azure-SOC-Honeynet-Live-Traffic-/blob/3a87e787047bd4e10c6d9ea0718f6f7e2da9bc94/2.gif)

## Architecture After Hardening / Security Controls
![image alt](https://github.com/richurross/Azure-SOC-Honeynet-Live-Traffic-/blob/3a87e787047bd4e10c6d9ea0718f6f7e2da9bc94/3.gif)


## Attack Maps Before Hardening / Security Controls

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2024-12-06T09:36:35
Stop Time 2024-12-07T09:36:35

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 15592
| Syslog                   | 14354
| SecurityAlert            | 6
| SecurityIncident         | 316
| AzureNetworkAnalytics_CL | 1217

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2024-12-10T08:57:05
Stop Time	2024-12-10T08:57:05

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 512
| Syslog                   | 8
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Change After Securing the Environment

| Metric                   | Count
| ------------------------ | -----
| Security Events (Windows VMs)            | -96.72%
| Syslog (Linux VMs)                   | -99.87%
| SecurityAlert (Microsoft Defender for Cloud)            | -100.00%
| SecurityIncident (Sentinel Incients)       | -100.00%
| NSG Inbound Malicious Flows Allowed | -100.00%

## Conclusion

