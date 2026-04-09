# /firstprinciples — First-Principles Reduction Evaluator

## What It Is

A ruthlessly simple skill that forces every proposal through three questions before a single line is written or changed:

1. **Why this?** — What is the actual user need, stated without solution language?
2. **Why not nothing?** — What breaks if this doesn't exist?
3. **Why this way?** — Is there a simpler approach that achieves the same outcome?

It combines Kaplan's "assume over-engineered, cut first" with DHH's "chasing that '90s PHP high" and Jensen's "reason from first principles, then manifest the future." The result is a filter that eliminates noise before it enters the system.

The goal is not to say no. The goal is to arrive at work that is load-bearing — where every piece earns its place.

---

## Trigger

Invoke when:
- User says "firstprinciples", "evaluate this", "do we need this", "is this necessary"
- Before starting any non-trivial implementation
- During code review, architecture planning, or feature scoping
- When a decision has multiple valid approaches and the path forward is unclear

---

## Inputs

- **Proposal** — a feature request, code change, architecture decision, or workflow
- **Context** — what the system does, who uses it, what problem space it lives in

---

## Workflow

```
1. Receive the proposal
2. Ask: "Why this?" — Strip all solution language. What is the actual user need?
   - If the answer is "because everyone does it" or "for future flexibility" → flag it
3. Ask: "Why not nothing?" — What is the actual cost of not doing this?
   - If the answer is "nothing breaks" → question the proposal's necessity
   - If the answer is "something breaks" → name what breaks, exactly
4. Ask: "Why this way?" — Is there a simpler version?
   - Compare to: doing nothing, doing it by hand, doing it with existing tools
   - If the simplest version wasn't chosen → demand a reason
5. Score the Three Lenses:
   Load-Bearing?  — [Yes / Partial / No] + what would break if removed
   Simplest Path? — [Yes / No] + what simpler alternative exists
   Reversible?    — [Yes / No] + cost of undoing if wrong
6. Output: The Cut → The Three Lenses → The Decision
```

---

## The Three Lenses

| Lens | What It Measures |
|------|----------------|
| **Load-Bearing** | Would something actually break if this didn't exist? Or is this a solution in search of a problem? |
| **Simplest Path** | Is this the minimum intervention that solves the actual need? Or is there a simpler version? |
| **Reversible** | If this decision is wrong, what's the cost to undo? Low-reversibility decisions deserve more scrutiny. |

---

## The Three Questions (Depth)

### Why this?

Reject the solution language. "We need a caching layer" is not a need — "users see 3-second delays on repeated queries" is a need.

A valid need statement:
- Names a specific pain experienced by a specific user
- States the current cost (time, money, errors, frustration)
- Does not prescribe a solution

Red flags:
- "For future scalability"
- "Industry standard"
- "Best practice"
- "We might need this later"

### Why not nothing?

If you removed this thing entirely, what would actually go wrong? Be specific. "The app would work fine without it" is a valid and important answer — it means the proposal is optional.

If something would genuinely break:
- Name the specific failure mode
- Quantify the cost if possible
- If the cost is low, that's a signal this can be small

### Why this way?

The space of solutions includes:
- Doing nothing
- Doing it manually
- Using an existing tool or system
- Building something new

If the chosen path isn't the simplest one that solves the need, the burden of proof shifts to: *what specific property does this approach have that simpler approaches lack?*

---

## Output Format

### The Cut
What specific elements, logic, or complexity can be removed or deferred?

### The Three Lenses
```
Load-Bearing:  [Yes / Partial / No]  — explanation
Simplest Path: [Yes / No]            — simpler alternative or why this is it
Reversible:    [Yes / No]            — cost of undo if wrong
```

### The Decision
```
✅ Build it.  — (load-bearing, simplest path, reversible)
⚠️ Build it smaller. — (load-bearing but over-engineered)
❌ Don't build it. — (not load-bearing, or simplest path is doing nothing)
🔄 Defer it. — (might be load-bearing but not now)
```

---

## Rules

- **Start from skepticism.** Default posture: this proposal has optional complexity.
- **Name the failure mode.** "Something would break" is not specific enough. What, specifically, would stop working?
- **Prefer reversible decisions.** High-reversibility = low cost if wrong. Prefer the option that keeps doors open.
- **"Because everyone does it" is not a reason.** Every team has different constraints. What works at Google doesn't automatically work here.
- **Do not mistake activity for progress.** A complex solution to a simple problem is not a sign of sophistication.
- **Simplicity is a feature.** The simplest thing that solves the actual need is almost always the right choice.

---

## Language Rules

**Avoid:** "ecosystem", "journey", "holistic", "synergy", "scalable", "robust", "enterprise", "future-proof"

**Use:** "workflow", "action", "button", "endpoint", "state", "user need", "failure mode", "cost", "reversible"

---

## When Not to Use

- The proposal is already minimal and load-bearing — you'd be adding noise
- Speed of implementation is more critical than quality right now (startup MVP phase)
- Context is exploratory — you're brainstorming, not evaluating
- The decision is already made and committed — firstprinciples is for live decisions, not post-hoc rationalization

---

## The Deeper Intention

First-principles thinking is not pessimism. It's the discipline to ask whether a thing should exist before asking *how* to build it.

Most complexity enters systems not through bad implementation but through unexamined assumptions: "we'll need this," "everyone does this," "what if we grow." The cost of that complexity — maintainability, cognitive load, fragility — is paid slowly over time. The cost of the question is a minute now.

/kaplanfilter handles reduction once a thing exists. /firstprinciples handles the question of whether the thing should exist at all.

Together: /firstprinciples → /kaplanfilter → /mine

```
Does this need to exist?       → firstprinciples
Is this as simple as it can be? → kaplanfilter
Does this sound like a human wrote it? → mine
```

---

## Sources

Extracted from Lex Fridman Podcast analysis:
- **Jeff Kaplan** — "focus on what you wanna do, not what you wanna be"; ruthless prioritization; cutting to the single defining action
- **DHH** — "a lot of people...compensate for that existential dread by over-complicating things"; chasing the '90s PHP high; austere precision
- **Jensen Huang** — "I manifest a future and that future is so convincing, there's no way it won't happen"; reason from first principles; step-by-step belief shaping before execution

## Dependencies

None. Pure reasoning skill — no external tools required.
