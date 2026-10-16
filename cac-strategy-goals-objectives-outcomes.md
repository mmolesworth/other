# CAC Strategy, Goals, Objectives, and Outcomes

**Status:** v1.1, 2026-10-02 (v1.0 same day; v1.1 moves Verified security to Goal 1 and extends the period to five sprints)
**Supersedes:** `cac-foundation-goals-and-objectives.md` (September draft, three-outcome structure)
**Companion to:** the roadmap doc "CAC Foundation Roadmap, 8-Week Plan" (Strategy tab holds the same content; Sprint plan tab holds the sprint-by-goal matrix); `cac-governance-plan-outline.md` (the governance plan is the vehicle for several objectives; cross-map pending)
**Framework:** project custom instructions (strategy → goals → objectives → outcomes → initiatives and outputs)

## Strategy: CAC foundation for safe, predictable change

### Diagnosis

Three changes that are hard to reverse are coming to the CAC: the Lightning platform upgrade, backup and recovery, and the move from custom data components to standard ones. Each depends on understanding a system nobody fully understands, and the system must keep handling consumer complaints while they happen.

It is not understood because a decade of hand-built customization replaced capabilities Salesforce now provides, the documents describe the intended design rather than what was built, and the critical context lives in individuals. It cannot be changed safely because there are no tests tied to business behavior, deployments go by changeset with no record or rollback, the three environments have drifted apart, and the O&M plan asserts controls that cannot be verified.

The evidence is the incident: personal information was exposed and no control detected it. The cost of each coming initiative is a guess for the same reason. The alternatives, "modernize now" or "fix the findings," both act on the system without the visibility to size the work or the means to test it. The binding constraint is knowledge and control, not technology.

### Guiding policy

Make the system visible and make change controlled before making the system different. Two thrusts: one authoritative, version-controlled picture of the as-built system, with its security verified against the NIST 800-53 controls the incident implicates; and one path to production that tests business behavior, leaves a record, and can be recovered from. Scope each cycle to what the three coming changes need. Build on today's system whatever the upgrade will not redo; fold the rest into the upgrade.

**Planning period:** October 8 to December 16, 2026 (five two-week sprints). Owner is Mark unless noted.

## Goal 1. Verified security

The security of the CAC is known rather than assumed: every control it relies on can be checked, and every known weakness has an owner and a decision.

### 1.1 Establish the security posture of the CAC against the in-scope NIST 800-53 controls, with evidence recorded for each control.

- When OCIO or the ISSO asks whether a control is in place, the answer is the evidence on file, not an assurance.
- Each in-scope control has a stated status (in place, partly in place, not in place) with the evidence behind it.
- Gaps found by the review are ranked by severity and assigned an owner before anyone starts fixing them, so effort goes to the highest risk first.

### 1.2 Establish who has access to the CAC and at what level, with every user, administrator, and integration account justified.

- Every active account traces to a person or a system and a business reason, and any that cannot is disabled.
- Anyone who asks who can change production gets a list of named accounts, each justified, not an estimate.
- Integration accounts run under their own credentials, not a person's.

### 1.3 Proactively resolve security vulnerabilities in the CAC's code before each release, with the Salesforce Code Analyzer run on every change and every high-severity finding remediated or formally accepted.

- No change reaches production with an unaddressed high-severity finding from the analyzer.
- Vulnerabilities in the code are found by the team's own analysis before the security team's scan reports them.
- Outdated JavaScript libraries, including the current jQuery references, are detected on every change rather than found by the scanner after the fact.

### 1.4 Establish the process for granting, changing, and removing access to the CAC, with user permissions reviewed on a defined schedule.

- Every access change has a requester and an approver on record.
- When someone leaves or changes role, their access is removed or adjusted within the agreed window rather than left in place.
- Each scheduled permission review leaves a record of what was found and what was changed.

### 1.5 Establish the process for receiving, triaging, and dispositioning security vulnerabilities reported by the security team, with each finding tracked to remediation, formal acceptance, or documented false positive.

- Every finding the security team reports has an owner and a disposition within the agreed triage window, and nothing sits unassigned.
- A false positive is closed once, with a documented and cited reason, and is not reopened on the next scan cycle.
- The security team can see the status of every finding they reported without asking the team.

## Goal 2. One picture of the system

Everyone who decides about, builds, or operates the CAC works from one authoritative, maintained record of how the system is actually built.

### 2.1 Establish a field-by-field baseline of the 17 most-used data objects, recorded as a source-to-target mapping: what each field holds, whether it contains personal information, and where it is used.

- From November 4, the team answers questions about what a field holds, whether it contains personal information, and what depends on it from the record, without querying production or asking whoever built it.
- The international address recommendation (3.4) and the security review of data-protection controls (1.1) take their facts about the 17 objects from the baseline rather than from fresh investigation.

### 2.2 Identify which of the CAC's data objects are obsolete or no longer in use, with the evidence for each.

- Every recommendation to retire or archive an object is backed by its record count, last activity, and usage references, and nothing is retired without them.
- The case for retiring each obsolete object goes to OCFP as a decision to approve, with the record count, last activity, and evidence of non-use attached, rather than as a question for them to investigate.

### 2.3 Establish current, team-verified diagrams of how the CAC is built and what it connects to.

- The restore order for the backup exercise (4.2) is taken from the diagrams rather than worked out during the exercise.
- The security review of integrations and external access (1.1) works from the diagrams' integration list rather than from memory.
- Any change touching an integration is checked against the diagrams before release.

### 2.4 Establish one source-controlled record of the system's metadata, environments, and certificates.

