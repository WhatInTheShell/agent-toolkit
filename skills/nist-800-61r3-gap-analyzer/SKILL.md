---
name: nist-800-61r3-gap-analyzer
description: "Identify prioritized gaps in any cybersecurity document against the NIST SP 800-61r3 CSF 2.0 Community Profile. Accepts raw document content or a coverage map from nist-800-61r3-csf-mapper and outputs a priority-ranked gap list (High/Medium/Low) with specific SP 800-61r3 citation anchors. Use when asked to 'find gaps in this IR plan', 'what's missing from this playbook', or 'gap analysis against 800-61r3'."
user-invocable: true
---

# NIST SP 800-61r3 Gap Analyzer

Identify and prioritize gaps in any cybersecurity document against the CSF 2.0 Community Profile defined in NIST SP 800-61r3 (April 2025).

---

## Goal

Produce a prioritized gap list — sorted High → Medium → Low — for every CSF 2.0 element from SP 800-61r3 that is missing or incomplete in the reviewed document. Each gap includes the SP 800-61r3 citation, the specific requirement not met, and a remediation suggestion.

---

## Inputs

- The document to analyze (text, file path, or description), OR
- A coverage map previously produced by `nist-800-61r3-csf-mapper`
- Document type (if not already classified)

---

## Workflow

```
1. Obtain Coverage Map (run mapper if not already done)
   ↓
2. Load SP 800-61r3 Element Baseline
   ↓
3. Identify Gaps
   ↓
4. Classify & Prioritize
   ↓
5. Generate Gap Report
```

### Step 1: Obtain Coverage Map

If a coverage map exists from `nist-800-61r3-csf-mapper`, use it directly. Otherwise, perform inline mapping against the document before gap analysis.

### Step 2: SP 800-61r3 Element Baseline

The complete element set from SP 800-61r3, organized by priority:

**HIGH PRIORITY — Table 3 (Incident Response)**

| CSF ID     | Description |
|------------|-------------|
| DE         | Detect Function |
| DE.CM      | Continuous Monitoring |
| DE.CM-01   | Networks/network services monitored |
| DE.CM-02   | Physical environment monitored |
| DE.CM-03   | Personnel activity and technology usage monitored |
| DE.CM-06   | External service provider activities monitored |
| DE.CM-09   | Computing HW/SW/runtime/data monitored |
| DE.AE      | Adverse Event Analysis |
| DE.AE-02   | Events analyzed to understand associated activities |
| DE.AE-03   | Information correlated from multiple sources |
| DE.AE-04   | Estimated impact and scope of adverse events understood |
| DE.AE-06   | Information on adverse events provided to authorized staff/tools |
| DE.AE-07   | CTI and contextual information integrated into analysis |
| DE.AE-08   | Incidents declared when adverse events meet incident criteria |
| RS         | Respond Function |
| RS.MA      | Incident Management |
| RS.MA-01   | IR plan executed on incident declaration |
| RS.MA-02   | Incident reports triaged and validated |
| RS.MA-03   | Incidents categorized and prioritized |
| RS.MA-04   | Incidents escalated or elevated as needed |
| RS.MA-05   | Recovery initiation criteria applied |
| RS.AN      | Incident Analysis |
| RS.AN-03   | Root cause and event sequence established |
| RS.AN-06   | Investigation actions recorded with integrity |
| RS.AN-07   | Incident data/metadata collected with integrity preserved |
| RS.AN-08   | Incident magnitude estimated and validated |
| RS.CO      | Incident Reporting and Communication |
| RS.CO-02   | Internal and external stakeholders notified |
| RS.CO-03   | Information shared with designated stakeholders |
| RS.MI      | Incident Mitigation |
| RS.MI-01   | Incidents contained |
| RS.MI-02   | Incidents eradicated |
| RC         | Recover Function |
| RC.RP      | Incident Recovery Plan Execution |
| RC.RP-01   | Recovery portion of IR plan executed |
| RC.RP-02   | Recovery actions selected, scoped, prioritized, performed |
| RC.RP-03   | Backup/restoration asset integrity verified |
| RC.RP-04   | Critical mission functions considered post-incident |
| RC.RP-05   | Restored asset integrity verified, normal status confirmed |
| RC.RP-06   | End of incident recovery declared, documentation completed |
| RC.CO      | Incident Recovery Communication |
| RC.CO-03   | Recovery activities/progress communicated to stakeholders |
| RC.CO-04   | Public updates shared using approved methods/messaging |

**MEDIUM PRIORITY — Table 2 (selected high-value elements)**

