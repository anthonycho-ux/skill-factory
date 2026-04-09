# /iterate-109 — Document Every Attempt Evaluator

## What It Is

A discipline and evaluation skill from Marc Raibert's Atlas 109-trials principle: the failure history is the learning history. Every attempt is documented.

Core: *"It took 109 tries and we have video of every one of them, we shoot everything."*

This is not about tolerance for failure. It is about treating failure as a data source, not an embarrassment.

---

## Trigger

Invoke when:
- Starting a project where success requires repeated empirical iteration
- Evaluating whether a team's learning culture is genuine or performed
- Assessing a "highlight reel" that only shows wins
- Deciding whether to invest in documentation tooling for an iterative process
- Building or buying test infrastructure for a system that must be robust

---

## Inputs

- **Process** — an iterative workflow (testing, tuning, building)
- **Team culture** — whether failures are documented or buried
- **Tooling** — whether the team has infrastructure to capture attempts

---

## The Three Layers

### Layer 1: Document It

Every attempt gets logged. Video if physical, logs if digital, notes if observational. The goal is to reconstruct the full attempt history from storage, not from memory.

**The test:** If someone asks "what happened on attempt 47?", can you answer in under a minute?

### Layer 2: Watch It

Failure footage is reviewed, not archived. The team that watches its failures learns faster than the team that buries them.

**The test:** Do people voluntarily watch the failure compilations, or are they treated as embarrassing?

### Layer 3: Publish It

The no-explanation standard: if the work can't stand without narration, it hasn't landed. Publishing forces genuine quality over narrative management.

**The test:** Remove all explanatory text, titles, narration. Is the result still legible and impressive?

---

## The 109-Attempt Rule

1. **Plan for 109 attempts** — not as an estimate, as a design constraint
2. **Build infrastructure to document all of them** — video, logs, metrics, timestamps
3. **Budget for repair** — the machine will break; budget spares and crew
4. **Review the failures, not just the successes** — failures carry more information
5. **Ship the video of every attempt** — transparency is a forcing function for quality

---

## The Signature Move: "Why Not?"

> "When someone would say, 'You can't do that.' He'd say, 'Why not?'"

The entry reflex for every constraint. Not "should we challenge it?" — the question is a reflex.

**Four answers to "why not?":**
1. **Historical accident.** → Challenge it.
2. **True then, not now.** → Challenge it.
3. **Protects a real interest.** → Understand it, find a narrower version.
4. **Physics says no.** → Accept it, find a different path.

Most of the time: answer is #1.

---

## The Hawaiian Shirt Principle

The contrarian reflex is a daily practice, not a personality trait. When offered a standard, convention, or majority view — ask who made it and for what conditions. The standard may be correct. It may also be an unexamined inherited constraint narrowing your space without justification.

---

## Success Criteria

- [ ] Attempt history is searchable and reviewable
- [ ] Failure compilations are watched voluntarily
- [ ] Published work meets the no-explanation standard
- [ ] "Why not?" is asked reflexively before accepting any constraint
- [ ] Contrarian challenges are documented and resolved, not dropped

---

## Language Rules

**Avoid:** "outtake", "failure footage", "what went wrong"
**Use:** "attempt history", "attempt 47", "the data from run 47", "documented iteration"

"Failure" implies blame. "Attempt" implies learning.

---

## Chaining

```
Building something hard?         → /iterate-109
Is this as simple as it can be?  → /firstprinciples
Does this pass the robustness test? → /kaplanfilter
Who do we trust with this?        → /commitment
```

---

## Source

Marc Raibert — Lex Fridman Podcast #412, Boston Dynamics

Core quotes:
- "It took 109 tries and we have video of every one of them, we shoot everything."
- "You have to have courage to be intrepid, when you work so hard to build your machine, and then you're trying it, and it just doesn't do what you thought."
- "My theory of the video is no explanation. If they can't see it, then it's not the right thing."
- "'Why not?' — it's a great question."
- "It took me a while to realize that I was a contrarian, but it can be a useful tool."

---

## Dependencies

None. Pure reasoning + documentation discipline.
