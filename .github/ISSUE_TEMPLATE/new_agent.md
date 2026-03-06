---
name: New Agent Proposal
about: Propose a new agent for the Jobim pipeline
title: "[AGENT] "
labels: agent-proposal
assignees: ''
---

## Agent Name

What should this agent be called?

## Pipeline Phase

Which phase will this agent operate in?

- [ ] Discovery
- [ ] Prototype
- [ ] Production
- [ ] Ship
- [ ] Launch

## Purpose

What is the agent's primary responsibility? Describe the problem it solves and why existing agents cannot handle it.

## Model Selection

Which Claude model should this agent use?

- [ ] **Haiku 4.5** — Lightweight, frequent invocation, worker agents, pair programming
- [ ] **Sonnet 4.6** — Main development, orchestration, complex coding tasks
- [ ] **Opus 4.5** — Deep reasoning, complex architecture, research and analysis

### Model Justification

Explain why the selected model is appropriate for this agent's workload. Consider:

- Task complexity (simple extraction vs. deep reasoning)
- Invocation frequency (called once vs. called per-file)
- Cost implications (Haiku is 3x cheaper than Sonnet)
- Latency requirements (real-time vs. batch)

## Input Contract

Define exactly what the agent receives as input.

```yaml
input:
  required:
    - name: ""
      type: ""
      description: ""
  optional:
    - name: ""
      type: ""
      description: ""
```

## Output Contract

Define exactly what the agent produces as output.

```yaml
output:
  format: ""  # e.g., markdown, JSON, file
  schema:
    - field: ""
      type: ""
      description: ""
```

## Quality Gates

What criteria must this agent's output meet before it can be passed to the next phase?

- [ ] Gate 1: [e.g., Output passes JSON schema validation]
- [ ] Gate 2: [e.g., All required fields are non-empty]
- [ ] Gate 3: [e.g., Confidence score >= 0.8]
- [ ] Gate 4: [e.g., No hallucinated data (verified against source)]

## Error Handling

How should the agent handle failures?

- **Retry strategy**: [e.g., 3 retries with exponential backoff]
- **Fallback**: [e.g., Degrade to simpler model, return partial results]
- **Escalation**: [e.g., Flag for human review]

## Dependencies

- **Upstream agents**: Which agents feed data into this one?
- **Downstream agents**: Which agents consume this agent's output?
- **External tools/APIs**: Any external services required?

## Example Interaction

Provide a concrete example of input and expected output.

### Input Example
```
(paste example input here)
```

### Expected Output Example
```
(paste example output here)
```

## Additional Context

Any references, prior art, or design considerations.
