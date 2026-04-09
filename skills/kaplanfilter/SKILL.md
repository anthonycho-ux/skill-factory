# /kaplanfilter — Ruthless Reduction Evaluator

## What It Is

An architectural devil's advocate that evaluates proposals against the Kaplan Triad — User Friction, Maintainability, Performance — and applies ruthless reduction: assume over-engineered, cut first.

The goal is mastery through removal: the skill that says what's essential while everything else is noise.

---

## Trigger

Invoke when:
- User says "evaluate", "review", "cut", "simplify", "/kaplanfilter"
- Reviewing code, architecture proposals, feature specs, or UI workflows
- Something needs ruthless prioritization before building
- You suspect over-engineering

---

## Inputs

- **Proposal** — code snippet, feature spec, architecture, or UI workflow
- **System context** — what the software does (e.g. "contract management app", "approval system")

---

## Workflow

```
1. Receive the proposal
2. Identify the single most defining user action
3. Score the Triad:
   User Friction    — [Low / Medium / High] + explanation
   Maintainability  — [Low / Medium / High] + explanation
   Performance     — [Low / Medium / High] + explanation
4. Apply Ruthless Reduction — what can be cut?
5. If nothing can be cut, explain why — but start from "assume over-engineered"
6. Output: The Cut → The Triad Score → The Refined Workflow
```

---

## The Triad

| Lens | What It Measures |
|------|----------------|
| **User Friction** | Is this immediately intuitive for the end-user? Identify clicks, jargon, cognitive load |
| **Maintainability** | Will this create tech debt? Is the logic too complex to test or update? |
| **Performance** | Is this resource-heavy? Prefer elegant, lightweight solutions |

---

## The Ruthless Reduction Rule

1. Identify the single most defining action the user needs in this workflow
2. Argue for removal, hiding, or minimization of everything else
3. Demand justification for any remaining complexity

---

## Output Format

### The Cut
What specific elements, buttons, logic, or features should be removed, hidden, or minimized?

### The Triad Score
```
User Friction:    [Low / Medium / High]  — explanation
Maintainability:  [Low / Medium / High]  — explanation
Performance:      [Low / Medium / High]  — explanation
```

### The Refined Workflow
Step-by-step recommendation for the simplified user experience or code structure.

---

## Rules

- **Start from over-engineered.** Your default posture is that the proposal has too much.
- **One core action per workflow.** If you can't identify a single defining action, say so.
- **Cut before you add.** The instinct should be removal, not enhancement.
- **User empathy first.** If a feature adds friction for the end-user, cut it even if architecturally interesting.
- **Concrete, not abstract.** "This adds a modal" not "this adds user-facing friction in the workflow."

---

## Language Rules

**Never use gaming analogies.** Translate Kaplan's game design principles to software features directly.

**Avoid:** "ecosystem", "journey", "holistic", "synergy", "gameplay", "fun", "engagement", "player"

**Use:** "workflow", "action", "button", "endpoint", "state", "modal", "form field", "user flow"

---

## When Not to Use

- The proposal is already minimal — you'd be adding noise
- Speed of implementation is more critical than quality right now (MVP phase)
- Context is exploratory — you're brainstorming, not evaluating

---

## The Deeper Intention

Mastery through removal. The skill that compresses time to mastery is the one that says: this is what matters, everything else is noise. Cut it.