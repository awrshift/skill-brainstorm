<div align="center">

![Claude Code](https://img.shields.io/badge/Claude%20Code-D97757?style=for-the-badge&logo=claude&logoColor=white)
![Gemini Pro](https://img.shields.io/badge/Gemini%20Pro-4285F4?style=for-the-badge&logo=google&logoColor=white)
![License MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)

# skill-brainstorm

**3-round adversarial brainstorm between Claude and Gemini. One idea in, one converged decision out.**

*Claude orchestrates. Gemini Flash researches. Gemini Pro reasons. You decide.*

</div>

---

## What It Does

- **Runs a structured 3-round dialogue** between Claude and Gemini Pro — diverge, deepen, converge
- **Web-grounds all facts before reasoning** using Gemini Flash (dual verification: Claude WebSearch + Flash Google Search)
- **Kills bad ideas with evidence** — not a polite brainstorm, an adversarial stress-test
- **Produces one action** — not a list of options, a single concrete deliverable with timeline and go/no-go criteria
- **Fact-checks the final decision** — catches stale knowledge, pricing changes, deprecated APIs

## Quick Install

**Claude Code (recommended):**
```
/plugin marketplace add awrshift/skill-brainstorm
```

**Manual:**
```bash
mkdir -p .claude/skills/brainstorm/scripts
curl -sL https://raw.githubusercontent.com/awrshift/skill-brainstorm/main/skills/brainstorm/SKILL.md \
  -o .claude/skills/brainstorm/SKILL.md
curl -sL https://raw.githubusercontent.com/awrshift/skill-brainstorm/main/skills/brainstorm/scripts/gemini.py \
  -o .claude/skills/brainstorm/scripts/gemini.py
```

## Requirements

- `GOOGLE_API_KEY` in your `.env` file (get one at [aistudio.google.com](https://aistudio.google.com))
- `pip install google-genai` (the Gemini Python SDK)
- Claude Code with WebSearch access

## How It Works

```
                  Claude (orchestrator)
                     |         |
        Phase 0.5    |         |    R1 / R2 / R3
        Phase 3.5    |         |
                     v         v
              Flash-Lite        Pro
           (research layer)  (reasoning layer)
                     |              ^
                     +--Verified----+
                        Context
```

### The Pipeline

| Phase | What Happens | Model |
|-------|-------------|-------|
| **0: Context** | Gather constraints, goals, existing work | Claude |
| **0.5: Ground** | Web-verify all technologies, prices, versions | Flash-Lite (grounded) + Claude WebSearch |
| **R1: Diverge** | Gemini challenges your framing, proposes 5+ angles | Pro (ungrounded) |
| **R1.5: Verify** | Check any new tech Gemini introduced | Flash-Lite (grounded) |
| **R2: Deepen** | Claude kills weak ideas, Gemini stress-tests survivors | Pro (ungrounded) |
| **Check-in** | User picks preference before final convergence | You |
| **R3: Converge** | One winner, one timeline, one go/no-go signal | Pro (ungrounded) |
| **3.5: Fact-check** | Dual-verify all claims in the final decision | Flash-Lite + Claude WebSearch |
| **Synthesize** | Summary table, kill list, final recommendation | Claude |

### Why Two Layers?

**Flash** ($0.25/1M tokens) searches the web and verifies facts. **Pro** ($2/1M tokens) does deep reasoning on pre-verified context. This way Pro never wastes expensive thinking tokens on factual lookups.

In v2, we sent everything to Pro with `--grounded`. Problem: Pro spent 40% of thinking tokens parsing search results instead of challenging ideas. v2.1 splits the work — faster, cheaper, better quality.

## Usage

| You say | What happens |
|---------|-------------|
| "Brainstorm how to launch X" | Full 3-round cycle with web grounding |
| "Let's think through options" | Activates with context gathering phase |
| "Explore this idea with Gemini" | Diverge → Deepen → Converge |
| "Diverge and converge on X" | Direct trigger, skips small talk |
| "I need more than a second opinion" | Upgrade from single Gemini call to full brainstorm |

## Cost Per Brainstorm

| Component | Calls | Est. Cost |
|-----------|-------|-----------|
| Flash-Lite (grounding) | 2-3 | ~$0.03 |
| Pro (reasoning) | 3 | ~$0.30 |
| Claude (orchestration) | Included in your session | $0 extra |
| **Total** | | **~$0.35** |

## Key Principles

1. **Flash researches, Pro reasons** — never waste Pro's tokens on factual lookups
2. **Web-ground before reasoning** — stale facts poison all 3 rounds
3. **Kill early, kill often** — R1: 7+ ideas, R2: cut to 3, R3: converge to 1
4. **Constraints are ammunition** — real limits kill impractical ideas
5. **One action, not a strategy** — R3 ends with a single deliverable + timeline
6. **Go/no-go criteria** — every brainstorm ends with "if X doesn't happen by Y, abandon"
7. **Show the funnel** — user sees the journey (7 → 3 → 1) so the winner is justified

## Gotchas

- **Requires `GOOGLE_API_KEY`** — without it, Gemini calls fail silently. Check your `.env`
- **`google-genai` not `google-generativeai`** — the new SDK package name (March 2026)
- **User check-in after R2 is mandatory** — prevents models from converging on something you don't want
- **Additional rounds are possible** — R4+ when go/no-go test produces new data or fact-check invalidates R3
- **Flash-Lite model ID is `gemini-3.1-flash-lite-preview`** — not Flash, not Lite separately

## Part of the AWRSHIFT Ecosystem

- [**skill-awrshift**](https://github.com/awrshift/skill-awrshift) — adaptive decision-making framework (Quick / Standard / Scientific)
- [**AWRSHIFT Framework**](https://github.com/awrshift/awrshift) — the full methodology
- [**ClawClaw Soul**](https://clawclawsoul.com) — persistent identity protocol for AI agents

## Contributing

1. Fork the repository
2. Create a feature branch
3. Submit a pull request

## License

MIT — see [LICENSE](LICENSE) for details.

---

<div align="center">
<em>One idea in. One decision out.</em>
</div>
