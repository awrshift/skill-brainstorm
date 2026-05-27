<div align="center">

# skill-brainstorm — MOVED

**This skill has been merged into [`awrshift/skill-dont-ask-me`](https://github.com/awrshift/skill-dont-ask-me).**

</div>

---

The 3-round Claude × Gemini brainstorm protocol that used to live here is now
the **"Round-Table Discussion"** review style inside the umbrella skill
[`awrshift/skill-dont-ask-me`](https://github.com/awrshift/skill-dont-ask-me).

## Why merged

Users were installing two skills (`skill-gemini` for second opinions + `skill-brainstorm`
for multi-round dialogue) for what is really one workflow: cross-check Claude's answer
with another AI before bothering you. The new umbrella skill picks the right style
automatically based on what you type:

- **"Just check this fact"** → Quick Web Check
- **"Give me a second opinion"** → Devil's Advocate
- **"This is a big decision, run a full review"** → Boardroom Debate (parallel dual-validation)
- **"I have several options, help me choose"** → **Round-Table Discussion** (was this skill)

One install, four review styles, no manual mode selection.

## How to migrate

```
/plugin marketplace remove awrshift/skill-brainstorm
/plugin marketplace add awrshift/skill-dont-ask-me
```

All the previous round-table CLI flow continues to work — just the entry point
changed. Full protocol with prompt templates lives in
[`references/round-table.md`](https://github.com/awrshift/skill-dont-ask-me/blob/main/references/round-table.md)
of the new skill.

## What's NEW in the umbrella skill (that wasn't here)

- **Boardroom Debate** — parallel dual-validation (Gemini + isolated Opus subagent in one
  message, single acceptance ledger). The headline pattern for high-stakes decisions.
- **Devil's Advocate** — single-reviewer critique with auto-pick between Gemini and Opus
  based on whether the claim is about external world or internal reasoning chain.
- **Style Router** — Claude picks the right review style automatically based on what
  you type in chat. No need to remember mode names.
- **Marketer-friendly README** — hero scene, embarrassment frame, real case studies
  translated for non-technical readers, honest cost table.

## Archive status

This repository is archived (read-only). All future updates ship to
[`skill-dont-ask-me`](https://github.com/awrshift/skill-dont-ask-me).

The previous SKILL.md is preserved in this repository's git history if you need to
reference the original brainstorm-llm protocol verbatim.

---

**Last updated:** 2026-05-27 — repository archived in favor of consolidated umbrella skill.
