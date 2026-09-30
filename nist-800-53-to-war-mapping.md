# NIST SP 800-53 Rev. 5 to Well-Architected Review Mapping

This document uses NIST SP 800-53 Rev. 5 as the basis of comparison and shows, for each control in the in-scope families at the FedRAMP Moderate baseline, which Well-Architected Review (WAR) best practices examine it. A mapping means the WAR investigates the control; it does not mean the control is satisfied. Findings determine that.

Base controls only. Control enhancements roll up to their base control. Best-practice IDs refer to `cac-well-architected-review-questions.md`.

## Families in scope

| Family | Name | Why in scope |
|---|---|---|
| AC | Access Control | The incident was a PII exposure. AC governs who can see and share records, fields, files, and reports, including guest and public access. |
| AU | Audit and Accountability | Determines whether an exposure can be detected and reconstructed. Without Shield, the customer-side controls are review and retention of the logs the platform provides. |
| CM | Configuration Management | The pipeline, source-controlled baseline, and drift detection are the structural fix for uncontrolled change. CM is where that work is assessed. |
| CP | Contingency Planning | The OWN backup implementation and restore test are in flight; CP is the family that judges them. |
| IA | Identification and Authentication | MFA, SSO, password policy, integration credentials, and guest authentication decide who the platform believes a user is. Added after the initial scoping because an assessor will expect it alongside AC for a PII exposure. |
| IR | Incident Response | The incident exposed gaps in handling and reporting. IR covers the process, testing, and reporting obligations. |
| SC | System and Communications Protection | The public site, transport encryption, certificates, and browser-facing settings are the boundary of the system. |
| SI | System and Information Integrity | Open findings (jQuery, Visualforce), input validation on public intake, and data retention all sit in SI. |

## Families out of scope for this cycle

| Family | Name | Reason |
|---|---|---|
| CA, RA, PL, PM | Assessment, Risk, Planning, Program Management | Agency-level programs. The WAR's Compliant domain touches CA-2, CA-3, CA-7, and RA-2 but does not assess them. |
| SA, SR | System and Services Acquisition, Supply Chain | Vendor and package governance is touched by the WAR (SA-9, SA-22) but formal assessment is deferred. |
| PE, MA, MP | Physical, Maintenance, Media | Inherited from Salesforce Government Cloud. |
| AT, PS | Awareness and Training, Personnel Security | Agency programs outside the platform team's control. |
| PT | PII Processing and Transparency | Pending client guidance. PT is in the SP 800-53B privacy baseline, not the FedRAMP Moderate security baseline, and is owned by the agency privacy office. Given the PII incident and the data retention work, a narrow slice (PT-2, PT-3, PT-5, PT-6, PT-7) may be brought into scope. Decision to be confirmed with the client before the review starts. |

## Status definitions

- **Covered**: at least one WAR best practice examines the control.
- **Inherited**: provided by Salesforce Government Cloud. Confirm against the Customer Responsibility Matrix (TR-COM1-BP02).
- **Agency**: owned by the agency outside the platform team; noted where the governance plan touches it.
- **Gap**: customer-responsible with no WAR coverage.


## AC: Access Control

