# Handover — Claude Code Skill

**Session-state handover docs that survive `/clear` and new sessions.** XML format, one file per day, with an auto-promotion hook into a persistent knowledge base.

> **Buy on Gumroad:** https://moliveiracn.gumroad.com/l/claude-code-handover-skill
> Single-user license · No redistribution · Lifetime updates for the current major version

---

## The problem

When you `/clear` or start a new Claude Code session, you lose:

- What you were in the middle of building
- Why you made the decisions you made
- Non-obvious gotchas you learned the hard way
- The next concrete step

Re-explaining all of this at the top of every session burns tokens and attention. Re-discovering the gotchas wastes hours.

## What this skill does

At session end (or on request), Claude writes a dense, structured handover XML to `.context/handover-YYYY-MM-DD.xml` covering:

- **Task** — one sentence of what's being built right now
- **Session-completed** — items with mandatory `why` attributes (not just `what`)
- **Files-modified** — only where the change isn't obvious from `git diff`
- **Decisions** — constraints for future work
- **Domain** — counterintuitive facts, gotchas, conventions
- **Candidate-rules** — business logic touched this session
- **Open-problems** — what's broken, with error messages
- **Next** — concrete runnable first step, linked to a persistent spec doc

At session start, if a handover file exists, Claude reads the most recent one, confirms the next step with you, and reads the linked spec file before doing anything.

## Trigger phrases

- "handover", "handoff", "write handover", "end session"
- "resume from previous session"
- Also triggers automatically at session start if `.context/handover-*.xml` exists

## Install (after purchase)

1. Unzip the package.
2. Copy the `handover/` folder into your project's `.claude/skills/` directory:

```
your-project/
└── .claude/
    └── skills/
        └── handover/
            └── SKILL.md
```

3. Restart or `/clear` your Claude Code session. The skill auto-loads when triggers match.

## Pairs with

The [**Knowledge** skill](https://github.com/moliveiracn/claude-skill-knowledge) — sold separately. The handover includes a promotion hook: at session end it asks whether to promote durable items (decisions with rationale, domain gotchas, business rules) into a persistent `knowledge.xml`. Together they give Claude Code a two-tier memory: one for the current session, one for the life of the project.

## Requirements

- Claude Code
- A repo with write access to `.context/` (the skill creates this folder if missing)

## License

Single-user, no redistribution. Full terms ship in `LICENSE.txt` inside the zip.
