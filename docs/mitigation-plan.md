# Risk Treatment and Mitigation Plan

| ID | Action | Priority | Owner role | Target | Verification evidence | Status |
|---|---|---|---|---|---|---|
| M-01 | Restrict the RDP NSG rule from `Any` to trusted IPv4 `/32` | P0 | Cloud Administrator | Immediate | Saved NSG rule and successful authorized RDP test | Complete |
| M-02 | Replace direct public RDP with Azure Bastion, VPN/private access, or JIT | P0 | Cloud Architect | 30 days | No continuously exposed public TCP/3389 rule | Planned |
| M-03 | Require MFA-capable centralized authentication for administrative access | P0 | Identity Administrator | 30 days | Conditional Access / authentication evidence and sign-in test | Planned |
| M-04 | Enable automated patch orchestration and compliance reporting | P1 | Endpoint Administrator | 30 days | Patch compliance dashboard or update report | Planned |
| M-05 | Enable Tamper Protection and potentially unwanted application blocking | P1 | Security Administrator | 14 days | Windows Security shows no corresponding warnings | Planned |
| M-06 | Deploy Azure Monitor Agent and send security events to Log Analytics | P1 | Cloud / SOC Engineer | 30 days | Security events queryable in the workspace | Planned |
| M-07 | Configure alert rules and an action group; test delivery | P1 | SOC Engineer | 30 days | Test alert received by the designated channel | Planned |
| M-08 | Review subscription Owner access and implement least privilege | P2 | Subscription Administrator | 45 days | Access review and documented role assignments | Planned |

## Treatment decisions

- **Mitigate:** R-01, R-02, R-03, and R-05 require technical controls.
- **Accept temporarily:** R-04 is acceptable for a personal lab, with the production recommendation clearly documented.
- **Transfer/Avoid:** not selected because the assessed lab remains owned and operated by the assessor.

## Residual risk statement

Restricting RDP to a trusted `/32` reduces exposure to arbitrary internet sources but does not eliminate risks from a compromised trusted endpoint, IP changes, credential theft, or a publicly routable management service. The strategic target remains private or Just-in-Time administrative access with MFA-capable centralized authentication.

