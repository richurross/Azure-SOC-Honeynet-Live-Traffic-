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
- _Honeynet Setup_: The intended targets I deployed were Linux and Windows virtual machines, as well as a public SQL server. The environment was made vulnerable by disabling the internal firewall, allowing all incoming ports and traffic, and settings weak user passwords. Afterwards, custom KQL queries were imported in order to trigger alerts for observation and remediation.

- _Observation and Analysis_: Logs from all vulnerable targets were aggregated into Microsoft Sentinel and Log Analytics Workspace for observation. Incoming traffic was analyzed to build comprehensive, geographical attack maps, precise alert triggering, and detailed incident reports.

- _Monitoring and Assessing Security Metrics_: The environment was left publicly live for 24 hours, allowing for anyone to leave behind traces of attacks. The environment was monitored for the above mentioned key security metrics, allowing for the establishment of a security baseline.

- _Resolving Security Issues_: By analyzing the insecure environment, I identified vulnerabilities and remediated Sentinel incidents according to severity level. Remediations and hardening were applied with best practices in mind from NIST SP 800-53 Rev 5 and NIST SP 800-61 Rev 2.

- _Post-Remediation Analysis_:  The envinroment was left live again for anothe 24 hours to review our key security metrics post-remediation and hardening. The new data was statistically weighed against the initial baseline for insightful comparative analysis.


## Architecture Before Hardening / Security Controls
![image alt](https://github.com/richurross/Azure-SOC-Honeynet-Live-Traffic-/blob/3a87e787047bd4e10c6d9ea0718f6f7e2da9bc94/2.gif)

The initial deployment of resources and VM's were configured to have disabled security features. This includes configuration of the Network Security Groups (NSG's) to allow all incoming traffic and ports, disabling default firewalls, and making public endpoints visible to the internet.

## Architecture After Hardening / Security Controls
![image alt](https://github.com/richurross/Azure-SOC-Honeynet-Live-Traffic-/blob/3a87e787047bd4e10c6d9ea0718f6f7e2da9bc94/3.gif)

After a 24-hour insecure assessment, I reinforced the security controls for the environment. This includes configuration the NSG's to only allow traffic from my private IP, re-enabling of the firewall, and utilization of private endpoints.

## Attack Maps Before Hardening / Security Controls

The attack map portrayed below details an overview of malicious attack attempts targeted at a publicly exposed Microsoft SQL server over a 24-hour period. The map highlights the precise geographic locations wherein said attacks or login attempts originated.

![image alt](https://github.com/richurross/Azure-SOC-Honeynet-Live-Traffic-/blob/c8dcadcc0edbefad6a61eb75e91a45e6868ce1ac/MSSQL%20Auth%20Fail%20Map.png)

The attack map portrayed below depicts numerous failed syslog authentication attemps of my Linux server. The map features unauthorized access attempts originating from sources external to the local network as the server was publicly exposed to the internet. The graphic accentuates the urgency of security hardening, robust identity and access management, and system log monitoring for detecting and preventing potentail breaches.

![image alt](https://github.com/richurross/Azure-SOC-Honeynet-Live-Traffic-/blob/c8dcadcc0edbefad6a61eb75e91a45e6868ce1ac/Linux%20SSH%20Auth%20Fail%20Map.png)

The attack map portrayed below highlights the number of attacks attempts after intentionally leaving my VM's Network Security Groups (NSG's) vulnerable and open to all traffic. This permits unchecked malicious network traffic and emphasizes how easily an attacker may discover a weak, exposed network. The graphic reminds us that NSG's and security rules are mandatory for minimizing the overall attack surface of a network.

![image alt](https://github.com/richurross/Azure-SOC-Honeynet-Live-Traffic-/blob/c8dcadcc0edbefad6a61eb75e91a45e6868ce1ac/NSG%20Malicious%20Flow%20Map.png)

The attack map portrayed below showcases various failed, unauthorized access attempts utilizing Remote Desktop Protocol (RDP) and Server Message Block (SMB) methods against my publicly exposed Windows machine. RDP, utilized for remote access, and SMB, utilized for file-sharing services, are typical networking protocols utilized by malicious entities to gain remote access to a network. As such, this map demonstrates the criticality in which we must preemptively secure these communication channels to prevent unauthorized access of sensitive data and davices.

![image alt](https://github.com/richurross/Azure-SOC-Honeynet-Live-Traffic-/blob/c8dcadcc0edbefad6a61eb75e91a45e6868ce1ac/Windows%20RDP%20Auth%20Fail%20Map.png)

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

## Attack Maps After Hardening / Security Controls

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

For this homelab project, I established a small honeynet on Microsoft Azure and integrated several log sources into a designated Log Analytics workspace. Microsoft Sentinel was used to generate alerts and create incidents based on the collected log data. Metrics were carefully monitored in the unsecured environment before implementing security measures, and then reassessed after the controls were in place. The results demonstrated a clear and substantial reduction in security events and incidents, confirming the positive impact of the applied security measures.

Additionally, it is important to consider that if the network’s resources had been more actively utilized by regular users, the number of security events and alerts could have been higher within the 24 hours after the security controls were applied.
