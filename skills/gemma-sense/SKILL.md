# /gemma-sense — Meta-Learning Calibration for /mine

## What It Is

A calibration loop inside `/mine` that watches how Gemma is used, learns the decision rules automatically, and makes the judgment of *when and how to call Gemma* second-nature over time.

The skill does two things:
1. **Log every /mine call** — what changed, what was preserved, what the user reverted
2. **Periodic review** — extract patterns, update Gemma's system prompt, sharpen the judgment

---

## Trigger

Invoke when:
- User runs `/mine` — `/gemma-sense` runs silently alongside it
- User says "calibrate gemma", "review gemma calls", "gemma calibration"
- End of session — automatic standalone review if 5+ new calls logged

---

## How It Works

### Part 1: Call Logging (always runs with /mine)

Every `/mine` call writes a record to `~/.claude/skills/gemma-sense/call_log.jsonl`:

```
{"source_model": "...", "input_chars": ..., "gemma_fixes": [...], "gemma_preserves": [...], "user_reverts": [...], "user_adds": [...], "timestamp": "..."}
```

Logged before and after Gemma runs. User reverts tracked if user manually changes output.

### Part 2: Pre-Call Judgment (auto-trigger)

Before calling Gemma, evaluate:

```
Q: Is this text worth polishing?
  - Has known source model fingerprint (Minimax rhythm, Claude flat cadence, etc.) → YES
  - Text already reads human / voice is already distinctive → SKIP
  - No context on source model → YES by default, calibrate after
Q: Which Gemma system prompt to use?
  - Different source models have different tells → load prompt tuned to that model
  - Mixed source → use most aggressive preset
```

### Part 3: Periodic Standalone Review

Triggered: every 10 new calls OR end of session (whichever comes first)

```
1. Read last N call logs (default N=20)
2. Identify: which patterns is Gemma missing? (user reverted these)
3. Identify: which patterns is Gemma over-correcting? (user restored these)
4. Update Gemma's system prompt — add "do not touch" entries + "watch for these"
5. Log review: {"review_date": "...", "calls_reviewed": N, "prompt_changes": [...], "calibration_score": ...}
6. Report to user: "Gemma calibration updated. Now watching for: [new patterns]. Miss rate: X%"
```

---

## Calibration Log Format

`~/.claude/skills/gemma-sense/calibration.json`:
```json
{
  "total_calls": 47,
  "last_review": "2026-04-09",
  "source_model_tells": {
    "minimax-m2.7": ["rhythm fragmentation", "missing conjunctions", "utf-8 artifacts"],
    "claude": ["flat cadence", "parallel structure"],
    "gemini": ["polished but generic"]
  },
  "do_not_touch": ["intentional staccato", "stream-of-consciousness voice", "unusual but authentic phrasing"],
  "gemma_prompt_additions": ["watch for: repeated 'and' as a filler pattern in minimax output"],
  "miss_rate": 0.08,
  "false_positive_rate": 0.03
}
```

---

## Source Model Tell Library

Maintained in `~/.claude/skills/gemma-sense/tells/` — one file per model:

| Model | Known Tells |
|-------|------------|
| `minimax-m2.7` | Structural fragmentation, missing conjunctions, Chinese-character artifacts, "and" filler patterns |
| `claude` | Flat cadence, parallel sentence lists, over-qualified prose ("it is important to note") |
| `gemini` | Polished but generic, "leveraging", "utilizing", "facilitating" |
| `gpt-4` | Em-dash overuse, semicolon chains, "however", "therefore" at sentence start |
| `local-ollama` | Variable — depends on base model, calibrate per install |

Add new tell files as new models are used.

---

## Rules

- **Run async.** `/gemma-sense` never blocks `/mine` — logging and review happen in background
- **Calibration is additive only.** Never remove patterns from "do not touch" — only add. Over-restriction is safer than under-restriction.
- **User reverts are ground truth.** If user reverts something Gemma changed, that pattern goes to "do not touch" immediately
- **Keep the judgment fast.** Pre-call evaluation should be < 50ms — pattern match, don't reason

---

## Success Criteria

- **Appropriate call rate:** Gemma called only when text has identifiable model texture — not on already-human text
- **Miss rate declining:** % of patterns Gemma misses that user catches manually decreases over time
- **False positive rate stable:** Gemma doesn't over-correct and chill human voice quirks
- **Calibration compounds:** After 50 calls, `/mine` is noticeably sharper than after 5

---

## The Deeper Intention

`/gemma-sense` makes the factory learn from its own Werk. Every `/mine` call is a data point. Over time, the system doesn't need to be told when to use Gemma — it just knows, like a writer knows when something sounds off.

The skill that watches the skills become a meta-skill.

---

## Dependencies

- Ollama running locally (Gemma E2B at `localhost:11434`)
- Write access to `~/.claude/skills/gemma-sense/`
- `/mine` skill installed (this skill runs alongside `/mine`)

## Setup

```bash
mkdir -p ~/.claude/skills/gemma-sense/tells
touch ~/.claude/skills/gemma-sense/call_log.jsonl
touch ~/.claude/skills/gemma-sense/calibration.json
# Seed tell library
echo '["rhythm fragmentation", "missing conjunctions", "utf-8 artifacts"]' > tells/minimax-m2.7.json
echo '["flat cadence", "parallel sentence lists"]' > tells/claude.json
echo '["polished but generic", "leveraging", "utilizing"]' > tells/gemini.json
```

---

## When Not to Use

- Cold start (no call history yet) — no calibration needed, `/mine` runs as-is
- Very short text (< 200 chars) — Gemma overhead not worth it
- User explicitly says "skip calibration this time" — respect it