# /firstprinciples — First-Principles Reduction Evaluator

## Definition

A skill that forces proposals through three questions before writing any line.

1. **Why this?** — Actual user need, devoid of solution language.
2. **Why not nothing?** — What breaks without this?
3. **Why this way?** — Is there a simpler path?

This filters noise before implementation. Goal: load-bearing work.

---

## Trigger

Invoke when:
- User requests evaluation ("firstprinciples," "evaluate this," "is this necessary").
- Before non-trivial implementation.
- During review, planning, or scoping.
- Decisions lack a clear path.

---

## Inputs

- **Proposal** — Feature, change, architecture, or workflow.
- **Context** — System function, users, problem space.

---

## Workflow

1. Receive proposal.
2. Ask: "Why this?" — Extract user need.
   - Reject justification ("because everyone does it").
3. Ask: "Why not nothing?" — Identify cost of omission.
   - If nothing breaks, question necessity.
   - If something breaks, name the failure mode.
4. Ask: "Why this way?" — Assess simplicity.
   - Compare to: do nothing, manual, existing tools.
   - Demand justification if the simplest path is not chosen.
5. Score Lenses:
   Load-Bearing? — [Yes / Partial / No] + consequence of removal.
   Simplest Path? — [Yes / No] + simpler alternative.
   Reversible? — [Yes / No] + cost to undo.
6. Output: The Cut → Lenses → Decision.

---

## The Three Lenses

| Lens | Measure |
|------|---------|
| **Load-Bearing** | Does this cause breakage if removed? Is it a solution seeking a problem? |
| **Simplest Path** | Is this the minimum intervention? Is there a simpler alternative? |
| **Reversible** | Cost to undo a wrong decision. Low-reversibility demands more scrutiny. |

---

## The Three Questions (Depth)

### Why this?

Reject solution language. "We need a caching layer" is not a need.
A valid need statement:
- Names specific pain by a specific user.
- States current cost (time, money, errors).
- Prescribes no solution.

Red flags:
- "Future scalability"
- "Industry standard"
- "Best practice"
- "We might need this later"

### Why not nothing?

If removed, what fails? Be specific. "The app works fine without it" validates omission.
If failure occurs:
- Name the specific failure mode.
- Quantify cost. Low cost signals small scope.

### Why this way?

Solutions include:
- Doing nothing.
- Manual execution.
- Existing tools.
- New construction.

If the chosen path is not the simplest solution, the burden is: *What property does this approach possess that simpler options lack?*

---

## Output Format

### The Cut
Elements, logic, or complexity to remove or defer.

### The Three Lenses
```
Load-Bearing:  [Yes / Partial / No]  — explanation
Simplest Path: [Yes / No]            — alternative or justification
Reversible:    [Yes / No]            — cost of undo
```

### The Decision
```
✅ Build it.  — (load-bearing, simplest path, reversible)
⚠️ Build smaller. — (load-bearing but over-engineered)
❌ Don't build it. — (not load-bearing, or simplest path is doing nothing)
🔄 Defer it. — (load-bearing but not now)
```

---

## Rules

- **Skepticism first.** Default: proposal contains optional complexity.
- **Name failure modes.** Specify what stops the system.
- **Prefer reversible decisions.** Low-reversibility increases risk.
- **"Because everyone does it" is irrelevant.** Constraints differ.
- **Activity is not progress.** Complex solutions do not equal sophistication.
- **Simplicity is a feature.** The simplest solution solves the need.

---

## Language Rules

**Avoid:** "ecosystem", "journey", "holistic", "synergy", "scalable", "robust", "enterprise", "future-proof".

**Use:** "workflow", "action", "button", "endpoint", "state", "user need", "failure mode", "cost", "reversible".

---

## When Not to Use

- Proposal is already minimal and load-bearing. Adding noise.
- Speed is paramount (MVP phase).
- Context is exploratory (brainstorming).
- Decision is committed (firstprinciples for live decisions).

---

## Deeper Intention

First-principles thinking is not pessimism. It is the discipline to ask if a thing should exist before asking how to build it.

Complexity enters systems via unexamined assumptions: "we'll need this." This complexity costs maintenance and fragility. The cost of the question is minimal now.

/firstprinciples handles existence. /kaplanfilter handles construction. /mine handles validation.

```
Does this need to exist?       → firstprinciples
Is this as simple as it can be? → kaplanfilter
Does this sound like human writing? → mine
```

---

## Sources

- **Jeff Kaplan** — Prioritize action. Cut complexity.
- **DHH** — Over-complication is dread. Austere precision.
- **Jensen Huang** — Reason from first principles. Shape belief before execution.

## Dependencies

None. Pure reasoning skill.
