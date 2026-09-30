# CAC Governance Plan: Outline

**Status:** Draft v0.1, 2026-09-18
**Replaces:** The security, version control and deployment, incident management, and monitoring sections of the existing O&M Plan
**Companion to:** `cac-foundation-roadmap-draft.md`, `cac-foundation-goals-and-objectives.md`

## Design principle

The plan states governance: decision rights, controls, risks, and cadences. Step-by-step procedures live in separate runbooks the plan references. This keeps the plan short enough to maintain and ensures every claim in it can be verified. The June 2026 presentation identified the current O&M plan's core weakness as assertions that are inaccurate or cannot be confirmed; separating governance from procedure is the structural fix.

## 1. Governance structure

- Roles: system owner (OCIO), business owner (OCFP), ISSO, Salesforce admin, developer, records officer, contractor team.
- Decision rights: who approves a release, an emergency change, a new user, a permission change, a data export, a sandbox refresh.
- Meeting cadence and the decisions each meeting makes.
- RACI for the controls in section 10.

## 2. Environment management

- Inventory of orgs and sandboxes: purpose, type, who has access.
- Production as source of truth.
- Refresh strategy: cadence, trigger events, what is refreshed, post-refresh steps.
- Alignment to the three Salesforce releases per year and sandbox preview windows; at least one sandbox previews each release before production receives it.
- PII in sandboxes: Data Mask is not licensed. State what is actually done (partial copy, manual scrub, or accepted risk).

Runbooks referenced: sandbox refresh, post-refresh configuration, release preview testing.

## 3. Change and release management

- Pipeline as the only path to production. Changesets retired (or scoped to this team if OCIO will not commit further).
- Branching, code review, test gates, deployment windows.
- Rollback approach: redeploy prior commit. State plainly that some metadata types cannot be rolled back this way.
- Emergency change path with after-the-fact review.
- Destructive changes process.
- Release readiness: release notes review, preview testing, known-issue tracking.

Runbooks referenced: deployment, emergency change, destructive change, release readiness checklist.

## 4. Access control

- Least privilege through permission sets rather than profiles.
- MFA: how it is enforced.
- Login IP ranges and session settings.
- Integration user accounts on Integration licenses; never a person's credentials.
- Admin account governance.
- Joiner, mover, leaver process.
- Periodic access review with defined frequency.

Runbooks referenced: user provisioning and deprovisioning, access review.

## 5. Security configuration and monitoring

- Health Check: baseline score, target score, review cadence.
- Setup Audit Trail and Login History review cadence.
- Monitoring limits stated plainly: Shield is not licensed, so Event Monitoring and Field Audit Trail are not available.
- Certificate register, rotation, expiry alerting.
- Salesforce Trust status subscription.
- Vulnerability management: scanner cadence, triage process, disposition categories (remediate, accept, documented false positive with primary-source citation).

Runbooks referenced: Health Check review, audit trail review, certificate rotation, scanner triage.

## 6. Data governance

- PII inventory by object and field.
- Field-level security and sharing model baseline.
- Data classification metadata on fields (available without Shield).
- Retention policy and disposition schedule (retain, archive, delete) by object.
- Rules for data exports and sandbox data.

Runbooks referenced: data export, retention disposition.

## 7. Backup and recovery

- OWN scope and schedule.
- RPO and RTO targets (currently open).
- Restore order derived from the business process map.
- Restore test cadence.
- Metadata recovery via the repository.
- Automation suppression steps during restore.

Runbooks referenced: restore, restore test.

## 8. Incident management

- Detection sources, given the monitoring limits in section 5.
- Roles and escalation, including agency incident response and PII breach reporting obligations.
- Salesforce support escalation path.
- Post-incident review feeding the risk register.

Runbooks referenced: incident response.

## 9. Risk register

- Format: risk, likelihood, impact, owner, treatment, status.
- Seeded from the consolidated gap list (well-architected review, NIST 800-53 scoped assessment, incident findings).
- Review cadence.

## 10. Controls catalog

The core of the plan. One row per control:

| Control statement | How verified | Frequency | Evidence location | Owner | NIST family |
|---|---|---|---|---|---|

This turns "the system is secure" into something checkable. Every control in sections 2 through 8 appears here.

## 11. Licensing and capacity

- License utilization review cadence.
- Storage, API, and other platform limits with thresholds and owners.

## 12. Plan maintenance

- Plan under version control alongside the component inventory.
- Review triggers: each Salesforce release, any incident, annually at minimum.

## Salesforce guidance mapping

| Section | Primary source |
|---|---|
| 2 | [Sandbox Types and Management Best Practices](https://help.salesforce.com/s/articleView?id=000387743&language=en_US&type=1); [Sandbox Preview Instructions](https://help.salesforce.com/s/articleView?id=000391927&language=en_US&type=1) |
| 3 | Development Lifecycle and Deployment Architect exam guide (project files) |
| 4 | [Security Implementation Guide: Login IP Ranges](https://developer.salesforce.com/docs/atlas.en-us.securityImplGuide.meta/securityImplGuide/login_ip_ranges.htm); [Session Security Settings](https://help.salesforce.com/s/articleView?language=en_US&id=admin_sessions.htm&type=5) |
| 4–8 | [Well-Architected: Trusted](https://architect.salesforce.com/well-architected/trusted/overview) ([Secure](https://architect.salesforce.com/well-architected/trusted/secure), [Compliant](https://architect.salesforce.com/well-architected/trusted/compliant), [Resilient](https://architect.salesforce.com/docs/architect/well-architected/guide/resilient.html)) |
| 10 | NIST SP 800-53 Rev. 5, scoped families AC, AU, CM, CP, IR, SC, SI |

## Open questions

- Does the existing O&M plan follow a required agency or contract template? If so, this structure must fit inside it.
- Will OCIO commit to retiring changesets org-wide, or only for this team?
- RPO and RTO targets need a decision from OCFP.

## Resume Here

- v0.1 captures the section outline as agreed 2026-09-18.
- Next: confirm template constraints; draft the controls catalog rows for sections 2 through 8; identify which runbooks already exist vs. need writing.
