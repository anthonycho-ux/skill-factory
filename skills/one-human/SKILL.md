# /one-human — The Single Control Point Auditor

## What It Is

In any automated chain, find the one human decision-maker. That person is the entire control structure — even if the chain looks automated. Exploit or protect them accordingly.

Named after the mortgage fraud chain analysis: credit scores automated, income verification automated, employment confirmation automated — only the appraisal requires a human with contextual knowledge of a specific neighborhood. That one human, doing 40–50 reviews a day, is the entire remaining control point.

---

## Trigger

Invoke when:
- "How does this process actually stop bad actors?"
- "What's the last line of defense in this automated system?"
- "Why did this get approved when it shouldn't have?"
- Auditing a financial, legal, or security system for control points
- Designing a new system: where do you put the human, and why only there?

---

## Steps

### 1. Map the automated chain.

List every step. For each step: what happens, what checks run, what documents are verified.

### 2. Identify the human step(s).

Where does a human look at something, make a judgment, or sign off? Everything else is automated.

### 3. Assess the human's position.

Is the human at the end of the chain (final approver) or in the middle? If in the middle and the chain continues past them, find who actually determines the outcome. Often there is one person who could stop the bad outcome.

### 4. Evaluate the human's load.

What volume does this human work through? 40 reviews a day? 200 applications a week? The load determines whether the human is actually checking or rubber-stamping because they cannot keep up.

### 5. Map the exploitation path.

If an attacker knows the human is the only real checkpoint:
- **Volume exhaustion:** give them too much to review carefully
- **Contextual blindness:** make the surrounding documentation look correct
- **Compliance camouflage:** make the violation look like a common edge case

If you're a defender, add secondary controls — because the single human will fail under load.

---

## The Deeper Principle

**Automation creates single points of control.** When you automate a process, you compress decision-making into fewer human touchpoints until one human is the only remaining eyes on the file. That human is usually overloaded and under-informed. They are the control structure and the vulnerability simultaneously.

---

## Rules

- **Find the human, then find their load.** A human with adequate time is a control. A human with 200 cases a day is a bottleneck.
- **Attackers know this before you do.** Every sophisticated fraudster maps the automated chain to find the human, then designs around them.
- **If the human is the only control, it's a single point of failure.**
- **Adding automation above the human doesn't protect them.** It increases their load. Security posture can go down while throughput goes up.

---

## Chaining

```
How does this stop bad actors? → /one-human
Is this automated process safe? → /one-human
We have multiple controls → verify there are multiple humans doing different checks
```

---

## Source

Matthew Cox — Lex Fridman Podcast #409

The analysis: credit scores, income, employment, rent history — all automated. Only the appraisal required a human with contextual knowledge. That one human, doing 40–50 reviews a day, was the entire remaining control.

---

## Dependencies

None. Pure systems analysis skill.