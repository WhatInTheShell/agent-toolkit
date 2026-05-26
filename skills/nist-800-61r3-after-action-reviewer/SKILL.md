---
name: nist-800-61r3-after-action-reviewer
description: "Evaluate post-incident reports, after-action reports (AARs), and lessons-learned documents against NIST SP 800-61r3's post-incident activity requirements — specifically RS.AN-03, RS.AN-06/07/08, RC.RP-06, and ID.IM-03. Checks root cause completeness, evidence integrity, magnitude validation, stakeholder communications, recovery verification, and whether lessons are actionable. Use when asked to 'review this after-action report', 'evaluate our lessons learned', or 'post-incident review check'."
user-invocable: true
---

# NIST SP 800-61r3 After-Action Reviewer

Evaluate post-incident reports, after-action reports (AARs), and lessons-learned documents against NIST SP 800-61r3 (April 2025) post-incident requirements.

---

## Goal

SP 800-61r3 defines rigorous requirements for what an after-action report must contain and how the lessons-learned process feeds back into IR program improvement. This skill checks that an AAR captures everything the standard requires — not just "what happened" but "how we know," "what we missed," and "what we're changing."

---

## Inputs

- The after-action report, post-incident report, or lessons-learned document (text or file path)
- Incident type (data breach, ransomware, account takeover, DoS, insider, etc.) — affects scope
- Was this a major incident? (affects whether senior leadership update requirements apply)

---

## Workflow

```
1. Check RC.RP-06 — After-Action Report Completeness
   ↓
2. Check RS.AN-03 — Root Cause Analysis Quality
   ↓
3. Check RS.AN-06/07/08 — Evidence & Records Integrity
   ↓
4. Check RS.CO-02/03 — Communication Retrospective
   ↓
5. Check RC.RP-04/05 — Recovery Verification
   ↓
6. Check ID.IM-03 — Lessons-Learned Loop Closure
   ↓
7. Generate AAR Review Report
```

### Step 1: RC.RP-06 — After-Action Report Completeness

**RC.RP-06.R1** states: "Prepare an after-action report that documents the incident itself, the response and recovery actions taken, and lessons learned."

Check that the AAR contains all three mandated components:

**Component A — The Incident**
- [ ] Incident type and classification (per RS.MA-03 categorization)
- [ ] Initial detection method and timestamp (links to DE.AE)
- [ ] Timeline of significant events from first indicator to recovery completion
- [ ] Systems, data, and services affected
- [ ] Estimated or confirmed impact (financial, operational, reputational, regulatory)
- [ ] Threat actor characterization if known (TTPs, attribution confidence)

**Component B — Response and Recovery Actions**
- [ ] Triage and validation actions (RS.MA-02)
- [ ] Incident management decisions and rationale (RS.MA-03, RS.MA-04)
- [ ] Containment measures applied (RS.MI-01)
- [ ] Eradication actions taken (RS.MI-02)
- [ ] Recovery steps executed in order (RC.RP-02, RC.RP-04)
- [ ] Recovery completion declaration (RC.RP-06)
- [ ] Notifications sent (RS.CO-02, RS.CO-03) with timestamps and recipients

**Component C — Lessons Learned**
- [ ] What worked well
- [ ] What did not work or was delayed
- [ ] Root cause(s) — not just proximate cause but systemic (see Step 2)
- [ ] Specific, assignable improvement actions (not vague "improve monitoring")
- [ ] Owner and deadline for each improvement action
- [ ] Which CSF Function each improvement targets

### Step 2: RS.AN-03 — Root Cause Analysis Quality

SP 800-61r3 RS.AN-03 requires four specific analysis activities:

**RS.AN-03.R1** — "Determine the sequence of events that have occurred during the incident and which assets and resources were involved in each of those events."
- Check: Is there a complete, timestamped event sequence?
- Check: Are affected assets enumerated at each stage?
- Gap signal: Report says "attacker gained access" without explaining the full chain

**RS.AN-03.R2** — "Determine what vulnerabilities, threats, and threat actors were directly or indirectly involved in the incident."
- Check: Is the specific vulnerability or misconfiguration that enabled the incident identified?
- Check: Are indirect enablers noted (e.g., missing MFA, stale accounts, excessive permissions)?
- Gap signal: Report blames "phishing" without identifying which controls failed or were absent

