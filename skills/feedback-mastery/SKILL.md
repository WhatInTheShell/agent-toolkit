---
name: feedback-mastery
description: Deliver high-stakes feedback, navigate difficult workplace conversations, and coach others through performance issues. Use when giving feedback, preparing for a hard 1:1, addressing conflict, managing underperformance, or coaching someone on receiving feedback. Keywords: feedback, difficult conversation, performance, conflict, behavior, 1:1, one-on-one, confrontation, underperformance, coaching.
allowed-tools: Read, Glob, Grep
---

# Feedback Mastery

## Mindset

1. **Feedback is information transfer, not judgment delivery.** The moment the receiver perceives evaluation, their prefrontal cortex partially shuts down — defensiveness is physiological, not character flaw. Frame as "I noticed / I want to understand" not "you did X wrong."

2. **Timing destroys or amplifies impact.** Feedback given within 48 hours of an event lands 3–4x more effectively than delayed feedback. "Annual review surprises" are managerial malpractice — they signal you withheld useful information for months.

3. **Psychological safety is the prerequisite, not the outcome.** If the receiver doesn't feel safe, no framework saves you. Check safety first: if someone is visibly activated (defensive posture, clipped answers, raised voice), name it before proceeding.

4. **The goal of feedback is behavior change, not catharsis.** If you need to vent, do it elsewhere. The conversation exists to help them, not to make you feel like you said something.

5. **Pattern vs. instance matters more than severity.** A single bad code review matters less than 3 in a row. Leading with "I've noticed a pattern" signals seriousness without catastrophizing a one-time event.

## Navigation

**Use this skill when**:
- Preparing to give feedback (corrective or positive) to a colleague or direct report
- Navigating conflict, tension, or misaligned expectations with stakeholders
- Coaching someone who received feedback poorly and needs to process it
- Handling underperformance conversations where HR escalation is possible
- Facilitating a conversation between two people in conflict

**Do NOT use this skill when**:
- Writing performance review prose (use a writing skill instead)
- Termination conversations (require HR, legal review — out of scope)
- Therapy or mental health support (refer appropriately)

**Quick decision tree for ambiguous inputs:**
```
Is this corrective or positive feedback?
  ├─ Corrective + first time → SBI + curiosity (explore root cause)
  ├─ Corrective + recurring pattern → SBI + explicit stakes + plan
  ├─ Corrective + HR-level severity → load references/difficult-conversation-scripts.md
  └─ Positive → SBI + specific impact (skip the "but" — never pair positive/corrective)
```

## Philosophy

Feedback is an act of respect — it assumes the person can change and is worth investing in. Withholding honest feedback to avoid discomfort is not kindness; it's abandonment. Deliver what's true, specifically, without cruelty.

## NEVER

- **NEVER use the feedback sandwich (positive-negative-positive)** — because research shows it trains people to distrust positive feedback and miss the corrective message. Receivers remember the bread, not the filling. Use pure SBI instead.

- **NEVER give corrective feedback in public** — because social threat activates the same neural circuits as physical threat (fMRI studies by Lieberman, 2013). Public correction compounds shame and guarantees defensiveness; the person will protect ego, not process content.

- **NEVER delay feedback to "find the right moment" indefinitely** — because memory encoding degrades within 72 hours. Waiting for perfect conditions means the specific behavior is no longer vivid to either party, and the conversation devolves into abstract debate about character.

- **NEVER pair positive and corrective feedback in the same sentence with "but"** — because "but" neurologically erases everything before it. "You did great work on the API, but the tests were weak" lands as "your tests were weak." Use separate conversations or at minimum separate paragraphs with a full stop.

- **NEVER give feedback when you or the receiver are emotionally flooded** — because cortisol and adrenaline impair complex cognition in both parties. A flooded conversation produces defensive agreements that don't stick. Reschedule explicitly: "I want to have this conversation when we're both at our best — can we do 10am tomorrow?"

- **NEVER interpret behavior aloud without evidence** — because attributing motive ("you clearly don't care about quality") activates the fundamental attribution error and makes the receiver defend their character rather than examine their behavior. Stick to observable actions and their effects.

- **NEVER skip the "impact" step of SBI** — because behavior without impact sounds like nitpicking. Impact connects the behavior to something the receiver actually cares about (team success, trust, project outcomes). Without it, feedback feels like personal preference, not professional necessity.

## Core Technique: SBI (Extended Practitioner Version)

Claude already knows the basic SBI framework. What it misses:

**The "I" in Impact must connect to receiver values, not just your frustration.** If you know they care about team perception, connect the impact to that. If they care about code quality, connect there. Generic impact ("it slowed us down") lands weaker than specific impact ("it meant Sarah had to redo 3 hours of work and now doubts whether to surface issues").

**SBI+ for recurring patterns:**
> Situation → Behavior → Impact → **Expectation** → **Stakes**

Add: "Going forward, I need [specific behavior]. If this continues, [concrete consequence]." The stakes must be real and proportional — don't threaten what you won't follow through on.

**Positive SBI is not trivial.** Most managers skip it entirely or give generic praise. Specific positive SBI ("In Thursday's incident review, you asked the question no one else would — which unlocked the root cause and saved us 2 days") builds the safety account that makes corrective feedback land better later.

## Timing Heuristics

| Scenario | Optimal Timing | Why |
|----------|---------------|-----|
| In-meeting behavior | Within same day, privately | Memory sharp; behavior still vivid |
| Code/work quality | Within 48 hours of delivery | Before they're deep in next task |
| Interpersonal conflict | After 2–4 hours cooling, same day | Enough distance to avoid flood; close enough to be concrete |
| Pattern (recurring issue) | Scheduled 1:1, not ad hoc | Signals importance, allows preparation |
| Crisis/incident behavior | After incident closes, not during | During crisis, feedback = distraction |

## When Things Go Wrong

| Situation | Likely Cause | Recovery |
|-----------|-------------|----------|
| Receiver goes silent or shuts down | Social threat response activated; they feel ambushed or shamed | Name it: "I notice you've gone quiet — I want to make sure this feels like a conversation, not a verdict. What's your reaction?" |
| Receiver becomes defensive / attacks back | Behavior was stated as interpretation, not observation; or they feel blindsided | Return to facts: "I want to make sure I'm working from what I actually observed. Can we back up to [specific event]?" |
| Receiver agrees but nothing changes | Agreement was to end the discomfort, not from genuine buy-in | Explicit follow-through plan required: named actions, dates, check-in. "What specifically will you do differently by [date]?" |
| You realize mid-conversation you lack enough specifics | Feedback was prepared based on impressions not evidence | Pause honestly: "I realize I should have more specific examples ready. Can we schedule 30 minutes tomorrow when I can come prepared?" |
| Positive feedback lands flat / receiver dismisses it | Generic praise, or receiver distrusts your motives | Increase specificity: name exact action, exact effect, exact why it mattered. Vague praise is discounted; surgical praise lands. |

## Reference Loading Triggers

Load `references/difficult-conversation-scripts.md` when:
- User needs exact opening lines, scripts, or word-for-word phrasing
- Scenario involves HR-sensitivity, termination risk, or legal exposure
- User is conflict-averse and needs scripted scaffolding to start

Load `references/feedback-sbi-model.md` when:
- User needs more SBI examples across different contexts (code reviews, meetings, deliverables)
- User is learning the framework and needs worked examples

Load `references/expectation-alignment.md` when:
- Issue is stakeholder misalignment, scope creep, or "moving goalposts"
- User needs to reset expectations without creating conflict
