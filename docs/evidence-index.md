# Evidence Index

All screenshots are point-in-time evidence collected from an authorized personal Azure lab. Sensitive IP addresses and identifiers were obscured before publication.

| ID | File | What it demonstrates | Related risks |
|---:|---|---|---|
| 00 | [GRC lab resource inventory](../evidence/00-grc-lab-resource-inventory.png) | `GRC-Lab` resource group and six supporting resources | Scope |
| 01 | [Azure VM overview](../evidence/01-azure-vm-overview.png) | VM name, Windows Server edition, size, region, network, and public-IP association | R-01, R-03 |
| 02 | [OS and administrator configuration](../evidence/02-os-admin-configuration.png) | Windows image, computer name, administrator username, and update setting | R-02, R-03 |
| 03 | [Native RDP access](../evidence/03-native-rdp-access.png) | Public-IP destination, TCP/3389, and `azureadmin` access path | R-01, R-02 |
| 04 | [Public RDP exposure](../evidence/04-public-rdp-exposure.png) | NSG inbound RDP rule allowing source `Any` | R-01 |
| 05 | [RDP rule details](../evidence/05-rdp-rule-details.png) | Baseline rule parameters: source Any, TCP/3389, Allow | R-01 |
| 06 | [Local user validation](../evidence/06-local-user-validation.png) | Enabled `azureadmin` local account | R-02 |
| 07 | [Local administrator membership](../evidence/07-local-admin-membership.png) | `azureadmin` membership in local Administrators | R-02 |
| 08 | [Windows Update status](../evidence/08-windows-update-status.png) | No updates available at capture time, with automatic updates turned off | R-03 |
| 09 | [Monitoring alert gap](../evidence/09-monitoring-alert-gap.png) | Azure Monitor alerts and enhanced monitoring not configured | R-05 |
| 10 | [Local Security event log](../evidence/10-local-security-event-log.png) | Local Windows Security events exist | R-05 |
| 11 | [Windows Security status](../evidence/11-windows-security-status.png) | Tamper Protection and PUA blocking warning states | R-03 |
| 12 | [Defender recommendations](../evidence/12-defender-recommendations.png) | Subscription-level recommendations view containing the assessed VM | R-03, R-05 |
| 13 | [Subscription RBAC](../evidence/13-subscription-rbac.png) | One Owner assignment at the assessed subscription scope | R-04 |
| 14 | [RDP restricted after mitigation](../evidence/14-rdp-restricted-after.png) | Trusted IPv4 `/32`, source port `*`, TCP/3389, Allow | R-01 |

## Evidence interpretation notes

- A public IP alone does not establish internet exposure. Evidence 04 and 05 establish exposure because the NSG rule allowed TCP/3389 from `Any`.
- Evidence 08 does not prove the VM was missing a specific patch. It establishes a patch-management configuration concern because automatic updates were disabled.
- Evidence 10 confirms local event availability; evidence 09 establishes the separate centralized alerting gap.
- Evidence 12 is a subscription-level view. Only findings related to `GRC-WIN-VM01` are within assessment scope.
- Evidence 13 documents a lab governance risk, not an assertion that the Owner role is inherently unauthorized.

