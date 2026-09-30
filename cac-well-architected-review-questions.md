# CAC Well-Architected Review: Questions by Domain

| # | Domain | Description | Questions | NIST families |
|---|---|---|---|---|
| 1 | Identity and access | Who can log in, how they authenticate, what privileges they hold, and how duties are separated. | 5 | AC, CM, IA, SC |
| 2 | External exposure and integration | Everything reachable without an internal login: guest users, sites, public forms, Connected Apps, APIs, packages, and the authorization boundary. | 5 | AC, CM, IA, SC, SI |
| 3 | Data protection | Where PII lives, who can see it, and every path by which it leaves the sharing model. This is where the incident occurred; its findings feed the retention and data architecture decisions. | 5 | AC, AU, CM, IA, SC, SI |
| 4 | Application security | Custom code and Classic-era customizations: Apex, Visualforce, Lightning components, third-party libraries, input validation, error handling, and platform limits. | 4 | AC, SC, SI |
| 5 | Logging, monitoring, and detection | What is recorded, who reviews it, what alerts exist, and how advisories reach the team. Stated within the limits of an org without Shield. | 4 | AU, CM, IR, SI |
| 6 | Change and configuration management | How change reaches production: pipeline, source control, drift, impact analysis, deploy access, least functionality, and unused customization. | 5 | AC, CM |
| 7 | Resilience and recovery | Backup, restore, continuity, incident response, reporting obligations, and knowledge concentration. | 5 | AC, CM, CP, IR, SC |
| 8 | Compliance and governance | Obligations, the Customer Responsibility Matrix, evidence, continuous monitoring, accessibility, policy, and architectural strategy. | 5 | AU, SI |
| 9 | Maintainability and usability | Easy-pillar and composability questions not driven by the security incident. Run last or defer to the next cycle. | 6 | — |

## Domain 1: Identity and access

Who can log in, how they authenticate, what privileges they hold, and how duties are separated.

### TR-SEC 1. How do you manage identity and access for users and automated processes?

- TR-SEC1-BP01: Least-privilege profile and permission set design
- TR-SEC1-BP02: Org-wide defaults and sharing model are deliberately set
- TR-SEC1-BP03: User lifecycle is managed (provisioning, deprovisioning, review)

### TR-SEC 2. How do you control privileged access?

- TR-SEC2-BP01: System Administrator access is restricted to a small, documented set of users
- TR-SEC2-BP02: Integration and API-only users use dedicated accounts with minimum scope
- TR-SEC2-BP03: Break-glass / emergency access is defined and controlled

### TR-SEC 4. How do you authenticate users?

- TR-SEC4-BP01: MFA is enforced for all interactive logins
- TR-SEC4-BP02: SSO, if used, is configured securely
- TR-SEC4-BP03: Password policy meets FedRAMP Moderate expectations

### TR-SEC 5. How do you control sessions and network access?

- TR-SEC5-BP01: Session timeout, secure connection, and cookie settings match data sensitivity
- TR-SEC5-BP02: Login IP ranges and login hours are configured for sensitive profiles
- TR-SEC5-BP03: Mobile access is governed

### TR-SEC 10. How do you separate duties across administration, development, and deployment?

- TR-SEC10-BP01: Change authors, approvers, and deployers are different people
- TR-SEC10-BP02: A system use notification is displayed at login

## Domain 2: External exposure and integration

Everything reachable without an internal login: guest users, sites, public forms, Connected Apps, APIs, packages, and the authorization boundary.

### TR-SEC 13. How do you control public and guest access?

- TR-SEC13-BP01: Guest user profiles hold the minimum permissions and sharing
- TR-SEC13-BP02: Site security settings are hardened
- TR-SEC13-BP03: Public intake forms validate input and collect the minimum
- TR-SEC13-BP04: Uploaded files are restricted by type and size and scanned where possible

### TR-SEC 3. How do you manage Connected Apps and API access?

- TR-SEC3-BP01: Connected Apps are inventoried and scoped minimally
- TR-SEC3-BP02: Credentials for outbound integrations are stored in Named Credentials or External Credentials

### TR-SEC 14. How do you harden browser-facing security settings?

- TR-SEC14-BP01: Session Settings browser protections are enabled and CSP and CORS allowlists are minimal
- TR-SEC14-BP02: Outbound email from the org is authenticated

### TR-COM 3. How do you handle the FedRAMP authorization boundary as the org changes?

- TR-COM3-BP01: Changes that may affect the authorization boundary are reviewed before deployment
- TR-COM3-BP02: Installed packages and integrations are inventoried and reviewed periodically

### AD-CMP 2. How do you make integrations clean and reusable?

- AD-CMP2-BP01: Integrations follow consistent patterns
- AD-CMP2-BP02: Custom Apex APIs are versioned and documented
- AD-CMP2-BP03: Platform Events and Change Data Capture are used where they fit

