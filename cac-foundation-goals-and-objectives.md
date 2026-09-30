# CAC Foundation: Goals and Objectives

**Status:** Draft v0.1, 2026-09-18
**Companion to:** `cac-foundation-roadmap-draft.md`

Three outcomes organize the work. Each has one goal (the end state) and a set of objectives (verifiable conditions that show the goal is met).

## Know what we have

**Goal:** One authoritative, maintained picture of the system that every stakeholder works from, replacing knowledge that lives in individuals.

**Objectives**

- Every component in the inventory is tied to the business process it serves, or flagged as unused.
- Every object and field that holds PII is identified.
- Environments, their drift from production, and the refresh history are documented in one record.
- Certificates are registered with expiration dates and owners.
- License counts, usage, and utilization are reported.
- A target data architecture exists that states which custom objects and fields map to standard equivalents and what waits for modernization.
- The record is under version control and has a defined refresh cadence.

## Close the exposure

**Goal:** Known security gaps are closed or formally accepted, the system can be recovered, and no data is retained longer than policy requires.

**Objectives**

- Open findings from the incident are resolved, with each disposition documented.
- Controls in the scoped NIST 800-53 families (AC, AU, CM, CP, IR, SC, SI) are assessed with evidence, and gaps are ranked in one list with owners.
- The system is rated against the Salesforce Well-Architected Framework, and findings feed the same gap list.
- Backup is live and a restore has been exercised and documented.
- A retention policy is adopted and every object has an approved disposition: retain, archive, or delete.
- Unused components are identified with evidence and removed or scheduled for removal.

## Control how it changes

**Goal:** Every change to production is source-controlled, tested against what the business needs, and traceable, and the operating plan describes how the system actually runs.

**Objectives**

- All production deployments go through the pipeline; changesets are retired.
- A security fix has reached production through the pipeline, gated by tests.
- Business-driven test cases exist for critical processes and run before every release.
- Environments are refreshed on a defined strategy, and at least one refresh has been executed under it.
- The O&M plan is revised so each claim about deployment, monitoring, backup, recovery, incident handling, and retention is verifiable.
- A standing review cadence is set for the inventory, the architecture review, certificates, and licenses.

## Open items

- "Changesets are retired" requires OCIO agreement that no one bypasses the pipeline. If not winnable in this window, soften to "all changes from this team go through the pipeline."

## Resume Here

- v0.1 captures goals and objectives as agreed 2026-09-18.
- Next: confirm the changeset objective with OCIO; align objective wording with the client-facing version of the roadmap.
