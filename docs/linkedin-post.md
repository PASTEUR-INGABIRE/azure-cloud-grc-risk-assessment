# LinkedIn Publication Draft

I completed my second cybersecurity portfolio project: **Cybersecurity Project: Cloud Security Risk Assessment & GRC Simulation (Azure)**.

In this project, I assessed a Windows Server virtual machine hosted in Microsoft Azure from a Governance, Risk, and Compliance perspective. I documented the environment, identified realistic cloud risks, scored likelihood and impact, mapped safeguards to NIST CSF 2.0 and CIS Controls v8.1, and produced an executive-ready risk assessment report.

Key findings included:

- RDP exposed to any internet source
- A privileged local administrator access path
- Endpoint and patch-management configuration gaps
- No configured Azure Monitor alerts for the VM
- Subscription-level Owner privilege concentration

The highest risk was public RDP exposure, scored **16/25 (High)**. I reduced this exposure by restricting the Azure Network Security Group rule from `Any` source to a trusted public IPv4 `/32`, then documented the before-and-after evidence. This reduced the assessed residual score to **8/25 (Medium)**.

The project strengthened my practical skills in Azure cloud security, risk assessment, risk-register development, control mapping, audit evidence, mitigation planning, and technical-to-business risk communication.

GitHub project: **[ADD YOUR GITHUB REPOSITORY URL]**

#Cybersecurity #CloudSecurity #MicrosoftAzure #GRC #RiskAssessment #NISTCSF #CISControls #AzureSecurity #CybersecurityPortfolio #ContinuousLearning

## Recommended LinkedIn media

Attach these three images in this order:

1. `05-rdp-rule-details.png` - baseline risk
2. `14-rdp-restricted-after.png` - implemented mitigation
3. `reports/report-cover.png` - professional report cover