## Domain 3: Data protection

Where PII lives, who can see it, and every path by which it leaves the sharing model. This is where the incident occurred; its findings feed the retention and data architecture decisions.

### TR-SEC 6. How do you enforce field-level and object-level access?

- TR-SEC6-BP01: Field-level security restricts sensitive fields appropriately
- TR-SEC6-BP02: Apex enforces sharing, CRUD, and FLS

### TR-SEC 7. How do you protect data at rest and in transit?

- TR-SEC7-BP01: Sensitive data is classified and inventoried
- TR-SEC7-BP02: Encryption in transit uses current TLS
- TR-SEC7-BP03: Encryption at rest beyond the platform default
- TR-SEC7-BP04: Certificates and keys are inventoried, owned, and rotated before expiry

### TR-SEC 11. How do you control the surfaces through which data leaves the sharing model?

- TR-SEC11-BP01: Report and dashboard folders are shared deliberately and dashboards run as an appropriate user
- TR-SEC11-BP02: List views on PII-bearing objects are not visible to all users unnecessarily
- TR-SEC11-BP03: Files and attachments cannot be exposed through public links or over-broad sharing
- TR-SEC11-BP04: Outbound email does not carry more PII than necessary
- TR-SEC11-BP05: Bulk export capability is limited and inventoried

### TR-SEC 12. How do you protect production data outside production?

- TR-SEC12-BP01: Production PII in sandboxes is masked, minimized, or access-restricted
- TR-SEC12-BP02: Debug logs and trace flags do not become a PII store

### TR-COM 4. How do you manage records retention and deletion?

- TR-COM4-BP01: Records retention obligations are mapped to platform behavior
- TR-COM4-BP02: Right-to-deletion / data subject requests can be honored

## Domain 4: Application security

Custom code and Classic-era customizations: Apex, Visualforce, Lightning components, third-party libraries, input validation, error handling, and platform limits.

### TR-SEC 8. How do you secure custom code beyond sharing/FLS?

- TR-SEC8-BP01: Dynamic SOQL is parameterized or escaped
- TR-SEC8-BP02: LWC and Aura components avoid unsafe DOM and data exposure patterns

### TR-SEC 15. How do you secure Visualforce and Classic-era customizations?

- TR-SEC15-BP01: Visualforce pages escape output and validate parameters
- TR-SEC15-BP02: Third-party JavaScript libraries are inventoried, current, and free of known vulnerabilities
- TR-SEC15-BP03: Errors shown to users do not leak internal detail

### TR-REL 2. How do you stay ahead of governor limits and platform constraints?

- TR-REL2-BP01: API and async limit usage is monitored against allocation
- TR-REL2-BP02: Apex and SOQL respect bulk patterns and governor limits

### TR-REL 3. How do you handle errors and failures in automation and integrations?

- TR-REL3-BP01: Apex and Flow have defined error handling and surfacing
- TR-REL3-BP02: Inbound and outbound integrations have retry, idempotency, and timeout handling
- TR-REL3-BP03: Asynchronous failures (Queueable, Batch, Platform Events) are detected and handled

## Domain 5: Logging, monitoring, and detection

What is recorded, who reviews it, what alerts exist, and how advisories reach the team. Stated within the limits of an org without Shield.

### TR-SEC 9. How do you detect security events and maintain an audit trail?

- TR-SEC9-BP01: Setup Audit Trail is exported and reviewed on a defined cadence
- TR-SEC9-BP02: Field History Tracking is enabled on sensitive fields
- TR-SEC9-BP03: Long-term audit retention beyond 18 months
- TR-SEC9-BP04: Real-time security event detection

### TR-SEC 16. How do you protect and act on security records and advisories?

- TR-SEC16-BP01: Exported audit records are protected and retained
- TR-SEC16-BP02: Security advisories and Trust notifications reach a named owner

### TR-REL 1. How do you know the org is healthy?

- TR-REL1-BP01: Salesforce Health Check is run and tracked
- TR-REL1-BP02: Salesforce Optimizer is run and reviewed

### TR-REL 5. How do you observe what the org is doing in production?

- TR-REL5-BP01: Login, API, and integration activity is monitored
- TR-REL5-BP02: Alerts exist for failures that affect users or the business

## Domain 6: Change and configuration management

How change reaches production: pipeline, source control, drift, impact analysis, deploy access, least functionality, and unused customization.

### TR-REL 6. How do you manage environments and releases?

- TR-REL6-BP01: Sandbox strategy supports the release cadence
- TR-REL6-BP02: Releases follow a defined process with rollback capability

### AD-RES 1. How do you manage the application lifecycle from change to production?

- AD-RES1-BP01: A defined CI/CD or release pipeline moves changes from source to production
- AD-RES1-BP02: Apex test coverage is meaningful, not just sufficient
- AD-RES1-BP03: Metadata source-of-truth conflicts are detected

