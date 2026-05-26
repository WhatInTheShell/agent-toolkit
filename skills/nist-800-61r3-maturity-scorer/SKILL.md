---
name: nist-800-61r3-maturity-scorer
description: "Score an organization's IR program maturity against the NIST SP 800-61r3 CSF 2.0 Community Profile using a weighted scoring model tied to element priority (High/Medium/Low). Produces a per-function heatmap, weighted overall score, maturity level (1-5), and the highest-leverage improvement actions. Use when asked to 'score this against NIST', 'maturity assessment', 'how mature is our IR program', or 'NIST compliance score'."
user-invocable: true
---

# NIST SP 800-61r3 Maturity Scorer

Score an organization's IR program maturity against the complete CSF 2.0 Community Profile from NIST SP 800-61r3 (April 2025).

---

## Goal

Produce a quantitative maturity score grounded in SP 800-61r3's own priority system. High-priority elements (all Table 3 elements) have the most weight; Medium-priority elements (Table 2 selected) have moderate weight; Low-priority elements contribute minimally. Output a score, maturity level, per-function heatmap, and the top improvement actions by ROI.

---

## Inputs

- Coverage data from any of:
  - Raw document (will map inline)
  - Coverage map from `nist-800-61r3-csf-mapper`
  - Gap report from `nist-800-61r3-gap-analyzer`
  - Recommendation audit from `nist-800-61r3-recommendation-auditor`
  - Combined inputs from multiple documents (whole-program assessment)
- Assessment mode: **Document** (single doc) or **Program** (entire IR program across multiple docs)

---

## Workflow

```
1. Determine Element Coverage
   ↓
2. Apply Weighted Scoring Model
   ↓
3. Compute Per-Function Scores
   ↓
4. Compute Overall Weighted Score
   ↓
5. Assign Maturity Level
   ↓
6. Identify High-ROI Improvements
   ↓
7. Generate Maturity Report
```

### Step 1: Determine Element Coverage

For each SP 800-61r3 element, assign a coverage score:
- **1.0** — Fully addressed (evidence is explicit and complete)
- **0.5** — Partially addressed (element present but key sub-requirements missing)
- **0.0** — Not found or absent

If working from a raw document, perform inline mapping before scoring.

### Step 2: Weighted Scoring Model

SP 800-61r3's own priority system drives the weights:

| Priority | Source | Weight |
|----------|--------|--------|
| High     | Table 3 (all DE/RS/RC elements) | 3 |
| Medium   | Table 2 selected GV/ID/PR elements | 2 |
| Low      | Table 2 remaining GV/ID/PR elements | 1 |

**Score formula per function:**
```
Function_score = Σ(element_coverage × element_weight) / Σ(element_weight)
```

**Overall weighted score:**
```
Overall = Σ(all element_coverage × element_weight) / Σ(all element_weight)
```

### Step 3: SP 800-61r3 Element Registry with Weights

**HIGH WEIGHT (3) — Table 3 Elements**

| CSF ID | Weight | Description |
|--------|--------|-------------|
| DE.CM | 3 | Continuous Monitoring (parent) |
| DE.CM-01 | 3 | Network monitoring |
| DE.CM-02 | 3 | Physical environment monitoring |
| DE.CM-03 | 3 | Personnel activity monitoring |
| DE.CM-06 | 3 | External service provider monitoring |
| DE.CM-09 | 3 | Computing HW/SW/runtime monitoring |
| DE.AE | 3 | Adverse Event Analysis (parent) |
| DE.AE-02 | 3 | Events analyzed |
| DE.AE-03 | 3 | Information correlated from multiple sources |
| DE.AE-04 | 3 | Impact and scope estimated |
| DE.AE-06 | 3 | Info provided to authorized staff/tools |
| DE.AE-07 | 3 | CTI integrated into analysis |
| DE.AE-08 | 3 | Incident declaration criteria |
| RS.MA | 3 | Incident Management (parent) |
| RS.MA-01 | 3 | IR plan executed on declaration |
| RS.MA-02 | 3 | Incidents triaged and validated |
| RS.MA-03 | 3 | Incidents categorized and prioritized |
| RS.MA-04 | 3 | Incidents escalated/elevated |
| RS.MA-05 | 3 | Recovery initiation criteria applied |
| RS.AN | 3 | Incident Analysis (parent) |
| RS.AN-03 | 3 | Root cause established |
| RS.AN-06 | 3 | Investigation actions recorded with integrity |
| RS.AN-07 | 3 | Incident data collected with integrity |
| RS.AN-08 | 3 | Incident magnitude estimated |
| RS.CO | 3 | Incident Communication (parent) |
| RS.CO-02 | 3 | Stakeholders notified |
| RS.CO-03 | 3 | Information shared with stakeholders |
| RS.MI | 3 | Incident Mitigation (parent) |
| RS.MI-01 | 3 | Incidents contained |
| RS.MI-02 | 3 | Incidents eradicated |
| RC.RP | 3 | Recovery Plan Execution (parent) |
| RC.RP-01 | 3 | Recovery plan executed |
| RC.RP-02 | 3 | Recovery actions performed |
| RC.RP-03 | 3 | Backup integrity verified |
| RC.RP-04 | 3 | Critical functions considered post-incident |
| RC.RP-05 | 3 | Restored asset integrity verified |
| RC.RP-06 | 3 | Recovery declared, documentation completed |
| RC.CO | 3 | Recovery Communication (parent) |
| RC.CO-03 | 3 | Recovery progress communicated |
| RC.CO-04 | 3 | Public updates shared |