| CSF ID     | Description |
|------------|-------------|
| GV.OC-03   | Legal, regulatory, contractual requirements understood |
| GV.RR      | Roles, responsibilities, authorities established |
| GV.RR-02   | Roles/responsibilities documented and enforced |
| GV.PO      | Organizational cybersecurity policy established |
| GV.OV-01   | Risk management strategy outcomes reviewed |
| GV.SC-08   | Relevant suppliers included in IR planning/response |
| ID.AM-01   | HW inventories maintained |
| ID.AM-02   | SW/services inventories maintained |
| ID.RA-02   | CTI received from sharing forums/sources |
| ID.RA-05   | Threats/vulns/likelihoods used to inform risk response |
| ID.RA-06   | Risk responses chosen, tracked, communicated |
| ID.IM-01   | Improvements identified from evaluations |
| ID.IM-02   | Improvements from security tests and exercises |
| ID.IM-03   | Improvements from operational execution |
| ID.IM-04   | IR plans established, maintained, improved |
| PR.DS-11   | Backups created, protected, maintained, tested |
| PR.PS-04   | Log records generated for continuous monitoring |

**LOW PRIORITY — Table 2 (informational)**

All remaining GV, ID, PR elements not listed above.

### Step 3: Identify Gaps

For each element in the baseline, determine its status in the coverage map:
- `Not Found` → Gap
- `Partial` → Partial Gap (flag as gap with lower severity modifier)
- `Addressed` → No gap

### Step 4: Classify & Prioritize

For each gap, assign:

**Severity** (for High-priority elements):
- **Critical**: Element is absent and directly impacts incident handling (RS.MA-02, DE.AE-08, RS.AN-03, RS.MI-01, RC.RP-06)
- **Significant**: Element is absent but has workarounds or is partially covered
- **Minor**: Partial coverage that needs strengthening

**Gap type**:
- **Missing**: No evidence of the element
- **Incomplete**: Element addressed but key sub-requirements absent

### Step 5: Generate Gap Report

---

## Output Format

```
=== NIST SP 800-61r3 Gap Analysis Report ===
Document: [name/type]
Standard: NIST SP 800-61r3 (April 2025)
Analysis date: [date]

━━━ CRITICAL GAPS (High Priority — Table 3) ━━━

[C1] DE.AE-08 — Incident Declaration Criteria
     Status: Missing
     Requirement: "Apply incident criteria to known and assumed characteristics
     of analyzed activity, and consider known false positives to determine
     whether an incident should be declared." (DE.AE-08.R1)
     Impact: Without defined declaration criteria, incident response may start
     too late or on false positives — undermining RS.MA-02 triage.
     Remediation: Define specific observable thresholds (e.g., confirmed C2
     beacon, lateral movement detected, data staged for exfil) that constitute
     an incident declaration trigger.

[C2] RS.MA-02 — Incident Triage and Validation
     Status: Partial (severity categories present, no urgency criteria)
     Requirement: "Perform a preliminary review of a new incident report to
     verify that a cybersecurity incident has occurred, then estimate the
     severity and urgency needed to respond to it." (RS.MA-02.R1)
     Impact: Severity tiers exist but no time-based urgency criteria — teams
     cannot determine response SLAs.
     Remediation: Add urgency criteria alongside severity (e.g., P1 = respond
     within 1hr, P2 = 4hr, P3 = 24hr).

...

━━━ SIGNIFICANT GAPS (High Priority) ━━━

[S1] RS.CO-02 — Stakeholder Notification
     ...

━━━ MEDIUM PRIORITY GAPS (Table 2) ━━━

[M1] ID.IM-04 — IR Plans Maintained and Improved
     ...

━━━ SUMMARY ━━━

Critical gaps:    3  (must address before next incident)
Significant gaps: 5  (address within 30 days)
Minor gaps:       4  (address in next program review cycle)
Medium gaps:      6
Low gaps:         2

Highest-impact single fix: Adding DE.AE-08 incident declaration criteria would
immediately improve RS.MA-02, RS.MA-03, and RS.MA-04 effectiveness.
```

---

## Deliverable

A prioritized, citation-anchored gap report suitable for:
- Direct input to `nist-800-61r3-maturity-scorer`
- Action items for IR program improvement backlog
- Audit findings documentation

---

## NEVER

- **NEVER mark a gap as Critical unless it is in Table 3 AND directly impacts incident handling**
- **NEVER suggest remediation that adds bureaucracy** — all suggestions should be practical, not compliance theater
- **NEVER conflate Missing with Partial** — partial coverage is progress; acknowledge what exists
- **NEVER omit citation anchors** — every finding must cite the specific CSF ID and R/C/N item from SP 800-61r3
