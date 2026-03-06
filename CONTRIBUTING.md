# Contributing to Jobim

Thanks for your interest in contributing to Jobim.

## How to Contribute

### Reporting Issues

Open an issue with:
- What you expected to happen
- What actually happened
- Steps to reproduce
- Your Claude Code version

### Adding a New Agent

1. Fork and clone the repository
2. Create your agent file in `.claude/agents/your-agent.md`
3. Create the matching command in `.claude/commands/your-agent.md`
4. Follow the existing contract pattern (input/output/quality gates)
5. Add the agent to the pipeline in `jobim.md`
6. Submit a PR with a description of what the agent does

### Pull Requests

1. Fork the repository
2. Create a feature branch (`git checkout -b feat/new-agent`)
3. Commit with conventional commits (`feat:`, `fix:`, `docs:`)
4. Push and open a PR

### Commit Format

```
<type>: <description>

Types: feat, fix, docs, refactor, test, chore
```

## Ideas for Contributions

- New specialized agents (Analytics, Copywriter, SEO, Database)
- Design library additions (more reference screenshots)
- Translations for agent prompts
- Example PRDs for common project types
- Integration tests for the pipeline
