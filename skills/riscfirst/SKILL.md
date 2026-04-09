# /riscfirst — Operator Surface Area Minimizer

## What It Is

Evaluate and design abstraction layers, APIs, frameworks, and runtimes by asking: how many operators does this require?

Every layer of a modern stack — Python, C++, CUDA, LLVM, PTX — is Turing complete. This is not a feature. It is a design flaw. The goal is a stack with the fewest operators possible, where each is load-bearing and nothing is redundant.

> "Tinygrad has about 25 operators. XLA has about 200. PyTorch PrimTorch has about 250. Tinygrad is RISC; everything else is SISC."

Fewer operators means: the system can be held in a single head, every behavior is inspectable and predictable, and the system can be reasoned about — not just simulated.

---

## Trigger

Invoke when:
- Designing a new API, abstraction, framework, or language runtime
- Evaluating an existing stack for unnecessary complexity
- Deciding between competing frameworks
- Before adding a new operator/primitive to an existing system
- "Too much boilerplate", "abstraction leak", "API surface area"

---

## The Operator Count Test

For any abstraction layer:

1. **What is the operator count?** How many distinct primitives must you understand before this system makes sense?
2. **Which are load-bearing?** Which operators, if removed, would make the system stop working?
3. **Which decompose into others?** If X can be written as Y + Z, X is not an operator — it is syntax.
4. **Is there a RISC version?** Can this be done with fewer operators?

---

## The RISC vs SISC Scale

| System | Operators | Classification |
|--------|-----------|----------------|
| Tinygrad | ~25 | RISC |
| XLA | ~200 | SISC |
| PrimTorch | ~250 | SISC |
| PyTorch (legacy) | ~2000 | CISC |

**The goal is always RISC.** Not for aesthetic reasons — because a system with fewer operators is more reason-able. You can hold it in your head. You can predict its behavior. You can debug it without a debugger.

---

## The Decomposition Test

Hotz refused to add a MatMul primitive to Tinyrad. Reason: MatMul decomposes into shape ops + multiply + reduce. Adding it means the operator list contains something that is not irreducible.

Before adding an operator: can this be expressed as a combination of existing operators? If yes, it isn't a new operator.

---

## The Surface Area Rule

Every new operator:
- Increases cognitive load of everyone who must understand the system
- Adds a new failure mode
- Creates a dependency on that operator's correctness
- Reduces ability to reason from first principles

**Rule:** Before adding an operator, prove it cannot be decomposed. Before adding a layer, prove it cannot be eliminated.

---

## The Turing Completeness Warning

Once a layer is Turing complete, it can compute anything — including things you don't want it to. Turing completeness is an escape hatch: instead of reasoning about the problem in the layer where it was stated, you can compute your way around it. Useful for bugs. Destructive for design.

The goal: a stack where every layer is as constrained as possible, and Turing completeness appears only at the point where it must — at the hardware, not in the abstractions above it.

---

## The Boilerplate Rule

> "Programming is tool complete. So if Codex or Copilot are helping you, that probably means your framework or library is bad — there's too much boilerplate in it."

Boilerplate is evidence of missing operators. If you find yourself writing the same seventeen-line pattern repeatedly: either the operator that would eliminate this pattern is missing, or the abstraction itself is wrong.

---

## The Holodeck Test

> "There's a Star Trek episode where Janeway edits her holodeck lover to remove his minor annoyances. Then she realizes: it's actually all their nuances and quirks that make the relationship worthwhile."

Applied to software: the quirks in a system are often load-bearing. Removing them to make the system "clean" can break the thing that made it work. Ask: what does this imperfection actually do? Before removing it, know what you're removing.

---

## Rules

- **Every operator is a debt.** Sometimes necessary debt — but debt.
- **Decompose before you add.**
- **Surface area compounds.** Every new operator multiplies interaction complexity.
- **Turing completeness is an escape hatch, not a goal.**
- **Boilerplate is a smell.**
- **Tests are velocity.** A small stack you can't trust is still slow.

---

## Chaining

```
Does this need to exist?              → /firstprinciples
Is the tool complexity proportional?    → /shipitfit
Is the operator count minimal?          → /riscfirst
```

---

## Source

George Hotz — Lex Fridman Podcast #391

Core quotes:
- "Tinygrad has about 25 operators. XLA has about 200. Tinygrad is RISC; everything else is SISC."
- "Once you get rid of Turing completeness, you can reason about things."
- "It's refactoring all the way down."

---

## Dependencies

None. Pure reasoning skill.