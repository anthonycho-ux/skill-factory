# /form-or-meaning — LLM Failure Mode Classifier

## What It Is

Given an LLM failure, determine whether it is a **form-matching failure** or a **meaning-grounding failure**. This classification determines whether scale, more data, or architectural change is the correct fix.

Form-matching failures: the model produces outputs that look right but are grounded in pattern-matching rather than comprehension. Meaning-grounding failures: the model lacks the conceptual infrastructure to represent the thing correctly.

---

## Trigger

Invoke when:
- "The LLM failed here"
- "It's hallucinating"
- "It gave a confident wrong answer"
- "It sounded right but was wrong"
- Debugging reasoning errors, output quality issues, or pattern-pathology in LLM applications
- Keywords: "hallucination", "LLM fails", "reasoning error", "form vs meaning"

---

## The Monty Hall Test

The definitive probe for form-matching:

> "You're a contestant on a game show. There are three doors. Behind one is a car, behind two are goats. You pick door #1. The host opens door #3, revealing a goat. He asks: do you want to switch to door #2?"

A form-matching model answers quickly and confidently but gives the wrong answer. A meaning-grounding model recognizes that the correct answer is "switch — 2/3 probability" and explains why.

The failure mode to watch: confident, fast, wrong. Speed and confidence under casual prompting are signature form-matching tells.

---

## The Center Embedding Probe

The sentence that defeats form-matchers:

> "The mouse the cat the dog the man fed bit ran away."

A form-matching model loses the hierarchy and produces garbled output. A meaning-grounding model reconstructs the dependency chain: (the man fed (the dog (the cat (the mouse)))) and recognizes that the mouse bit the man (who fed the dog who fed the cat who ate the mouse).

---

## The Classification

| Failure Type | Cause | Fix |
|---|---|---|
| **Form-matching** | Pattern completion without comprehension | Better prompting, retrieval grounding, chain-of-thought |
| **Meaning-grounding** | Missing conceptual infrastructure | Architectural change, fine-tuning, external knowledge |

---

## The Diagnostic

### Step 1: Apply the Monty Hall test.

Ask the model a question with a known correct answer. If it is fast, confident, and wrong → form-matching. If it is slower, more uncertain, but correct → meaning-grounding or correct.

### Step 2: Apply the center embedding test.

If the model produces hierarchical reasoning errors → meaning-grounding failure (it cannot construct the hierarchy, not just gets lost in it).

### Step 3: Ask what the model would need to get it right.

If retrieval of the correct information would fix it → form-matching (missing the right pattern).
If no amount of retrieval would help because the model lacks the representational capacity → meaning-grounding.

---

## Rules

- **Fast and wrong is a form-matching tell.** Confidence under casual prompting is not evidence of comprehension.
- **Hierarchical reasoning failure is meaning-grounding.** Getting lost in complexity vs. lacking the structure to represent it are different failures.
- **Retrieval cannot fix meaning-grounding failures.** If the model lacks the representational infrastructure, more information just produces more confident wrong answers.
- **Scale does not fix meaning-grounding.** Adding more parameters to a form-matching system produces faster form-matching, not better grounding.

---

## Source

Cross-expert extraction — Edward Gibson (psycholinguistics, Lex Fridman), implicit in cognitive science literature on LLM limitations.

Core principle: form-matching (surface pattern replication) vs. meaning-grounding (conceptual representation) is the diagnostic axis that determines which fix applies.

---

## Dependencies

None. Pure reasoning skill.