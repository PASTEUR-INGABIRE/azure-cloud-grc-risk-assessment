# Cloud Security Risk Assessment Report

**Project:** Cybersecurity Project: Cloud Security Risk Assessment & GRC Simulation (Azure)  
**Assessor:** PASTEUR INGABIRE  
**Assessment type:** Point-in-time, non-exploitative GRC simulation  
**Environment:** Microsoft Azure personal lab  

## 1. Executive summary

This report documents a cloud security risk assessment of one Azure-hosted Windows Server virtual machine. The assessment evaluated remote access, local administrative privileges, endpoint configuration, patch management, logging, monitoring, Defender recommendations, and subscription-level authorization.

Five risks were recorded: four High and one Medium. The most significant finding was an NSG rule permitting inbound RDP from any source. A compensating control was implemented by restricting the rule to a trusted IPv4 `/32`, reducing the assessed score from 16 to 8. The environment retains material residual risk because RDP remains reachable over a public IP and the remaining recommended controls were not implemented during this simulation.

Overall inherent risk posture: **Medium-High**.  
Current overall posture after the validated RDP restriction: **Medium-High**, because other High risks remain untreated. The target residual posture is **Medium** after completing the planned identity, monitoring, endpoint-hardening, patch, and RBAC actions.

## 2. Scope and environment

### In scope

- `GRC-Lab` resource group and resources supporting `GRC-WIN-VM01`
- Windows Server 2022 Datacenter: Azure Edition VM
- Public IP, NIC, VNet/subnet, and NSG
- Native RDP access on TCP/3389
- Local administrator identity and group membership
- Windows Update and Windows Security posture
- Local Windows Security event logs
- Azure Monitor alert posture
- Defender for Cloud recommendation context
- Subscription RBAC relevant to administrative control

### Out of scope

- Exploitation, password attacks, or vulnerability scanning
- Business applications, production data, and data classification
- Formal regulatory audit or control effectiveness attestation
- Resources unrelated to the assessed VM

## 3. Asset inventory

| Category | Asset | Security relevance |
|---|---|---|
| Compute | `GRC-WIN-VM01` | Hosts the Windows operating system and services |
| Network | Public IP | Provides an internet-routable address |
| Network | Network Security Group | Controls permitted inbound and outbound flows |
| Network | NIC and virtual network | Connect the VM to the Azure network |
| Identity | Local `azureadmin` account | Provides full local administrative control |
| Cloud authorization | Azure subscription Owner role | Grants broad management and access-assignment capability |
| Logging | Windows Security event log | Provides local security telemetry |
| Monitoring | Azure Monitor / Defender for Cloud | Provides centralized visibility, recommendations, and alerting capability |

## 4. Threat and vulnerability summary

| Asset | Threat scenario | Observed weakness | Business impact |
|---|---|---|---|
| RDP service | Password spraying or brute force | TCP/3389 initially allowed from any source | Unauthorized access, service disruption, or initial foothold |
| Local administrator | Credential theft or reuse | Enabled account with local Administrators membership; MFA not demonstrated for this path | Full VM control and loss of confidentiality, integrity, or availability |
| Windows OS | Exploitation or security control tampering | Automatic updates turned off; Tamper Protection and PUA blocking shown disabled | Greater likelihood of compromise or defense impairment |
| Subscription authorization | Privilege misuse or account compromise | One account has Owner at subscription scope | High-impact changes across subscription resources |
| Logs and monitoring | Undetected malicious activity | Local logs exist, but Azure alerts and enhanced monitoring were not configured | Delayed detection, triage, containment, and evidence collection |

## 5. Risk assessment

Likelihood and impact use a 1-5 scale. Risk score equals likelihood multiplied by impact.

| ID | Scenario | Likelihood | Impact | Inherent score | Rating | Evidence |
|---|---|---:|---:|---:|---|---|
| R-01 | Publicly reachable RDP is targeted by automated credential attacks | 4 | 4 | 16 | High | 03, 04, 05 |
| R-02 | Local administrator credential compromise grants full VM control | 3 | 5 | 15 | High | 02, 06, 07 |
| R-03 | Endpoint and update configuration gaps increase exploitation risk | 3 | 4 | 12 | High | 08, 11, 12 |
| R-04 | Subscription Owner concentration enables high-impact misuse | 2 | 5 | 10 | High | 13 |
| R-05 | Lack of centralized alerting delays detection and response | 3 | 3 | 9 | Medium | 09, 10 |