| Control | Title | Status | WAR best practices / explanation |
|---|---|---|---|
| AC-1 | Policy and Procedures | Agency | The -1 control in each family is the policy and procedures requirement. The agency owns the policy; the governance plan is the platform-level procedure that implements it. |
| AC-2 | Account Management | Covered | TR-SEC1-BP03 (User lifecycle is managed (provisioning, deprovisioning, review)); TR-SEC2-BP03 (Break-glass / emergency access is defined and controlled); TR-SEC5-BP02 (Login IP ranges and login hours are configured for sensitive profiles) |
| AC-3 | Access Enforcement | Covered | TR-SEC1-BP02 (Org-wide defaults and sharing model are deliberately set); TR-SEC11-BP01 (Report and dashboard folders are shared deliberately and dashboards run as an appropriate user); TR-SEC11-BP02 (List views on PII-bearing objects are not visible to all users unnecessarily); TR-SEC12-BP01 (Production PII in sandboxes is masked, minimized, or access-restricted); TR-SEC13-BP01 (Guest user profiles hold the minimum permissions and sharing); TR-SEC15-BP01 (Visualforce pages escape output and validate parameters); TR-SEC3-BP01 (Connected Apps are inventoried and scoped minimally); TR-SEC6-BP01 (Field-level security restricts sensitive fields appropriately); TR-SEC6-BP02 (Apex enforces sharing, CRUD, and FLS) |
| AC-4 | Information Flow Enforcement | Covered | TR-SEC3-BP01 (Connected Apps are inventoried and scoped minimally); TR-SEC6-BP01 (Field-level security restricts sensitive fields appropriately) |
| AC-5 | Separation of Duties | Covered | TR-SEC10-BP01 (Change authors, approvers, and deployers are different people) |
| AC-6 | Least Privilege | Covered | AD-RES4-BP02 (Production change access is restricted to the pipeline and a minimal set of admins); TR-SEC1-BP01 (Least-privilege profile and permission set design); TR-SEC11-BP05 (Bulk export capability is limited and inventoried); TR-SEC12-BP01 (Production PII in sandboxes is masked, minimized, or access-restricted); TR-SEC2-BP01 (System Administrator access is restricted to a small, documented set of users); TR-SEC2-BP02 (Integration and API-only users use dedicated accounts with minimum scope); TR-SEC2-BP03 (Break-glass / emergency access is defined and controlled) |
| AC-7 | Unsuccessful Logon Attempts | Covered | TR-SEC4-BP03 (Password policy meets FedRAMP Moderate expectations) |
| AC-8 | System Use Notification | Covered | TR-SEC10-BP02 (A system use notification is displayed at login) |
| AC-11 | Device Lock | Covered | TR-SEC5-BP01 (Session timeout, secure connection, and cookie settings match data sensitivity) |
| AC-12 | Session Termination | Covered | TR-SEC5-BP01 (Session timeout, secure connection, and cookie settings match data sensitivity) |
| AC-14 | Permitted Actions Without Identification or Authentication | Covered | TR-SEC13-BP01 (Guest user profiles hold the minimum permissions and sharing); TR-SEC13-BP02 (Site security settings are hardened) |
| AC-17 | Remote Access | Covered | TR-SEC5-BP02 (Login IP ranges and login hours are configured for sensitive profiles); TR-SEC5-BP03 (Mobile access is governed) |
| AC-18 | Wireless Access | Inherited | No wireless access is provided by the Salesforce service; agency wireless is outside this system boundary. |
| AC-19 | Access Control for Mobile Devices | Covered | TR-SEC5-BP03 (Mobile access is governed) |
| AC-20 | Use of External Systems | Covered | TR-COM3-BP01 (Changes that may affect the authorization boundary are reviewed before deployment); TR-REL7-BP01 (Backup data is encrypted, access-controlled, and inside the authorization boundary) |
| AC-21 | Information Sharing | Covered | TR-SEC11-BP01 (Report and dashboard folders are shared deliberately and dashboards run as an appropriate user); TR-SEC11-BP03 (Files and attachments cannot be exposed through public links or over-broad sharing); TR-SEC11-BP04 (Outbound email does not carry more PII than necessary); TR-SEC11-BP05 (Bulk export capability is limited and inventoried) |
| AC-22 | Publicly Accessible Content | Covered | TR-SEC11-BP03 (Files and attachments cannot be exposed through public links or over-broad sharing); TR-SEC13-BP01 (Guest user profiles hold the minimum permissions and sharing); TR-SEC13-BP03 (Public intake forms validate input and collect the minimum) |

## AU: Audit and Accountability