**RS.AN-03.R3** — "Analyze the incident to find the underlying or systemic root causes."
- Check: Does the AAR go beyond the proximate cause (the exploit/vector) to systemic causes?
- Systemic cause examples: patch management failure, training gap, monitoring blind spot, inadequate access controls, architectural weakness
- Technique check: Was a 5-Whys or fishbone analysis performed?
- Gap signal: Report identifies root cause as "an employee clicked a phishing link" — this is a proximate cause, not systemic

**RS.AN-03.R4** — "Check any deployed cyber deception technology for additional information on attacker behavior."
- Check: If honeypots, deception tokens, or canary files were deployed — were they checked?
- Mark N/A if no deception technology is deployed

### Step 3: RS.AN-06/07/08 — Evidence & Records Integrity

**RS.AN-06.R1** — "Safeguard the confidentiality and integrity of incident response records; ensure only authorized personnel have access."
- Check: Does the AAR reference how IR records were protected?
- Check: Is there a statement about who had access to incident data?
- Note: The incident lead is responsible for records safeguarding

**RS.AN-07.R1** — "Collect and retain evidence per evidence preservation procedures and data retention policies; consider factors including the possibility of prosecution."
- Check: Were forensic images, logs, or artifacts collected and documented?
- Check: Is there reference to chain of custody procedures?
- Check: Was prosecution possibility considered and documented?
- Check: Are retention timelines for collected evidence noted?

**RS.AN-08.R1** — "Look for indicators of compromise, evidence of persistence, and other signs of an incident on both the assets known to be targeted and other potential targets."
- Check: Was the incident scope validated beyond the initially identified systems?
- Check: Were adjacent/related assets checked for IoCs?
- Check: Was persistence mechanism identified and confirmed removed?
- Gap signal: Report addresses only initially identified host without checking lateral spread

### Step 4: RS.CO-02/03 — Communication Retrospective

Review whether required notifications were actually performed:

**RS.CO-02.R2** — "Follow established procedures concerning incident coordination: what must be reported, to whom, and at what times."
- Check: Were all required internal notifications made (leadership, legal, HR, asset owners)?
- Check: Were notification timestamps documented?

**RS.CO-02.R3** — "Perform notifications in compliance with incident notification laws/regulations."
- Check: Were regulatory/legal notification obligations triggered?
- Check: If triggered, were they met within required timeframes?
- Check: Is there documentation of the notification decision (even if decided not required)?

**RS.CO-02.R5** — "Notify law enforcement and regulatory bodies per criteria in IR plan."
- Check: Was law enforcement notification considered and decision documented?

**RS.CO-03.R2** — "Regularly update senior leadership on status of major incidents."
- Check (major incidents only): Were senior leadership updates provided during the incident?
- Check: Is there a log of leadership communications?

### Step 5: RC.RP-04/05 — Recovery Verification

**RC.RP-04.R1** — "Validate that essential services are restored in the appropriate order."
- Check: Does the AAR document the restoration sequence?
- Check: Were critical services restored before non-critical?

**RC.RP-04.R2** — "Work with system owners to confirm successful restoration and return to normal operations."
- Check: Did system owners sign off on recovery?
- Check: Is there documentation of owner confirmations?

**RC.RP-04.R3** — "Monitor performance of restored systems to verify adequacy of restoration."
- Check: Was there a post-recovery monitoring period?
- Check: Were any anomalies detected post-restoration?

**RC.RP-05.R1** — "Check restored assets for IoCs; remediate root causes before production use."
- Check: Were restored systems scanned for IoCs before going back online?
- Check: Were root causes remediated before production restoration?

**RC.RP-05.R2** — "Verify correctness and adequacy of restoration actions before putting restored system online."
- Check: Was there a pre-production verification step?

### Step 6: ID.IM-03 — Lessons-Learned Loop Closure

**ID.IM-03.N3** — "Creating follow-up reports or holding 'lessons learned' meetings when an incident's recovery efforts are concluding, especially if the incident was major."

**ID.IM-03.N2** — "Improvements that affect IR can be made to the IR program itself (plan, policy, procedures) or to other aspects of cybersecurity risk management (e.g., identifying TTPs not currently blocked by safeguards or flagged by detection technologies)."

Check:
- [ ] Was a lessons-learned meeting held? (attendees, date documented?)
- [ ] Do improvement actions target IR program changes (not just technical fixes)?
- [ ] Do any lessons feed back to Preparation (GV, ID, PR functions)?
- [ ] Are improvement actions SMART (Specific, Measurable, Assignable, Realistic, Time-bound)?
- [ ] Is there a tracking mechanism for improvement actions?

