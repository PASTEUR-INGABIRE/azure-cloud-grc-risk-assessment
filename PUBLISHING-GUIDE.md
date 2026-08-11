# GitHub and LinkedIn Publishing Guide

## GitHub repository settings

**Repository name**

`azure-cloud-grc-risk-assessment`

**Description**

`Evidence-based Azure cloud security risk assessment and GRC simulation with risk scoring, NIST CSF 2.0/CIS Controls v8.1 mapping, and validated RDP mitigation.`

**Visibility**

Public

**Suggested topics**

`azure` `cloud-security` `grc` `cybersecurity` `risk-assessment` `nist-csf` `cis-controls` `windows-server` `network-security-group` `cybersecurity-portfolio`

## Publish using the GitHub website

1. Sign in to GitHub and select **New repository**.
2. Use the exact repository name above.
3. Set visibility to **Public**.
4. Do not create another README, `.gitignore`, or license because they are already included.
5. Upload the contents of this project directory, preserving the `docs`, `evidence`, and `reports` folders.
6. Commit with this message:

   `Publish Azure cloud security GRC risk assessment`

7. Add the suggested description and topics.
8. Open the public repository in a private/incognito browser window and verify every image, workbook, and PDF link.

## Publish using Git

Create the empty GitHub repository first, then run these commands from the project directory. Replace `YOUR-GITHUB-USERNAME` with your actual username.

```bash
git init
git add .
git commit -m "Publish Azure cloud security GRC risk assessment"
git branch -M main
git remote add origin https://github.com/YOUR-GITHUB-USERNAME/azure-cloud-grc-risk-assessment.git
git push -u origin main
```

If Git asks for an identity before committing, configure the name and verified email associated with your GitHub account.

## Final public-content check

- Confirm the README cover and before/after images render correctly.
- Download and open `reports/cloud-security-risk-assessment.pdf`.
- Download and open `reports/risk-register.xlsx`.
- Confirm no password, access token, private key, public IP, subscription ID, or tenant ID is readable.
- Confirm the final RDP evidence shows source ports `*` and destination TCP/3389.
- Confirm only project files are present; do not upload the original mixed screenshot folder.

## LinkedIn publication

1. Replace `[ADD YOUR GITHUB REPOSITORY URL]` in [docs/linkedin-post.md](docs/linkedin-post.md).
2. Create a LinkedIn post using that draft.
3. Attach these images in order:

   1. `evidence/05-rdp-rule-details.png`
   2. `evidence/14-rdp-restricted-after.png`
   3. `reports/report-cover.png`

4. Paste the GitHub URL near the end of the post.
5. After publishing, add the project to the LinkedIn **Featured** section using the GitHub repository URL.

## LinkedIn Featured entry

**Title**

`Azure Cloud Security Risk Assessment & GRC Simulation`

**Description**

`Evidence-based Azure security assessment featuring a professional risk register, NIST CSF 2.0 and CIS Controls v8.1 mapping, and a validated RDP exposure mitigation.`