### AD-RES 4. How do you analyze and restrict changes before they reach production?

- AD-RES4-BP01: Security impact analysis precedes production changes
- AD-RES4-BP02: Production change access is restricted to the pipeline and a minimal set of admins
- AD-RES4-BP03: Unused platform features and settings are disabled
- AD-RES4-BP04: A configuration management plan names the baseline, roles, and change process

### AD-CMP 3. How do you package and deploy customizations as cohesive units?

- AD-CMP3-BP01: Metadata is grouped into deployable units that match logical boundaries
- AD-CMP3-BP02: Managed package dependencies are inventoried and governed

### EZ-INT 2. How do you keep the customization surface maintainable?

- EZ-INT2-BP01: Unused customization is identified and removed
- EZ-INT2-BP02: Workflow Rules and Process Builder are migrated to Flow
- EZ-INT2-BP03: Naming conventions and metadata hygiene are enforced

## Domain 7: Resilience and recovery

Backup, restore, continuity, incident response, reporting obligations, and knowledge concentration.

### TR-REL 4. How do you back up and recover org data and metadata?

- TR-REL4-BP01: A current data backup capability exists and is tested
- TR-REL4-BP02: Metadata is version-controlled and recoverable independently of the org

### TR-REL 7. How do you protect the backup copy itself?

- TR-REL7-BP01: Backup data is encrypted, access-controlled, and inside the authorization boundary

### AD-RES 2. How do you respond to incidents?

- AD-RES2-BP01: A documented incident response process exists and is exercised
- AD-RES2-BP02: Salesforce-specific incident escalation paths are known

### AD-RES 5. How do you meet incident reporting obligations?

- AD-RES5-BP01: Reporting obligations and timelines are defined for security and PII incidents

### AD-RES 3. How do you plan for continuity beyond individual incidents?

- AD-RES3-BP01: Business continuity assumptions about Salesforce are documented and tested
- AD-RES3-BP02: Knowledge of the org is not concentrated in one person

## Domain 8: Compliance and governance

Obligations, the Customer Responsibility Matrix, evidence, continuous monitoring, accessibility, policy, and architectural strategy.

### TR-COM 1. How do you identify and track the regulatory and contractual obligations that apply to this org?

- TR-COM1-BP01: Applicable obligations are inventoried and assigned an owner
- TR-COM1-BP02: The Customer Responsibility Matrix (CRM) is reviewed and acted on

### TR-COM 2. How do you maintain evidence that customer-responsible controls are implemented?

- TR-COM2-BP01: Evidence for each customer-responsible control is current and accessible
- TR-COM2-BP02: Continuous monitoring activities are defined and performed

### TR-COM 5. How do you meet accessibility obligations?

- TR-COM5-BP01: Custom UI meets Section 508 / WCAG 2.1 AA
- TR-COM5-BP02: Salesforce VPATs for the in-use products are obtained and reviewed

### TR-COM 6. How do you manage ethical and policy-driven obligations beyond regulation?

- TR-COM6-BP01: Internal data-use and ethics policies are reflected in platform configuration

### EZ-INT 1. How do you maintain a clear architectural strategy for the org?

- EZ-INT1-BP01: A current architectural overview exists
- EZ-INT1-BP02: Build-vs-configure decisions follow a defined heuristic

## Domain 9: Maintainability and usability

Easy-pillar and composability questions not driven by the security incident. Run last or defer to the next cycle.

### EZ-INT 3. How do you keep automation and code readable?

- EZ-INT3-BP01: Apex follows a documented style and structure
- EZ-INT3-BP02: Flows are structured for readability

### EZ-AUT 1. How do you automate routine work efficiently?

- EZ-AUT1-BP01: Manual administrative work has been identified and reduced
- EZ-AUT1-BP02: Automation overlaps and conflicts are mapped

### EZ-AUT 2. How do you keep data clean and trustworthy?

- EZ-AUT2-BP01: Validation rules enforce data quality at entry
- EZ-AUT2-BP02: Duplicate management rules are configured and active
- EZ-AUT2-BP03: Data cleanup runs as a defined process, not as crisis response

### EZ-ENG 1. How do you keep the user experience focused and efficient?

- EZ-ENG1-BP01: Page layouts and Lightning record pages match how users actually work
- EZ-ENG1-BP02: Navigation and app structure match user mental models

### EZ-ENG 2. How do you help users succeed in the moment?

- EZ-ENG2-BP01: In-app guidance is used where it reduces support load
- EZ-ENG2-BP02: Error messages and validation feedback are useful to the user

### AD-CMP 1. How do you keep concerns separated in the org?

- AD-CMP1-BP01: Apex follows a layered structure (service / selector / domain / trigger handler)
- AD-CMP1-BP02: Automation responsibility per object is consolidated and clear
