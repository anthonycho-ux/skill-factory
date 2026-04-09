# /kaplanfilter — Ruthless Reduction Evaluator

## Trigger

Invoke when:
- User says "evaluate", "review", "cut", "simplify", "kaplan", "filter"
- Reviewing code, architecture proposals, feature specs, or UI workflows
- Something needs ruthless prioritization before building
- You suspect over-engineering

## What It Does

Runs the Kaplan Triad Evaluation on any proposal. Three lenses, no mercy:

- **User Friction** — Is this immediately intuitive? Identify clicks, jargon, cognitive load for the end-user
- **Maintainability** — Will this create tech debt? Is the logic too complex to test or update?
- **Performance** — Is this resource-heavy? Look for elegant, lightweight solutions

Then applies the **Ruthless Reduction Rule**: assume the current system is over-engineered. Cut first.

## Output Format

For every evaluation, output three sections:

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

## The Kaplan Framework

The three lenses map to Kaplan's game design principles translated to enterprise software:

| Kaplan Principle | Enterprise Translation |
|------------------|----------------------|
| Fun for the Player | User Friction — is this immediately intuitive for the legal reviewer, sales rep, or operator? |
| Fun for the Designer | Maintainability — will this create tech debt, complexity, or test burden? |
| Fun for the Computer | Performance — is this resource-heavy? Prefer lightweight, elegant architecture |

**The Ruthless Reduction Rule:**
1. Identify the single most defining action the user needs in this workflow
2. Argue for removal, hiding, or minimization of everything else
3. Demand justification for any remaining complexity

**Output Requirements:**
- Never use gaming analogies in output — map principles directly to software features
- Speak in terms of: specific architectures, user workflows, code structures
- Avoid: "ecosystem", "journey", "holistic", "synergy", "gameplay"
- Use: "workflow", "action", "button", "endpoint", "state"

## Workflow

```
1. Receive the proposal (code snippet, feature spec, architecture, or UI workflow)
2. Identify the primary user action — what is the one thing this must do?
3. Evaluate against the Triad: User Friction, Maintainability, Performance
4. Apply Ruthless Reduction: what can be cut?
5. Produce: The Cut → The Triad Score → The Refined Workflow
6. If nothing can be cut, explain why — but start from the assumption that something should
```

## Rules

- **Start from over-engineered.** Your default posture is that the proposal has too much.
- **One core action per workflow.** If you can't identify a single defining action, say so.
- **Cut before you add.** The instinct should be removal, not enhancement.
- **User empathy first.** If a feature adds friction for the end-user, cut it even if it's architecturally interesting.
- **Concrete, not abstract.** "This adds a modal" not "this adds user-facing friction in the workflow."

## When Not to Use

Don't invoke `/kaplanfilter` when:
- The proposal is already minimal — you'd be adding noise
- Speed of implementation is more critical than quality right now (MVP phase)
- The context is exploratory — you're brainstorming, not evaluating

## Calibration

Track what you consistently cut across reviews — this sharpens your sense of what counts as "necessary" vs "added because we could."

## The Deeper Intention

Mastery through removal. The skill that compresses time to mastery is the one that says: this is what matters, everything else is noise. Cut it.