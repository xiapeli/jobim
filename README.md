<div align="center">

<img src=".github/social-preview.png" alt="Jobim — AI Agent Orchestrator" width="100%">

# Jobim

**Multi-agent orchestrator for Claude Code — from idea to shipped product**

[![MIT License](https://img.shields.io/badge/License-MIT-gold.svg?style=for-the-badge)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude_Code-Skill-blue?style=for-the-badge)](https://claude.ai)
[![Agents](https://img.shields.io/badge/Agents-8-green?style=for-the-badge)](.claude/agents/)
[![Pipeline](https://img.shields.io/badge/Phases-5-purple?style=for-the-badge)]()

*Named after Tom Jobim — like bossa nova harmonizes simplicity with complexity,
Jobim orchestrates specialized AI agents to build complete applications.*

[Install](#quick-start) · [Agents](#the-8-agents) · [Pipeline](#pipeline) · [PRD Loop](#autonomous-mode-prd-loop) · [Contributing](#contributing)

</div>

---

## What It Does

One prompt. Eight agents. Full-stack delivery.

You describe what you want. Jobim (Claude Opus) breaks it into phases and delegates to 7 specialized sub-agents. Each agent has deep domain expertise, structured JSON contracts, and quality gates.

No manual coordination. No context-switching. From idea to deployed product.

```
/jobim new "Create a task management SaaS with real-time collaboration"
```

Jobim plans the work, delegates to Scout for market research, Builder for code, Designer for the design system, Tester for quality gates, and ships it.

## Architecture

```
┌──────────────────────────────────────────────────────────────┐
│  USER — provides high-level objective                        │
└────────────────────────────┬─────────────────────────────────┘
                             ▼
┌──────────────────────────────────────────────────────────────┐
│  JOBIM (Opus) — Orchestrator                                 │
│  Plans, delegates, synthesizes, decides                      │
│  Maintains state in .jobim/state.json                        │
│  NEVER executes code — always delegates                      │
└───────┬──────┬──────┬──────┬──────┬──────┬──────┬────────────┘
        ▼      ▼      ▼      ▼      ▼      ▼      ▼
┌──────────────────────────────────────────────────────────────┐
│  SUBAGENTS (Haiku / Sonnet)                                  │
│                                                              │
│  Scout   Builder  Tester  Designer  UXer  Shipper  Launcher  │
│  (Haiku) (Sonnet) (Sonnet) (Sonnet) (Sonnet) (Sonnet) (Sonnet) │
│                                                              │
│  Execute specific tasks → Return structured JSON             │
└──────────────────────────────────────────────────────────────┘
```

## The 8 Agents

| Agent | Model | What It Does |
|-------|-------|-------------|
| **Jobim** | Opus | Orchestrates the full pipeline. Plans, delegates, synthesizes results. Never writes code directly. |
| **Scout** | Haiku | Market research, competitor analysis, tech stack recommendation, viability scoring |
| **Builder** | Sonnet | Full-stack implementation — React, Next.js, APIs, databases, responsive layouts |
| **Designer** | Sonnet | Design systems, HSL color tokens, typography scales, spacing, visual effects |
| **UXer** | Sonnet | Flow analysis, friction audit, Nielsen heuristics, WCAG accessibility, conversion optimization |
| **Tester** | Sonnet | Code review, OWASP security scan, test writing, quality gates |
| **Shipper** | Sonnet | Docker configs, GitHub Actions CI/CD, deploy pipelines, monitoring |
| **Launcher** | Sonnet | README generation, social posts (X/LinkedIn), Product Hunt copy, launch checklist |

## Pipeline

Five phases, each with dedicated agents and quality gates:

```
Discovery → Prototype → Production → Ship → Launch
  Scout      Builder     Builder +    Shipper  Launcher
  (Haiku)    (Sonnet)    Tester       (Sonnet) (Sonnet)
                         (parallel)
```

### State Tracking

Jobim persists state across the session in `.jobim/state.json`:

```json
{
  "version": "2.0",
  "phase": { "current": "discovery", "completed": [], "history": [] },
  "context": {
    "discovery": null,
    "prototype": null,
    "production": null,
    "ship": null,
    "launch": null
  },
  "decisions": [],
  "artifacts": []
}
```

## Quick Start

### Option 1: Install agents only (safe, non-destructive)

```bash
git clone https://github.com/xiapeli/jobim.git
cd jobim

# Copy agents and commands (won't overwrite existing files)
mkdir -p ~/.claude/agents ~/.claude/commands
cp -n .claude/agents/*.md ~/.claude/agents/
cp -n .claude/commands/*.md ~/.claude/commands/
```

### Option 2: Full install with settings

```bash
git clone https://github.com/xiapeli/jobim.git
cd jobim

# Back up your existing config first
[ -d ~/.claude ] && cp -r ~/.claude ~/.claude.backup.$(date +%s)

# Install everything
mkdir -p ~/.claude/agents ~/.claude/commands
cp .claude/agents/*.md ~/.claude/agents/
cp .claude/commands/*.md ~/.claude/commands/
cp .claude/settings.json ~/.claude/settings.json
```

### Usage

```bash
# Full autonomous pipeline
/jobim new "Create a task management SaaS"

# Interactive mode — pause for approval at each phase
/jobim new "Create a meditation app" interactive

# Run a specific phase only
/jobim run design

# Check progress
/jobim status

# Use individual agents directly
/scout "Research design system trends 2026"
/builder "Create a responsive landing page"
/designer "Design system for a fitness app"
/tester "Review the auth module for security issues"
```

## Autonomous Mode (PRD Loop)

Jobim includes a PRD-driven autonomous loop based on the [Ralph Pattern](https://ghuntley.com/specs/). Define user stories in a `prd.json`, and Jobim implements them one by one:

```bash
cd prd-loop
cp prd.json.example prd.json  # edit with your user stories
./jobim-loop.sh 10            # run up to 10 iterations
```

Each iteration:
1. Reads the PRD and progress log
2. Implements the next incomplete user story
3. Commits the work
4. Updates the progress file
5. Stops when all stories pass or max iterations reached

> **Note:** The PRD loop uses `--dangerously-skip-permissions` to run without interactive prompts. This allows fully autonomous operation but gives Claude unrestricted tool access. Review the [prompt.md](prd-loop/prompt.md) before running.

## Design Library

Jobim includes a curated design library with:
- **159 reference screenshots** from award-winning sites
- **Curated references** organized by category (SaaS, portfolio, e-commerce, etc.)
- **Design system patterns** extracted from top implementations

See [`design-library/`](design-library/) for the full collection.

## Contract System

Every agent follows structured contracts:
- **Input contract**: Required and optional parameters with types
- **Output contract**: JSON schema defining the response format
- **Quality gates**: Conditions that must pass before Jobim accepts the output

When a quality gate fails, Jobim retries (up to 3 times), then escalates with full context.

## Requirements

- [Claude Code](https://claude.ai) with API access
- Claude Opus for the orchestrator (Jobim agent)
- Claude Sonnet/Haiku for sub-agents

## Contributing

Contributions welcome. See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

Ideas for contributions:
- New specialized agents (e.g., Analytics, Copywriter, SEO)
- Additional design library references
- Language translations for agent prompts
- Example PRDs for common project types

## License

[MIT](LICENSE) — Phelipe Xavier, 2026