**MEDIUM WEIGHT (2) — Table 2 Selected**

| CSF ID | Weight |
|--------|--------|
| GV.RR | 2 |
| GV.RR-02 | 2 |
| GV.PO | 2 |
| GV.OC-03 | 2 |
| GV.SC-08 | 2 |
| GV.OV-01 | 2 |
| ID.RA-02 | 2 |
| ID.RA-05 | 2 |
| ID.RA-06 | 2 |
| ID.AM-01 | 2 |
| ID.AM-02 | 2 |
| ID.IM-01 | 2 |
| ID.IM-02 | 2 |
| ID.IM-03 | 2 |
| ID.IM-04 | 2 |
| PR.DS-11 | 2 |
| PR.PS-04 | 2 |

**LOW WEIGHT (1) — Table 2 Remaining**

All remaining GV, ID, PR elements not listed above (GV.OC-01/02/04/05, GV.RM-01–07, GV.RR-01/03/04, GV.PO-01/02, GV.OV-02/03, GV.SC-01–10, ID.AM-03–08, ID.RA-01/03/04/07/08/09/10, PR.AA, PR.AT, PR.DS, PR.PS, PR.IR)

### Step 4: Per-Function Scores

Compute a score for each of the 6 CSF Functions independently, using only the elements belonging to that function.

Convert to percentage and render a visual bar:
```
DE (Detect)  [████████░░]  80%
RS (Respond) [██████░░░░]  60%
RC (Recover) [████████░░]  80%
GV (Govern)  [██████░░░░]  55%
ID (Identify)[████░░░░░░]  45%
PR (Protect) [████░░░░░░]  40%
```

### Step 5: Maturity Level Assignment

Map the overall weighted score to a maturity level:

| Score | Level | Name | Characterization |
|-------|-------|------|-----------------|
| 0–29% | 1 | Initial | No consistent IR practices; ad hoc and reactive |
| 30–49% | 2 | Developing | Basic IR exists but is undocumented or inconsistently applied |
| 50–69% | 3 | Defined | Documented IR program exists; key processes established |
| 70–84% | 4 | Managed | Measured IR program; performance tracked; continuous improvement in place |
| 85–100% | 5 | Optimizing | IR integrated into all cybersecurity risk management; lessons feed back continuously |

These levels correspond loosely to CSF 2.0 Implementation Tiers 1–4 and the maturity concepts from ID.IM.

### Step 6: High-ROI Improvements

Identify the top 5 improvements with highest score impact:

For each Not Met or Partial element, compute:
- **Score uplift**: (1.0 - current_coverage) × weight / total_weighted_points
- **Dependencies unlocked**: how many other elements improve if this one is addressed

Rank by (score_uplift × 3) + (dependencies_unlocked × 2).

Common high-ROI improvements (based on typical IR programs):
1. **DE.AE-08** (incident declaration criteria) — weight 3; enables RS.MA-01 through RS.MA-05
2. **ID.IM-04** (IR plan maintenance) — weight 2; foundational for all Table 3 elements
3. **RS.AN-03** (root cause analysis) — weight 3; enables ID.IM-03 improvement loop
4. **RS.CO-02** (stakeholder notifications) — weight 3; legal/regulatory exposure reduction
5. **PR.PS-04** (log records) — weight 2; enables DE.AE-02/03/07 detection capabilities

