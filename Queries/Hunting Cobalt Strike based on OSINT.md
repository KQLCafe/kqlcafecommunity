# Hunting Cobalt Strike based on OSINT

The high fidelity Cobalt Strike IPs are collected and all lists are automatically retrieved and parsed on a daily (24h) basis and the final result is pushed to this repository.You can hunt for any Cobalt strike IPs in your environment with the query below.

## Query

```Kusto
let MaliciousIPs = materialize (
    (externaldata(report:string)
    [@"https://raw.githubusercontent.com/drb-ra/C2IntelFeeds/master/feeds/IPC2s.csv"]
    with (format = "txt",ignoreFirstRecord=true))
    | extend report = parse_csv(report)
    | extend RemoteIP = tostring(report[0])
    | project RemoteIP);
union
(MaliciousIPs
| join (DeviceNetworkEvents) on RemoteIP)
| project Timestamp, DeviceName, RemoteIP,InitiatingProcessAccountUpn,InitiatingProcessCommandLine,InitiatingProcessFileName
```
## Category

This query can be used to detect the following attack techniques and tactics ([see MITRE ATT&CK framework](https://attack.mitre.org/)) or security configuration states.

| Technique, tactic, or state | Covered? (v=yes) | Notes |
|-|-|-|
| Initial access |  |  |
| Execution |  |  |
| Persistence |  |  |
| Privilege escalation | |  |
| Defense evasion |  |  |
| Credential Access |  |  |
| Discovery | v |  |
| Lateral movement |  |  |
| Collection |  |  |
| Command and control | v |  |
| Exfiltration |  |  |
| Impact |  |  |
| Vulnerability |  |  |
| Misconfiguration |  |  |
| Malware, component |  |  |

## See also



## Contributor info
Contributor: Shivam Malaviya
GitHub alias: Shivammalaviya
Organization: Open System
Contact info: Shivammalaviya@hotmail.com