**Lessons-captured vs. lessons-actionable assessment:**
- Count total lessons identified
- Count lessons with assigned owner AND deadline
- Ratio = actionability score

---

## Output Format

```
=== NIST SP 800-61r3 After-Action Review ===
Document: [AAR name/incident reference]
Incident type: [ransomware / data breach / etc.]
Severity: [major / significant / minor]
Standard: NIST SP 800-61r3 (April 2025)

━━━ RC.RP-06 — AFTER-ACTION REPORT COMPLETENESS ━━━

Component A — Incident Documentation
[✓] Incident type and classification: Present (§1)
[✓] Detection method and timestamp: Present (§2.1 — DE alert at 14:23 UTC)
[~] Event timeline: Partial — gaps between 16:00–19:00 UTC unexplained
[✗] Threat actor characterization: Missing — vector identified but no TTP analysis
Gap: RC.RP-06.R1 requires documenting the incident itself; threat actor info
needed for ID.IM-03 improvement loop.

Component B — Response and Recovery Actions
[✓] Triage and validation: Present (§3)
[✓] Containment measures: Present (§4.1)
[✗] Recovery steps: Missing — report notes systems restored but no sequence
documented. RC.RP-04.R1 requires restoration order validation.

Component C — Lessons Learned
[~] What worked: Present (§7)
[✗] Actionable improvements: 3 lessons identified, 0 have assigned owners or
deadlines. ID.IM-03 requires SMART improvement actions.

━━━ RS.AN-03 — ROOT CAUSE ANALYSIS ━━━

[✓] R1 — Event sequence: Complete timeline from initial access to containment
[~] R2 — Vulnerability identification: Phishing vector identified; no analysis
of why MFA bypass was possible or why the phishing email bypassed email filtering
[✗] R3 — Systemic root cause: Report identifies "employee clicked phishing link"
as root cause — this is proximate, not systemic. No 5-Whys or structural analysis.
Gap: Missing analysis of: why MFA was not enforced on this account class,
why email filtering did not catch this variant, whether this reflects a pattern.
[N/A] R4 — No deception technology deployed per §1.3

━━━ RS.AN-06/07/08 — EVIDENCE & RECORDS ━━━
[✓] RS.AN-06.R1 — IR records access control referenced (§6.2)
[~] RS.AN-07.R1 — Evidence collected but no retention timeline documented
[✗] RS.AN-08.R1 — Scope validation missing: no evidence adjacent systems
were checked for lateral movement or IoC presence

━━━ RS.CO COMMUNICATIONS RETROSPECTIVE ━━━
[✓] Internal notifications made with timestamps (§5.1)
[~] RS.CO-02.R3 — Regulatory notification decision not documented (HIPAA
applicability not assessed in AAR)
[✓] RS.CO-03.R2 — Senior leadership received 3 updates during incident

━━━ RC.RP RECOVERY VERIFICATION ━━━
[~] RC.RP-04.R2 — System owner confirmations: verbal only, not documented
[✗] RC.RP-05.R1 — No pre-production IoC scan of restored systems documented

━━━ ID.IM-03 — LESSONS LEARNED LOOP ━━━
Lessons identified: 3
Lessons with owner + deadline: 0
Actionability score: 0% — all lessons are observations, none are assigned actions

━━━ SUMMARY ━━━
Critical gaps: RS.AN-03.R3 (systemic root cause), RC.RP-05.R1 (IoC scan),
              ID.IM-03 actionability (no assigned owners)
Significant gaps: RS.AN-08.R1 (scope validation), RC.RP-04.R2 (owner sign-off)
Assessment: AAR captures what happened but will not improve the IR program.
The absence of systemic root cause analysis means the same incident is likely
to recur. The 0% actionability on lessons learned means no improvements will
be tracked or implemented.
```

---

## Deliverable

A section-by-section AAR review with citation-anchored findings, a lessons-actionability score, and specific improvement recommendations. Suitable for:
- IR program quality assurance
- Compliance audit support
- AAR revision guidance
- Input to `nist-800-61r3-maturity-scorer`

---

## NEVER

- **NEVER accept proximate cause as root cause** — "user clicked a link" is never a root cause; the systemic failure enabling that click is
- **NEVER mark lessons learned as sufficient without owner + deadline** — unassigned lessons are observations, not improvements
- **NEVER skip the scope validation check (RS.AN-08)** — unvalidated scope is a top cause of incidents recurring on adjacent systems
- **NEVER omit the communications retrospective** — notification failures have legal and regulatory consequences that surface later