| Control | Title | Status | WAR best practices / explanation |
|---|---|---|---|
| AU-1 | Policy and Procedures | Agency | The -1 control in each family is the policy and procedures requirement. The agency owns the policy; the governance plan is the platform-level procedure that implements it. |
| AU-2 | Event Logging | Covered | TR-SEC9-BP01 (Setup Audit Trail is exported and reviewed on a defined cadence); TR-SEC9-BP02 (Field History Tracking is enabled on sensitive fields); TR-SEC9-BP04 (Real-time security event detection) |
| AU-3 | Content of Audit Records | Inherited | Salesforce generates audit records with the required content; the customer cannot alter record format. |
| AU-4 | Audit Log Storage Capacity | Inherited | Log storage capacity is managed by Salesforce; customer retention limits (180 days Setup Audit Trail, 6 months Login History) are addressed under AU-11. |
| AU-5 | Response to Audit Logging Process Failures | Inherited | Salesforce is responsible for responding to failures in its logging infrastructure. |
| AU-6 | Audit Record Review, Analysis, and Reporting | Covered | TR-COM2-BP01 (Evidence for each customer-responsible control is current and accessible); TR-COM2-BP02 (Continuous monitoring activities are defined and performed); TR-REL5-BP01 (Login, API, and integration activity is monitored); TR-SEC9-BP01 (Setup Audit Trail is exported and reviewed on a defined cadence); TR-SEC9-BP04 (Real-time security event detection) |
| AU-7 | Audit Record Reduction and Report Generation | Inherited | Reporting on audit data is provided through Salesforce Setup pages and exports; the customer-side review is assessed under AU-6. |
| AU-8 | Time Stamps | Inherited | Time stamps are applied by the platform. |
| AU-9 | Protection of Audit Information | Covered | TR-SEC12-BP02 (Debug logs and trace flags do not become a PII store); TR-SEC16-BP01 (Exported audit records are protected and retained) |
| AU-11 | Audit Record Retention | Covered | TR-COM4-BP01 (Records retention obligations are mapped to platform behavior); TR-SEC16-BP01 (Exported audit records are protected and retained); TR-SEC9-BP03 (Long-term audit retention beyond 18 months) |
| AU-12 | Audit Record Generation | Inherited | Audit record generation is a platform function; what the customer reviews is assessed under AU-2 and AU-6. |

## CM: Configuration Management

| Control | Title | Status | WAR best practices / explanation |
|---|---|---|---|
| CM-1 | Policy and Procedures | Agency | The -1 control in each family is the policy and procedures requirement. The agency owns the policy; the governance plan is the platform-level procedure that implements it. |
| CM-2 | Baseline Configuration | Covered | AD-RES1-BP01 (A defined CI/CD or release pipeline moves changes from source to production); AD-RES1-BP03 (Metadata source-of-truth conflicts are detected); AD-RES4-BP04 (A configuration management plan names the baseline, roles, and change process) |
| CM-3 | Configuration Change Control | Covered | AD-RES1-BP01 (A defined CI/CD or release pipeline moves changes from source to production); AD-RES1-BP03 (Metadata source-of-truth conflicts are detected); AD-RES4-BP04 (A configuration management plan names the baseline, roles, and change process); TR-REL6-BP02 (Releases follow a defined process with rollback capability) |
| CM-4 | Impact Analyses | Covered | AD-RES4-BP01 (Security impact analysis precedes production changes) |
| CM-5 | Access Restrictions for Change | Covered | AD-RES4-BP02 (Production change access is restricted to the pipeline and a minimal set of admins); TR-SEC10-BP01 (Change authors, approvers, and deployers are different people) |
| CM-6 | Configuration Settings | Covered | TR-REL1-BP01 (Salesforce Health Check is run and tracked) |
| CM-7 | Least Functionality | Covered | AD-RES4-BP03 (Unused platform features and settings are disabled); EZ-INT2-BP01 (Unused customization is identified and removed) |
| CM-8 | System Component Inventory | Covered | AD-CMP3-BP02 (Managed package dependencies are inventoried and governed); TR-COM3-BP02 (Installed packages and integrations are inventoried and reviewed periodically) |
| CM-9 | Configuration Management Plan | Covered | AD-RES4-BP04 (A configuration management plan names the baseline, roles, and change process) |
| CM-10 | Software Usage Restrictions | Covered | TR-COM3-BP01 (Changes that may affect the authorization boundary are reviewed before deployment) |
| CM-11 | User-Installed Software | Covered | TR-COM3-BP01 (Changes that may affect the authorization boundary are reviewed before deployment) |
| CM-12 | Information Location | Covered | TR-REL7-BP01 (Backup data is encrypted, access-controlled, and inside the authorization boundary); TR-SEC12-BP01 (Production PII in sandboxes is masked, minimized, or access-restricted); TR-SEC7-BP01 (Sensitive data is classified and inventoried) |

