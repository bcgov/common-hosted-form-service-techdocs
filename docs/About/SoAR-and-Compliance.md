[Home](index) > [About CHEFS](About) > **SoAR and Compliance**
***

# SoAR and Compliance Procedures

The Security Threat and Risk Assessment's (STRA) Statement of Acceptable Risks (SoAR) describes how the security of CHEFS is to be maintained. The following procedures are used to stay in compliance with the SoAR.

## Access Review

The SoAR section "Assessment", subsection "Access Control" states:

> Access reviews are done regularly every month to ensure accounts are removed when no longer required.

CHEFS is on a two week sprint schedule, and this review happens every second sprint before the sprint planning meeting. Check the following access controls and remove stale user accounts:

- The `Collaborators` in the GitHub repo must only be current developers, and contractors must not have more than `Write` access
- The [chefs-team](https://github.com/orgs/bcgov/teams/chefs-team) in GitHub must only be current developers, and contractors must not have more than `Member` access
- The `pr-external`, `test`, and `prod` Environments in GitHub have `Required reviewers` in the protection rules that must only be current users
- The `RoleBindings` in the OpenShift `-tools`, `-dev`, `-test`, and `-prod` environments of the `a12c97` and `a191b5` namespaces must only be for current `User` and `ServiceAccount` subjects
- SysDig access must only be for current team users (`oc -n a12c97-tools get sysdig-team a12c97-sysdigteam -o yaml`)
- The [SSO CSS app](https://bcgov.github.io/sso-requests-preview) in the `My Teams` tab must only contain current users in the `CoCo Team`
<!--
#### TODO:
- api.gov.bc.ca
- Discord?
- Confluence/JIRA
- S3
-->

Update the log at the end of this page to show that this step has been completed.

## Advanced Cluster Security (ACS)

The SoAR section "Assessment", subsection "Vulnerability Management" states:

> Advanced Cluster Security (ACS) is used by the CHEFS Team to identify, prioritize, and address security risks and vulnerabilities in the CHEFS application, including images, pods, and configurations.

CHEFS is on a two week sprint schedule, and this review happens before every sprint planning meeting. In [Red Hat ACS](https://acs.developer.gov.bc.ca) ensure that the top item in the `Images most at risk` has a JIRA item created for it. If not, create a JIRA item in the Backlog using the template:

- _Type_: Task
- _Title_: ACS Image at risk: **[IMAGE_NAME]**
- _Description_:<br>The Red Hat Advanced Cluster Security (ACS) application has identified the image **[IMAGE_NAME]** as having vulnerabilities that are fixable. To satisfy the requirements outlined in the Security Threat and Risk Assessment's (STRA) Statement of Acceptable Risks (SoAR), this image must be updated to resolve fixable vulnerabilities (or mitigated in some other way, if updating the image is not possible).
- _Epic Link_: CHEFS Bugs and Defects

Update the log at the end of this page to show that this step has been completed.

During sprint planning arrange for the new JIRA item to be included in the sprint.

## Dependabot

The SoAR section "Assessment", subsection "Vulnerability Management" states:

> GitHub’s Dependabot is enabled for enforced for security alerts. Dependency package security audits are done periodically for the main CHEFS image which is updated regularly.

CHEFS is on a two week sprint schedule, and this review happens before every sprint planning meeting. In the `common-hosted-form-service` GitHub repository check the `Security` > `Dependabot` alerts. Create a JIRA item in the Backlog for new alerts using the template:

- _Type_: Task
- _Title_: Dependabot Vulnerability Alert for **[PACKAGE_NAME]** in **[MANIFEST_DIR]**
- _Description_:<br>The GitHub Dependabot process has created an alert for the **[PACKAGE_NAME]** dependency. To satisfy the requirements outlined in the Security Threat and Risk Assessment's (STRA) Statement of Acceptable Risks (SoAR), this vulnerability must be handled by updating the package version (or mitigated in some other way, if updating the package is not possible).<br>
  ht<workaround>tps://gi</workaround>thub.com/bcgov/common-hosted-form-service/security/dependabot/**[DEPENDABOT_ID]**
- _Epic Link_: CHEFS Bugs and Defects

Update the log at the end of this page to show that this step has been completed.

During sprint planning arrange for the new JIRA item to be included in the sprint.

## OWASP Zap Scan

The SoAR section "Findings and Conclusion" states:

> The CHEFS Team has remediated all medium vulnerabilities identified in OWASP ZAP scan conducted by NRS. Also, they have added the OWASP ZAP tool into the CHEFS development pipeline.

The ZAP scan vulnerabilities were remediated, and the GitHub Actions now run the scans with every build. Manual steps are needed to check the scan results to see if new vulnerabilities exist.

CHEFS is on a two week sprint schedule, and this review happens before every sprint planning meeting. In the `common-hosted-form-service` GitHub repository open the `Issue` called `ZAP Full Scan Report`. At the bottom of the issue follow the link to retrieve the `zap_scan` artifact. Create a JIRA item in the Backlog for new alerts using the template:

- _Type_: Task
- _Title_: OWASP ZAP Scan Vulnerability **[VULNERABILITY_NAME]**
- _Description_:<br>The OWASP Zap Scan process has identified a **[VULNERABILITY_RISK_LEVEL]** risk level vulnerability:<br>
  \> **[VULNERABILITY_DESCRIPTION]**<br>
  To satisfy the requirements outlined in the Security Threat and Risk Assessment's (STRA) Statement of Acceptable Risks (SoAR), this vulnerability must be remediated.
- _Epic Link_: CHEFS Bugs and Defects

Update the log at the end of this page to show that this step has been completed.

During sprint planning arrange for the new JIRA item to be included in the sprint.

## Log

<!-- NOTE: The log is in reverse order by date (newest at top) -->
|Date|Access Review|ACS|Dependabot|OWASP Zap Scan|
|:---:|:---:|:---:|:---:|:---:|
|2024-06-27|&check;|&check;|&check;|Broken|
|2024-05-30|&check;|&check;|&check;|Broken|
|2024-04-11|&check;|&check;|&check;|Broken|
|2024-03-28|&check;|&check;|&check;|Broken|
|2024-03-14|&check;|&check;|&check;|Broken|
|2024-02-29|&check;|&check;|&check;|Broken|
|2024-02-15|&check;|&check;|&check;|Broken|
|2024-02-01|&check;|&check;|&check;|&check;|
|2024-01-18|&check;|&check;|&check;|&check;|
|2024-01-04|&check;|&check;|&check;|&check;|
|2023-12-07|&check;|&check;|&check;|&check;|
|2023-11-01|&check;|&check;|&check;|Wait for Vue3|
|2023-10-12|&check;|&check;|&check;|Wait for Vue3|

***
[Terms of Use](Terms-of-Use) | [Privacy](Privacy) | [Security](Security) | [Service Agreement](Service-Agreement) | [Accessibility](Accessibility)