### Scoring justification

- **R-01 likelihood 4:** internet-reachable administrative ports are routinely scanned and targeted. **Impact 4:** successful authentication would provide interactive access, although additional controls and credential quality affect final impact.
- **R-02 likelihood 3:** credential compromise is possible but was not observed. **Impact 5:** the account is a local administrator and can fully control the VM.
- **R-03 likelihood 3:** endpoint configuration gaps create plausible exposure, but this assessment did not verify a specific exploitable CVE. **Impact 4:** successful exploitation or control tampering could significantly affect the VM.
- **R-04 likelihood 2:** misuse is less likely in a controlled personal lab. **Impact 5:** Owner permissions at subscription scope can affect resources and access assignments.
- **R-05 likelihood 3:** adverse activity is possible in an internet-connected environment. **Impact 3:** local logs provide some evidence, but absent centralized alerting can delay response.

## 6. Security controls and framework alignment

| Risk | Control | Type | NIST CSF 2.0 | CIS Controls v8.1 |
|---|---|---|---|---|
| R-01 | Restrict administrative ingress and remove continuous public management exposure | Preventive | PR.PS, PR.AA | 4.4, 12.2 |
| R-02 | Require MFA for administrative access and centralize authentication | Preventive | PR.AA | 6.4, 6.5, 6.7 |
| R-03 | Maintain secure configuration and automated OS patch management | Preventive / Corrective | PR.PS | 4.1, 7.3 |
| R-04 | Enforce least privilege, RBAC, separation of duties, and access reviews | Governance / Preventive | GV.RR, PR.AA | 5.1, 6.8 |
| R-05 | Collect guest logs centrally and configure actionable alerts | Detective | DE.CM, DE.AE | 8.2, 8.11 |

The mappings demonstrate alignment to control intent. They do not assert certification or complete implementation of either framework.

## 7. Treatment plan

| Priority | Owner | Action | Target result | Status |
|---|---|---|---|---|
| P0 | Cloud administrator | Restrict RDP source to trusted IPv4 `/32` | No `Any` source for TCP/3389 | Complete |
| P0 | Cloud administrator | Replace direct RDP with Bastion, VPN/private access, or JIT | No continuously exposed public admin port | Planned |
| P0 | Identity administrator | Require MFA-capable centralized authentication | MFA required for administrative access where supported | Planned |
| P1 | Endpoint administrator | Enable patch orchestration and verify compliance | Scheduled patching with compliance evidence | Planned |
| P1 | Security administrator | Enable endpoint protections shown as disabled | Warnings resolved or formally accepted | Planned |
| P1 | SOC / cloud administrator | Send guest logs to Log Analytics and enable alerts | Central queries and tested notifications | Planned |
| P2 | Subscription administrator | Replace standing Owner access with least privilege | No unnecessary permanent Owner assignment | Planned |

## 8. Mitigation validation

The baseline RDP rule allowed the source `Any`. The rule was changed to `IP Addresses` with the trusted administrator public IPv4 expressed as a `/32`, source ports set to `*`, destination TCP/3389, and action Allow.

This control reduces attack surface but does not eliminate public RDP risk. The revised likelihood for R-01 is 2, while impact remains 4, producing a residual score of 8 (Medium). A private administrative access method or Just-in-Time access remains recommended.

## 9. Overall risk posture

The lab's limited scale does not eliminate risk: a public administrative access path, a privileged local credential, endpoint configuration gaps, limited centralized monitoring, and broad subscription privilege can still produce significant impact. One meaningful mitigation was implemented and validated, but identity, monitoring, patching, endpoint-hardening, and RBAC actions remain necessary for a mature target posture.

## 10. Limitations and statement of use

This is a portfolio GRC simulation conducted in an authorized personal Azure lab. Findings are based on screenshots and configuration review at a point in time. No active exploitation was performed. The report is not a penetration-test report, formal audit opinion, compliance certificate, or guarantee that no other risks exist.
