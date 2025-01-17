# Azure-SOC-Honeynet-Live-Traffic


## Introduction
![image alt](https://github.com/richurross/Azure-SOC-Honeynet-Live-Traffic-/blob/3a87e787047bd4e10c6d9ea0718f6f7e2da9bc94/1.gif)


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

