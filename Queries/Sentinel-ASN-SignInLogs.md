# IOC - ASN Cloud Providers - AzureAD Signin Logs

---

## Query

```Kusto
let List = (externaldata(Netblock:string, Company:string, Count:int) [@"https://raw.githubusercontent.com/KustoKing/SentinelWatchlists/main/ASN-of-CloudProviders.csv"] with (ignoreFirstRecord=true, format="SCsv"));
SigninLogs
| where ResultType in(0, 50125, 50140, 70043, 70044)
| evaluate ipv4_lookup(List, IPAddress, Netblock)
| project-reorder TimeGenerated, Identity, UserPrincipalName, ClientAppUsed, AppDisplayName, IPAddress, Company, DeviceDetail
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
| Discovery |  |  |
| Lateral movement |  |  |
| Collection |  |  |
| Command and control |  |  |
| Exfiltration |  |  |
| Impact |  |  |
| Vulnerability |  |  |
| Misconfiguration |  |  |
| Malware, component |  |  |

## See also



## Contributor info

**Contributor:** 
**Contact info:** [Gianni](https://twitter.com/castello_johnny)

