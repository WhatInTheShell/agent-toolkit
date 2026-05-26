---
name: nist-800-61r3-policy-reviewer
description: "Evaluate IR policy and procedure documents against NIST SP 800-61r3 Section 2.3 required policy elements and the GV.PO/GV.RR/ID.IM-04 CSF categories. Checks for all 8 required policy elements, role authority designations, and plan maintenance requirements. Use when asked to 'review this IR policy', 'check our incident response policy', 'is this policy complete', or 'policy completeness check'."
user-invocable: true
---

# NIST SP 800-61r3 Policy Reviewer

Evaluate IR policies, plans, and procedure documents against the requirements defined in NIST SP 800-61r3 Section 2.3 and the associated CSF 2.0 GV/ID elements.

---

## Goal

SP 800-61r3 Section 2.3 explicitly defines the required elements of an IR policy. This skill checks that a policy document contains all required elements, properly designates roles and authorities, and establishes the plan maintenance framework needed to stay current.

---

## Inputs

- The IR policy, IR plan, or procedures document to review (text or file path)
- Organization type (federal agency, private sector, MSSP) — affects regulatory notification requirements

---

## Workflow

```
1. Load Section 2.3 Policy Checklist
   ↓
2. Check 8 Required Policy Elements
   ↓
3. Check Roles & Authorities (GV.RR-02)
   ↓
4. Check Plan Framework (ID.IM-04)
   ↓
5. Check Shared Responsibility & Supply Chain (GV.SC-08)
   ↓
6. Generate Policy Review Report
```

### Step 1: Section 2.3 Policy Checklist

SP 800-61r3 §2.3 states that most IR policies include the same key elements. These are the required policy elements:

| # | Element | CSF Anchor |
|---|---------|-----------|
| 1 | Statement of management commitment | GV.RR-01 |
| 2 | Purpose and objectives of the policy | GV.PO |
| 3 | Scope of the policy (to whom/what it applies, under what circumstances) | GV.PO |
| 4 | Definition of events, cybersecurity incidents, investigations, and related terms | DE.AE-08 |
| 5 | Roles, responsibilities, and authorities (including who has authority to confiscate/disconnect/shut down assets) | GV.RR-02 |
| 6 | Guidelines for prioritizing incidents, estimating severity, initiating recovery, maintaining/restoring operations, and other key actions | RS.MA-03, RS.MA-05 |
| 7 | Performance measures | ID.IM-01 |
| 8 | Shared responsibility model with third parties (MSSPs, CSPs, ISPs) if applicable | GV.SC-08, GV.RR-02 |

### Step 2: Check 8 Required Policy Elements

For each element, determine:
- **Present** — policy explicitly addresses this element
- **Partial** — element is referenced but incomplete (e.g., roles listed but no authority designations)
- **Missing** — no evidence of the element

**Detailed checks per element:**

**Element 1 — Management Commitment**
- Is there a signed/dated endorsement from executive leadership?
- Does it reference resource allocation for IR?
- CSF: GV.RR-01 — "Organizational leadership is responsible and accountable for cybersecurity risk"

**Element 2 — Purpose and Objectives**
- Does the policy state why it exists?
- Does it reference reducing incident impact and improving response effectiveness?
- CSF: GV.PO

**Element 3 — Scope**
- Who does this apply to? (employees, contractors, third parties, specific systems)
- What environments are covered? (cloud, on-prem, OT/ICS, mobile)
- Are exclusions documented?
- CSF: GV.PO

**Element 4 — Definitions**
- Are "event," "adverse event," and "cybersecurity incident" defined per SP 800-61r3 Appendix B?
- Is "incident" distinguished from "event" — incidents jeopardize CIA of information or constitute policy violations
- Are investigation-related terms defined?
- CSF: DE.AE-08

**Element 5 — Roles, Responsibilities, and Authorities**
- Are incident response roles explicitly named (incident lead, handlers, legal, HR, comms, leadership)?
- Does the policy designate which roles have authority to:
  - Confiscate assets
  - Disconnect systems from the network
  - Shut down technology assets
- Are third-party roles (MSSP, CSP, law enforcement) addressed?
- CSF: GV.RR-02.R1, GV.RR-02.R2

**Element 6 — Prioritization, Severity, and Recovery Guidelines**
- Are incident severity/priority tiers defined (e.g., P1–P4 or Critical/High/Medium/Low)?
- Are risk evaluation factors listed? SP 800-61r3 RS.MA.N2 suggests: asset criticality, functional impact, data impact, stage of observed activity, threat actor characterization, recoverability
- Are recovery initiation criteria defined? (RS.MA-05.R1)
- Are time-based response SLAs included?
- CSF: RS.MA-03.R1, RS.MA-05.R1

**Element 7 — Performance Measures**
- Are IR program performance metrics defined?
- Examples: mean time to detect, mean time to respond, mean time to recover, % incidents meeting SLAs, % staff trained
- Is there a review cycle for measuring performance against these metrics?
- CSF: ID.IM-01.R1 — "Periodically evaluate IR program performance to identify problems"

**Element 8 — Shared Responsibility Model**
- If the organization uses MSSPs/CSPs/ISPs: are their responsibilities documented?
- Are contracts/SLAs referenced?
- Are information flow and coordination authorities defined?
- Are restrictions on third-party actions documented (e.g., cannot share sanitized incident info with other customers)?
- CSF: GV.SC-08, GV.RR-02.R3

### Step 3: Roles & Authorities Deep Check (GV.RR-02)

Check specifically for GV.RR-02.R1, R2, R3:

**R1 — All IR roles documented in organizational policies:**
- [ ] Incident Response Team / SOC roles documented
- [ ] Legal counsel role in IR documented
- [ ] HR role documented (GV.RR-02 + RS.CO-03.R3)
- [ ] Public affairs / media relations role documented
- [ ] Physical security and facilities role documented
- [ ] Asset owners role documented
- [ ] Leadership decision authority documented

**R2 — All appropriate individuals designated the authority to fulfill IR responsibilities:**
- [ ] Named or role-titled individuals with authority to isolate/disconnect systems
- [ ] Named or role-titled individuals with authority to invoke business continuity plans
- [ ] Named or role-titled individuals with authority to engage law enforcement
- [ ] Escalation/elevation triggers and authority chain documented (RS.MA-04)

### Step 4: Plan Framework Check (ID.IM-04)

SP 800-61r3 ID.IM-04 has four recommendations for all cybersecurity plans:

- **R1** — Synchronize business continuity plans with incident response plans
  - Check: Does the policy reference BCP/DRP alignment?
- **R2** — Review and update all cybersecurity plans periodically or when significant improvements are identified
  - Check: Is there a review/update cycle defined? (Annual, post-incident trigger?)
- **R3** — Base each plan on the organization's unique requirements, mission, size, structure, and functions
  - Check: Is the policy tailored to the org or clearly a generic template?
- **R4** — Each plan identifies the resources and management support needed
  - Check: Are resource requirements (staff, tools, budget) referenced?

### Step 5: Regulatory & Notification Check (GV.OC-03)

Based on organization type, verify the policy addresses applicable notification requirements:

**GV.OC-03.R1** — Cybersecurity requirements include all IR-related requirements (incident notification, data breach reporting)

Check:
- [ ] Notification obligations referenced (FISMA, HIPAA, PCI-DSS, GDPR, state breach laws — as applicable)
- [ ] Breach notification timelines addressed (RS.CO-02.R3)
- [ ] Law enforcement notification criteria defined (RS.CO-02.R5)
- [ ] Regulatory body notification criteria defined

### Step 6: Generate Policy Review Report

---

## Output Format

```
=== NIST SP 800-61r3 IR Policy Review ===
Document: [policy name/version]
Organization type: [federal / private / MSSP]
Standard: NIST SP 800-61r3 §2.3 + CSF 2.0 GV/ID elements

━━━ SECTION 2.3 REQUIRED ELEMENTS CHECKLIST ━━━

[✓] Element 1 — Management Commitment
    Found: Executive VP signature, dated 2025-01-15; §1.1
    Note: Does not reference specific resource commitments (FTE, budget)

[✗] Element 4 — Definitions
    Missing: "Event" and "adverse event" are not defined.
    The policy uses "incident" broadly without distinguishing security events
    from confirmed cybersecurity incidents per FISMA 2014 definition.
    Required by: DE.AE-08, SP 800-61r3 Appendix B
    Fix: Add a definitions section with SP 800-61r3 Appendix B terms at minimum.

[~] Element 5 — Roles, Responsibilities, and Authorities
    Partial: Roles listed (IR Team, Legal, HR) but authority to disconnect
    systems is not designated to any specific role.
    Required by: GV.RR-02.R2 — "All appropriate individuals should be
    designated the authority necessary to fulfill their IR responsibilities"
    Fix: Add explicit authority table specifying who can isolate/disconnect/
    shut down each asset class.

[✓] Element 6 — Prioritization Guidelines
    Found: Four-tier severity model (P1-P4) with response SLAs; §3.2
    Note: Recovery initiation criteria (RS.MA-05.R1) are absent — policy
    defines when to start responding but not when to start recovering.

[✗] Element 7 — Performance Measures
    Missing: No IR performance metrics defined anywhere in the document.
    Required by: ID.IM-01.R1
    Fix: Define at minimum: MTTD, MTTR, % incidents within SLA,
    % staff completing IR training annually.

━━━ ROLES & AUTHORITIES (GV.RR-02) ━━━
[✓] IR Team roles documented
[✓] Legal counsel role documented
[~] HR role referenced but not scoped for insider threat (RS.CO-03.R3)
[✗] Physical security role not mentioned
[✗] No named authority to invoke BCP/DRP during incident

━━━ PLAN FRAMEWORK (ID.IM-04) ━━━
[~] R1 — BCP alignment mentioned in passing, not formally linked (§1.4)
[✓] R2 — Annual review cycle defined (§6.1)
[✗] R3 — Document appears to be a generic template; lacks org-specific context
[~] R4 — "Resources as needed" language present but no specifics

━━━ REGULATORY/NOTIFICATION (GV.OC-03) ━━━
[~] Notification obligations referenced but no specific laws cited
[✗] No breach notification timelines defined

━━━ SUMMARY ━━━
Present:  4 / 8 required elements fully addressed
Partial:  2 / 8 elements partially addressed
Missing:  2 / 8 required elements absent

Critical gaps: Element 4 (definitions) and Element 7 (performance measures)
Policy assessment: Not ready for operational use without addressing critical gaps.
Estimated effort to remediate: LOW — most gaps are additions, not rewrites.
```

---

## Deliverable

A checklist-based policy review report with element-by-element findings, direct SP 800-61r3 citations, and specific remediation guidance. Suitable for:
- IR policy audit findings
- Input to `nist-800-61r3-maturity-scorer`
- Policy revision task list

---

## NEVER

- **NEVER accept "implied" policy elements** — if an element is not explicit in the document, it is Missing
- **NEVER skip the authority designations check** — GV.RR-02.R2 is one of the most commonly missed requirements
- **NEVER recommend creating a separate document for each gap** — all elements should be in the policy; suggest additions to the existing document
- **NEVER skip the definitions check** — undefined terms (especially "event" vs. "incident") cause real operational confusion during actual incidents