## CP: Contingency Planning

| Control | Title | Status | WAR best practices / explanation |
|---|---|---|---|
| CP-1 | Policy and Procedures | Agency | The -1 control in each family is the policy and procedures requirement. The agency owns the policy; the governance plan is the platform-level procedure that implements it. |
| CP-2 | Contingency Plan | Covered | AD-RES3-BP01 (Business continuity assumptions about Salesforce are documented and tested) |
| CP-3 | Contingency Training | Agency | Contingency training is an agency program. The governance plan should name who is trained on the restore procedure (section 7). |
| CP-4 | Contingency Plan Testing | Covered | TR-REL4-BP01 (A current data backup capability exists and is tested) |
| CP-6 | Alternate Storage Site | Inherited | Alternate storage is part of Salesforce's data center architecture. |
| CP-7 | Alternate Processing Site | Inherited | Alternate processing is part of Salesforce's data center architecture. |
| CP-8 | Telecommunications Services | Inherited | Telecommunications resilience is provided by Salesforce. |
| CP-9 | System Backup | Covered | AD-RES3-BP01 (Business continuity assumptions about Salesforce are documented and tested); TR-REL4-BP01 (A current data backup capability exists and is tested); TR-REL7-BP01 (Backup data is encrypted, access-controlled, and inside the authorization boundary) |
| CP-10 | System Recovery and Reconstitution | Covered | AD-RES3-BP01 (Business continuity assumptions about Salesforce are documented and tested); TR-REL4-BP01 (A current data backup capability exists and is tested) |

## IA: Identification and Authentication

| Control | Title | Status | WAR best practices / explanation |
|---|---|---|---|
| IA-1 | Policy and Procedures | Agency | The -1 control in each family is the policy and procedures requirement. The agency owns the policy; the governance plan is the platform-level procedure that implements it. |
| IA-2 | Identification and Authentication (Organizational Users) | Covered | TR-SEC2-BP02 (Integration and API-only users use dedicated accounts with minimum scope); TR-SEC4-BP01 (MFA is enforced for all interactive logins); TR-SEC4-BP02 (SSO, if used, is configured securely) |
| IA-3 | Device Identification and Authentication | Inherited | Device authentication is not part of the Salesforce service boundary; agency network access control applies. |
| IA-4 | Identifier Management | Covered | TR-SEC1-BP03 (User lifecycle is managed (provisioning, deprovisioning, review)); TR-SEC2-BP02 (Integration and API-only users use dedicated accounts with minimum scope) |
| IA-5 | Authenticator Management | Covered | TR-SEC3-BP02 (Credentials for outbound integrations are stored in Named Credentials or External Credentials); TR-SEC4-BP03 (Password policy meets FedRAMP Moderate expectations); TR-SEC7-BP04 (Certificates and keys are inventoried, owned, and rotated before expiry) |
| IA-6 | Authentication Feedback | Inherited | Obscuring authentication feedback (masked passwords) is platform behavior. |
| IA-7 | Cryptographic Module Authentication | Inherited | FIPS-validated cryptographic modules are part of the Salesforce Government Cloud authorization. |
| IA-8 | Identification and Authentication (Non-Organizational Users) | Covered | TR-SEC13-BP02 (Site security settings are hardened); TR-SEC4-BP02 (SSO, if used, is configured securely) |
| IA-11 | Re-authentication | Covered | TR-SEC5-BP01 (Session timeout, secure connection, and cookie settings match data sensitivity) |
| IA-12 | Identity Proofing | Agency | Identity proofing is performed by agency HR and PIV issuance before an account is requested; the WAR assesses provisioning under IA-4 and AC-2. |

## IR: Incident Response