### Step 7: Generate Maturity Report

---

## Output Format

```
╔══════════════════════════════════════════════════════════════════╗
║     NIST SP 800-61r3 IR Maturity Assessment                     ║
║     Standard: NIST SP 800-61r3 (April 2025), CSF 2.0            ║
╚══════════════════════════════════════════════════════════════════╝

Assessment Mode: [Document / Program]
Document(s): [list]
Assessment Date: [date]

━━━ MATURITY SCORE ━━━

Overall Weighted Score: 61%
┌─────────────────────────────┐
│  MATURITY LEVEL 3: DEFINED  │
│  Score range: 50–69%        │
└─────────────────────────────┘
Documented IR program exists with key processes established.
Gaps remain in continuous improvement loop and detection coverage.

━━━ PER-FUNCTION SCORES ━━━

Function     Coverage  Score  Bar
──────────── ───────── ────── ──────────────────────
DE (Detect)   11/14 el   74%  ████████████████░░░░░
RS (Respond)  15/25 el   58%  ████████████░░░░░░░░░
RC (Recover)  10/12 el   80%  ████████████████░░░░
GV (Govern)    9/18 el   50%  ██████████░░░░░░░░░░░
ID (Identify)  8/18 el   44%  █████████░░░░░░░░░░░░
PR (Protect)   7/15 el   47%  █████████░░░░░░░░░░░░

Strongest function:  RC (Recover) — 80%
Weakest function:    ID (Identify) — 44%
Table 3 (IR) score:  67%  ← primary operational readiness indicator
Table 2 (Prep) score: 47%  ← preparation and prevention readiness

━━━ ELEMENT COVERAGE DETAIL ━━━

High Priority (Table 3):  24/39 elements addressed (3 partial)
Medium Priority (Table 2): 9/17 elements addressed (2 partial)
Low Priority (Table 2):   11/24 elements addressed

━━━ TOP 5 HIGH-ROI IMPROVEMENTS ━━━

Rank  Element        Score Uplift  Dependencies  Action
────  ─────────────  ────────────  ────────────  ──────────────────────────────
 1    DE.AE-08        +3.2%         5 unlocked    Define incident declaration
                                                  criteria with false-positive
                                                  guidance
 2    RS.AN-03        +2.8%         3 unlocked    Implement RCA methodology
                                                  (5-Whys or fishbone) in all
                                                  AAR procedures
 3    ID.IM-04.R2     +1.6%         2 unlocked    Establish formal IR plan
                                                  review cycle (annual +
                                                  post-major-incident trigger)
 4    RS.CO-02.R3     +2.4%         0 unlocked    Document regulatory
                                                  notification obligations by
                                                  jurisdiction and sector
 5    PR.PS-04        +1.8%         4 unlocked    Implement centralized log
                                                  management covering all
                                                  SP 800-61r3 DE.CM asset types

Implementing all 5 would raise score to approximately 72% (Level 4: Managed).

━━━ BENCHMARKING ━━━

Level 3 (Defined) organizations typically:
✓ Have documented IR policies and procedures
✓ Have incident classification and triage processes
✗ Lack continuous improvement mechanisms
✗ Have gaps in detection coverage (DE elements)
✗ Do not systematically measure IR program performance

This assessment is consistent with a Level 3 organization.

━━━ TREND (if prior assessment available) ━━━
Prior score: N/A
Change: N/A
```

---

## Deliverable

A scored maturity report with function-level heatmap, maturity level assignment, and prioritized improvement roadmap. Suitable for:
- Executive reporting on IR program state
- Security program roadmap planning
- Board/leadership cybersecurity briefings
- Benchmarking across assessment cycles

---

## NEVER

- **NEVER report a score without showing the per-function breakdown** — an overall score without function detail masks where the real problems are
- **NEVER assign Maturity Level 4 or 5 without verifying the ID.IM improvement loop** — a program that doesn't measure itself cannot be Managed or Optimizing
- **NEVER use the score as a compliance checkbox** — maturity scores measure program capability, not regulatory compliance; explicitly state this limitation
- **NEVER round up partial coverage** — 0.5 is 0.5; a half-addressed element is not the same as a fully addressed one