- When a change is questioned, the team shows what changed and when from the repository history, not from recollection.
- Before any deployment, the team knows which components differ between the target environment and production.
- Certificate renewals are scheduled ahead of expiry instead of being discovered by an outage.

## Goal 3. Controlled change, delivered

OCFP's requested changes continue to be delivered on the current system, each through one controlled path that proves the change does what the business needs and records what was done.

### 3.1 Establish the deployment pipeline as the only path for the team's production changes.

- From November 4, every production change the team makes is deployed from the repository through the pipeline; nothing goes in by changeset or by editing production directly.
- Any production deployment can be traced to what changed, who approved it, and when, from the pipeline record alone.
- A change that fails its checks stops before production instead of being discovered there.

### 3.2 Establish a suite of business test cases, agreed with OCFP, that runs before every release.

- No release reaches production until the test cases for the processes it touches have passed.
- A change that breaks something the business depends on is caught by the test cases before release rather than by a user after it.
- OCFP can read a test result and know what was verified, because the cases are written in the business terms they agreed to.

### 3.3 Establish a predictable turnaround for OCFP's approved modification requests, from approval to release in production.

- OCFP is given a release date when a modification request is approved, and the release lands on or before it.
- The time from approval to production is recorded for every request in the period, so the next cycle has a measured baseline instead of an estimate.

### 3.4 Establish a recommended approach for international address support, with the options compared, for OCFP's decision.

- OCFP receives a comparison of the international address options covering effort, impact on existing data, and rework risk under the upgrade, with a recommended option, by November 18.
- The recommendation states which options the upgrade would redo, so the build-now-or-wait decision can be made with that known.

## Goal 4. Recoverable

The CAC can be restored to a known good state after a bad change or an incident, and that capability has been demonstrated.

### 4.1 Establish automatic backup of production with the OWN backup solution, on an agreed scope and schedule.

- Production data and configuration are backed up on the agreed schedule without anyone starting it.
- A failed backup is noticed from an alert and acted on the same day, rather than discovered when a restore is needed.
- Anyone who asks what would be lost if production failed today gets an answer in hours of data, not a guess.

### 4.2 Prove that a restore works by restoring into a sandbox and documenting the steps.

- The time a restore takes and the order the objects must be restored in are known from the exercise rather than estimated.
- A team member who did not run the first exercise can restore a set of records into a sandbox by following the written steps.
- A restore no longer risks re-firing emails or automation, because the steps to suppress and re-enable them are part of the written procedure.

## Sprint plan by goal (in progress)

Five two-week sprints: S1 10/8 to 10/21, S2 10/22 to 11/4, S3 11/5 to 11/18, S4 11/19 to 12/2, S5 12/3 to 12/16. Federal holidays: Columbus Day 10/12 (S1), Veterans Day 11/11 (S3), Thanksgiving 11/26 (S4). One week of Mark's absence falls in the window, dates to be set.

| Sprint | 1. Verified security | 2. One picture of the system | 3. Controlled change, delivered | 4. Recoverable |
|---|---|---|---|---|
| S1 | | | | Prepare the backup service: license, service account, scope, owners. |
| S2 | | | | Turn on automatic production backups with failure alerts. |
| S3 | | | | Restore sample data into a test environment and document the steps. |
| S4 | | | | Repeat the restore from the written steps and tune the schedule. |
| S5 | | | | |

Goal 4 activities were derived from the Salesforce Backup & Recover help structure (setup and permissions, services, scheduling, retention and exclusions, restore application, Smart Alerts, weekly report, compare and find). Open check: confirm cross-org restore into a sandbox is supported under the agency's license before S3.

## Decisions recorded 2026-10-02

- Strategy kept to diagnosis and guiding policy; trade-offs, source of advantage, major moves, assumptions, and stakeholder response dropped by Mark's choice for this exercise.
- Two June goals (See the System, Control the Change) replaced by four. "Controlled change" and "customer requests" combined into one goal at Mark's direction. Recovery and security given their own goals.
- Verified security moved to Goal 1 (priority); others renumbered: One picture of the system 2, Controlled change 3, Recoverable 4.
- "In-scope NIST 800-53 controls" means the seven families the incident implicates: AC, AU, CM, CP, IR, SC, SI. The well-architected review is the method, not the standard named in the objective.
- Goal 1 (security) carries five objectives, one over the two-to-four guideline, intentionally.
- Dates appear only where an objective or outcome needs one; dates dependent on OCFP or on OWN enablement were removed.
- The governance plan (O&M plan revision) is the vehicle for several objectives rather than an objective itself; recovery targets and the restore-test cadence belong in it.
- Outcomes are written as the behaviors the objective enables, not as completion measures.
- Planning period extended from four sprints (ending 12/2) to five (ending 12/16) for holidays and a week of absence.
- Sprint tabs in the roadmap doc replaced by one sprint-by-goal matrix, to be filled in together; cells are concise activity statements for non-technical management.

## Resume Here

- v1.1 captures the strategy, four goals (security first), 15 objectives, outcomes, and the Goal 4 column of the sprint matrix as agreed 2026-10-02.
- Next: fill the matrix columns for Goals 1, 2, and 3; cross-map the objectives to the governance plan outline; align the roadmap doc's Overview, activity table, and timeline drawing to the four goals (they still use the two June goals and the "Baseline, Review, Tests, Governance" workstream names).
- Not yet done: owners other than Mark; the final per-goal table (Objective, Owner, Outcome, Metric, Baseline, Target, Target date, Data source, Guardrail) called for in the custom instructions, since metrics and baselines were deliberately left out of this pass.