| Control | Title | Status | WAR best practices / explanation |
|---|---|---|---|
| IR-1 | Policy and Procedures | Agency | The -1 control in each family is the policy and procedures requirement. The agency owns the policy; the governance plan is the platform-level procedure that implements it. |
| IR-2 | Incident Response Training | Covered | AD-RES2-BP01 (A documented incident response process exists and is exercised) |
| IR-3 | Incident Response Testing | Covered | AD-RES2-BP01 (A documented incident response process exists and is exercised) |
| IR-4 | Incident Handling | Covered | AD-RES2-BP01 (A documented incident response process exists and is exercised); TR-REL5-BP02 (Alerts exist for failures that affect users or the business) |
| IR-5 | Incident Monitoring | Covered | TR-SEC9-BP04 (Real-time security event detection) |
| IR-6 | Incident Reporting | Covered | AD-RES5-BP01 (Reporting obligations and timelines are defined for security and PII incidents) |
| IR-7 | Incident Response Assistance | Agency | Incident response assistance comes from the agency SOC and Salesforce Support. The escalation path is documented in the governance plan (section 8) but the WAR does not assess the assistance capability itself. |
| IR-8 | Incident Response Plan | Covered | AD-RES2-BP01 (A documented incident response process exists and is exercised); AD-RES5-BP01 (Reporting obligations and timelines are defined for security and PII incidents) |

## SC: System and Communications Protection

| Control | Title | Status | WAR best practices / explanation |
|---|---|---|---|
| SC-1 | Policy and Procedures | Agency | The -1 control in each family is the policy and procedures requirement. The agency owns the policy; the governance plan is the platform-level procedure that implements it. |
| SC-2 | Separation of System and User Functionality | Inherited | Separation of system management from user functionality is inherent to the multitenant platform. |
| SC-4 | Information in Shared System Resources | Inherited | Tenant isolation in shared resources is a Salesforce responsibility. |
| SC-5 | Denial-of-Service Protection | Covered | TR-REL2-BP01 (API and async limit usage is monitored against allocation); TR-SEC13-BP03 (Public intake forms validate input and collect the minimum) |
| SC-7 | Boundary Protection | Covered | TR-SEC13-BP02 (Site security settings are hardened); TR-SEC14-BP01 (Session Settings browser protections are enabled and CSP and CORS allowlists are minimal) |
| SC-8 | Transmission Confidentiality and Integrity | Covered | TR-SEC11-BP04 (Outbound email does not carry more PII than necessary); TR-SEC13-BP02 (Site security settings are hardened); TR-SEC14-BP02 (Outbound email from the org is authenticated); TR-SEC5-BP01 (Session timeout, secure connection, and cookie settings match data sensitivity); TR-SEC7-BP02 (Encryption in transit uses current TLS) |
| SC-10 | Network Disconnect | Covered | TR-SEC5-BP01 (Session timeout, secure connection, and cookie settings match data sensitivity) |
| SC-12 | Cryptographic Key Establishment and Management | Covered | TR-SEC7-BP04 (Certificates and keys are inventoried, owned, and rotated before expiry) |
| SC-13 | Cryptographic Protection | Covered | TR-SEC7-BP02 (Encryption in transit uses current TLS); TR-SEC7-BP03 (Encryption at rest beyond the platform default) |
| SC-15 | Collaborative Computing Devices and Applications | Inherited | No collaborative computing devices are within the system boundary. |
| SC-17 | Public Key Infrastructure Certificates | Covered | TR-SEC7-BP04 (Certificates and keys are inventoried, owned, and rotated before expiry) |
| SC-18 | Mobile Code | Covered | TR-SEC14-BP01 (Session Settings browser protections are enabled and CSP and CORS allowlists are minimal) |
| SC-20 | Secure Name/Address Resolution Service (Authoritative Source) | Inherited | DNS resolution for Salesforce domains is provided by Salesforce. |
| SC-21 | Secure Name/Address Resolution Service (Recursive or Caching Resolver) | Inherited | DNS resolution for Salesforce domains is provided by Salesforce. |
| SC-22 | Architecture and Provisioning for Name/Address Resolution Service | Inherited | DNS architecture for Salesforce domains is provided by Salesforce. |
| SC-23 | Session Authenticity | Covered | TR-SEC5-BP01 (Session timeout, secure connection, and cookie settings match data sensitivity) |
| SC-28 | Protection of Information at Rest | Covered | TR-REL7-BP01 (Backup data is encrypted, access-controlled, and inside the authorization boundary); TR-SEC7-BP03 (Encryption at rest beyond the platform default) |
| SC-39 | Process Isolation | Inherited | Process isolation is a platform responsibility. |

