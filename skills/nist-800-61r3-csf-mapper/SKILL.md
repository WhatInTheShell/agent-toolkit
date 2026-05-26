---
name: nist-800-61r3-csf-mapper
description: "Map content from any cybersecurity document (playbook, IR plan, policy, incident report) to NIST SP 800-61r3 CSF 2.0 elements. Produces a coverage table showing which Functions, Categories, and Subcategories are addressed, partially addressed, or absent. Use when asked to 'map this to NIST', 'what CSF elements does this cover', or 'tag this against 800-61r3'."
user-invocable: true
---

# NIST SP 800-61r3 CSF Mapper

Map any cybersecurity document to the CSF 2.0 Community Profile defined in NIST SP 800-61r3 (April 2025).

---

## Goal

Produce a structured coverage table that shows which CSF 2.0 elements from the SP 800-61r3 Community Profile are:
- **Addressed** — content explicitly satisfies the element
- **Partial** — content touches the element but incompletely
- **Not Found** — element is absent from the document

---

## Inputs

- The document to analyze (paste text, provide file path, or describe it)
- Document type (ask if not obvious): IR Plan, Playbook, Incident Report, After-Action Report, IR Policy, Risk Assessment, Other

---

## Workflow

```
1. Classify Document
   ↓
2. Determine Relevant CSF Scope
   ↓
3. Scan & Tag Content
   ↓
4. Build Coverage Table
   ↓
5. Output Summary
```

### Step 1: Classify Document

Identify the document type before mapping — different types have different expected coverage profiles:

| Document Type        | Primary CSF Scope Expected |
|----------------------|---------------------------|
| IR Plan              | GV.PO, GV.RR, ID.IM-04, RS (all), RC (all) |
| Playbook             | RS.MA, RS.AN, RS.MI, DE.AE-08, RC.RP |
| Incident Report      | RS.MA, RS.AN, RS.CO, RS.MI, RC.RP |
| After-Action Report  | RS.AN-03, RS.AN-06/07, RC.RP-06, ID.IM-03 |
| IR Policy            | GV.PO, GV.RR, ID.IM-04 (§2.3 elements) |
| Risk Assessment      | ID.RA (all), GV.RM, ID.AM |

### Step 2: Determine Relevant CSF Scope

SP 800-61r3 defines two tables:

**Table 2 — Preparation & Lessons Learned** (GV, ID, PR):
- GV: Govern (GV.OC, GV.RM, GV.RR, GV.PO, GV.OV, GV.SC)
- ID: Identify (ID.AM, ID.RA, ID.IM)
- PR: Protect (PR.AA, PR.AT, PR.DS, PR.PS, PR.IR)

**Table 3 — Incident Response** (DE, RS, RC) — all elements are High priority:
- DE: Detect (DE.CM, DE.AE)
- RS: Respond (RS.MA, RS.AN, RS.CO, RS.MI)
- RC: Recover (RC.RP, RC.CO)

For most documents, focus first on Table 3 elements (all High priority), then Table 2.

### Step 3: Scan & Tag Content

Read the document and for each meaningful section/paragraph:
1. Identify which CSF Subcategory it most closely satisfies
2. Assess completeness: does it fully satisfy the element or only partially?
3. Note the source location (section number, paragraph, or quote)

**Key semantic anchors** — phrases that signal specific CSF elements:

| If document mentions...                        | Maps to          |
|------------------------------------------------|------------------|
| Continuous monitoring, anomaly detection       | DE.CM            |
| Incident declaration criteria, threshold       | DE.AE-08         |
| Triage, severity assessment, validate          | RS.MA-02         |
| Incident categorization, incident type         | RS.MA-03         |
| Escalation, elevation, resource increase       | RS.MA-04         |
| Recovery initiation criteria                   | RS.MA-05         |
| Root cause analysis, event sequence            | RS.AN-03         |
| Evidence collection, chain of custody          | RS.AN-07         |
| Incident magnitude, IoC scope                  | RS.AN-08         |
| Stakeholder notification, breach notification  | RS.CO-02         |
| Information sharing, ISAC, threat intel share  | RS.CO-03         |
| Containment, isolate, quarantine               | RS.MI-01         |
| Eradication, persistence removal, patch        | RS.MI-02         |
| Recovery plan execution, restore operations    | RC.RP-01/02      |
| Backup integrity, clean restore verification   | RC.RP-03/05      |
| After-action report, lessons learned           | RC.RP-06, ID.IM-03 |
| IR policy, policy elements                     | GV.PO, ID.IM-04  |
| Roles, responsibilities, authority             | GV.RR-02         |

### Step 4: Build Coverage Table

Output a table with these columns:

| CSF ID | Priority | Description (brief) | Coverage | Evidence/Location |
|--------|----------|---------------------|----------|-------------------|

Coverage values: `Addressed` / `Partial` / `Not Found`

Group by Function: DE → RS → RC (Table 3 first), then GV → ID → PR (Table 2).

Only include elements that are relevant to the document type (skip Low-priority Table 2 elements unless the document explicitly covers them).

### Step 5: Output Summary

After the table, provide:
1. **Coverage counts**: X/Y High-priority elements addressed
2. **Top gaps**: The 3–5 most significant missing elements by priority
3. **Document type assessment**: Does the coverage match what's expected for this document type?

---

## Output Format

```
=== CSF 2.0 Coverage Map — [Document Name/Type] ===
Standard: NIST SP 800-61r3 (April 2025)
Document Type: [classified type]

TABLE 3 — INCIDENT RESPONSE (All High Priority)
────────────────────────────────────────────────────────────────────────
CSF ID      | Description                              | Coverage    | Location
────────────────────────────────────────────────────────────────────────
DE.CM       | Continuous monitoring of assets          | Partial     | §2.1
DE.CM-01    | Network monitoring                       | Addressed   | §2.1.a
DE.CM-09    | Computing HW/SW/runtime monitoring       | Not Found   | —
DE.AE       | Adverse event analysis                   | Partial     | —
DE.AE-02    | Events analyzed to understand activity   | Addressed   | §3.2
DE.AE-08    | Incident declaration criteria            | Not Found   | —
RS.MA       | Incident management                      | Partial     | §4
RS.MA-01    | IR plan executed on incident declaration | Addressed   | §4.1
RS.MA-02    | Incidents triaged and validated          | Partial     | §4.2 (no severity criteria)
...

TABLE 2 — PREPARATION & LESSONS LEARNED (Mixed Priority)
[only elements relevant to document type]
...

SUMMARY
────────
High-priority (Table 3) coverage: 9/23 elements addressed, 5 partial, 9 not found
Medium-priority coverage: 4/12 addressed
Top gaps: DE.AE-08 (incident criteria), RS.MA-02 (triage), RS.AN-03 (root cause), RS.CO-02 (notifications), RC.RP-06 (after-action)
Assessment: Coverage is below expected for an IR Plan — RS.CO and RC sections are largely absent.
```

---

## Deliverable

A coverage table + summary that can be handed directly to `nist-800-61r3-gap-analyzer` for prioritized gap analysis or to `nist-800-61r3-maturity-scorer` for scoring.

---

## NEVER

- **NEVER invent coverage** — only mark Addressed if the document explicitly addresses the element
- **NEVER skip Table 3** — all DE/RS/RC elements are High priority; always include them
- **NEVER use SP 800-61r2 element IDs** — this skill maps to r3/CSF 2.0 IDs only (no legacy "Preparation → Detection & Analysis" phases)
- **NEVER map vague language to specific elements** — "we monitor our systems" alone does not satisfy DE.CM-01 through DE.CM-09 individually
