# Security Control Mapping

## Mapping approach

Controls were selected based on whether they reduce the likelihood or impact of each documented risk. The mappings use current category names from NIST CSF 2.0 and safeguard identifiers from CIS Controls v8.1. They demonstrate alignment to framework intent, not compliance certification.

| Risk | Proposed control | Control type | NIST CSF 2.0 rationale | CIS Controls v8.1 rationale |
|---|---|---|---|---|
| R-01 | Restrict RDP ingress to trusted sources; prefer Bastion, VPN/private access, or JIT | Preventive | **PR.PS** protects platforms through secure configuration; **PR.AA** limits authorized access | **4.4** addresses host firewalls; **12.2** addresses secure network architecture |
| R-02 | Require MFA for administrative access and use centralized authentication where supported | Preventive | **PR.AA** covers identity management, authentication, and access control | **6.4** covers remote network access MFA; **6.5** administrative MFA; **6.7** centralized access control |
| R-03 | Enable endpoint protections and automated OS patch management | Preventive / Corrective | **PR.PS** covers platform security and configuration maintenance | **4.1** secure configuration process; **7.3** automated OS patch management |
| R-04 | Replace unnecessary standing Owner privilege with least privilege, separation of duties, and reviews | Governance / Preventive | **GV.RR** establishes roles and authorities; **PR.AA** enforces authorization | **5.1** account inventory; **6.8** role-based access control and recurring review |
| R-05 | Centralize Windows security logs and configure tested alerts | Detective | **DE.CM** covers continuous monitoring; **DE.AE** covers adverse-event analysis | **8.2** audit-log collection; **8.11** audit-log review |

## Important version note

The course material referenced `NIST CSF PR.AC`, which is a CSF 1.1 category. This portfolio uses **NIST CSF 2.0**, where identity and access outcomes are represented under **PR.AA**. This update is intentional and documented to avoid mixing framework versions.

## Sources

- NIST CSF 2.0: https://www.nist.gov/publications/nist-cybersecurity-framework-csf-20
- NIST CSF 2.0 Reference Tool: https://csrc.nist.gov/projects/cybersecurity-framework/filters
- CIS Controls v8.1: https://www.cisecurity.org/controls/v8-1
- CIS Controls Navigator: https://www.cisecurity.org/controls/cis-controls-navigator