## SI: System and Information Integrity

| Control | Title | Status | WAR best practices / explanation |
|---|---|---|---|
| SI-1 | Policy and Procedures | Agency | The -1 control in each family is the policy and procedures requirement. The agency owns the policy; the governance plan is the platform-level procedure that implements it. |
| SI-2 | Flaw Remediation | Covered | TR-SEC15-BP02 (Third-party JavaScript libraries are inventoried, current, and free of known vulnerabilities) |
| SI-3 | Malicious Code Protection | Covered | TR-SEC13-BP04 (Uploaded files are restricted by type and size and scanned where possible) |
| SI-4 | System Monitoring | Covered | TR-COM2-BP02 (Continuous monitoring activities are defined and performed); TR-REL5-BP01 (Login, API, and integration activity is monitored); TR-REL5-BP02 (Alerts exist for failures that affect users or the business); TR-SEC9-BP04 (Real-time security event detection) |
| SI-5 | Security Alerts, Advisories, and Directives | Covered | TR-SEC16-BP02 (Security advisories and Trust notifications reach a named owner) |
| SI-7 | Software, Firmware, and Information Integrity | Inherited | Platform software integrity is a Salesforce responsibility; customer code integrity is addressed through source control under CM-2 and CM-3. |
| SI-8 | Spam Protection | Covered | TR-SEC11-BP04 (Outbound email does not carry more PII than necessary) |
| SI-10 | Information Input Validation | Covered | TR-SEC13-BP03 (Public intake forms validate input and collect the minimum); TR-SEC13-BP04 (Uploaded files are restricted by type and size and scanned where possible); TR-SEC14-BP01 (Session Settings browser protections are enabled and CSP and CORS allowlists are minimal); TR-SEC15-BP01 (Visualforce pages escape output and validate parameters); TR-SEC8-BP01 (Dynamic SOQL is parameterized or escaped); TR-SEC8-BP02 (LWC and Aura components avoid unsafe DOM and data exposure patterns) |
| SI-11 | Error Handling | Covered | TR-REL3-BP01 (Apex and Flow have defined error handling and surfacing); TR-SEC13-BP02 (Site security settings are hardened); TR-SEC15-BP03 (Errors shown to users do not leak internal detail) |
| SI-12 | Information Management and Retention | Covered | TR-COM4-BP01 (Records retention obligations are mapped to platform behavior); TR-COM4-BP02 (Right-to-deletion / data subject requests can be honored); TR-SEC12-BP02 (Debug logs and trace flags do not become a PII store) |
| SI-16 | Memory Protection | Inherited | Memory protection is a platform responsibility. |

## Summary

| Family | Controls | Covered | Inherited | Agency | Gap |
|---|---|---|---|---|---|
| AC | 17 | 15 | 1 | 1 | 0 |
| AU | 11 | 4 | 6 | 1 | 0 |
| CM | 12 | 11 | 0 | 1 | 0 |
| CP | 9 | 4 | 3 | 2 | 0 |
| IA | 10 | 5 | 3 | 2 | 0 |
| IR | 8 | 6 | 0 | 2 | 0 |
| SC | 18 | 10 | 7 | 1 | 0 |
| SI | 11 | 8 | 2 | 1 | 0 |

## Controls not covered by the WAR

Every customer-responsible control in the eight families maps to at least one WAR best practice. The controls without WAR coverage fall into two groups:

- **Inherited from Salesforce Government Cloud** (listed as Inherited above): the platform provides the control and the customer cannot configure it. The evidence is Salesforce's FedRAMP authorization package and the Customer Responsibility Matrix, not an org review.
- **Agency-owned** (listed as Agency above): the -1 policy controls, contingency training (CP-3), identity proofing (IA-12), and incident response assistance (IR-7). These are programs the agency runs; the governance plan documents where the platform team plugs into them.

Two caveats. The Inherited designations are this document's reading of the shared responsibility model and must be confirmed against the Customer Responsibility Matrix before they are relied on. And Covered means examined, not satisfied: the WAR findings and the controls catalog in the governance plan carry the evidence.
