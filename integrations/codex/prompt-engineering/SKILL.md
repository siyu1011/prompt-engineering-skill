---
name: prompt-engineering
description: Design, refine, and evaluate prompts for LLM tasks. Use when Codex needs to write or improve system prompts, user prompts, reusable prompt templates, few-shot examples, structured-output prompts, prompt chains, or prompt debugging workflows for summarization, extraction, classification, rewriting, planning, coding, agent tasks, or retrieval-grounded generation.
---

# Prompt Engineering

## Overview

Turn vague requests into reliable prompts, with explicit task framing, context handling, output constraints, and technique selection. Prefer simple prompts first, then add examples, decomposition, or retrieval only when the task actually needs them.

## Workflow

1. Identify the true task type before writing the prompt: generation, rewriting, extraction, classification, reasoning, tool use, or retrieval-grounded answering.
2. Gather only the context that changes the answer. Do not bury the model in background that is irrelevant to the requested output.
3. State the instruction first. Then provide context, input data, constraints, and required output format.
4. Make the output testable. Specify schema, sections, style boundaries, acceptance criteria, and failure behavior.
5. Escalate technique only as needed: zero-shot -> few-shot -> decomposition -> retrieval/tool use.

## Prompt Skeleton

Use this default structure unless the task needs a different format:

```text
[Role or operating stance, only if useful]

Task:
- What to do
- What to optimize for

Context:
- Domain facts, policies, or source material

Input:
"""
{user_input}
"""

Requirements:
- Boundaries, constraints, style, exclusions
- How to handle ambiguity or missing information

Output format:
- Exact schema, sections, or JSON shape
```

## Technique Selection

### Use plain instruction first

Use direct prompting for simple transformations, summaries, rewrites, and straightforward content generation. Be specific about what good output looks like.

### Add examples for pattern matching

Use few-shot prompting when the model must imitate a format, tone, label set, extraction rule, or transformation pattern. Keep examples representative and consistent.

### Add structure for deterministic outputs

For extraction, classification, grading, and downstream automation:

- Define fields explicitly.
- Use delimiters around source text.
- Specify allowed labels or value ranges.
- Require valid JSON or a fixed section layout.

Read [templates.md](./references/templates.md) for reusable extraction and classification templates.

### Decompose hard reasoning tasks

For multi-step analysis, planning, or math-like reasoning, ask for staged work instead of one-shot output. Prefer visible intermediate artifacts such as assumptions, plan, sub-results, or a concise reasoning summary. Do not ask for hidden internal chain-of-thought; ask for brief, useful justification.

Choose among these patterns:

- Chain-of-thought style scaffolding: ask for stepwise analysis when the task benefits from explicit decomposition.
- Least-to-most: solve simpler subproblems first, then combine them.
- Step-back prompting: first extract the governing principle or abstraction, then solve the instance.
- Tree-of-thought style branching: only for unusually ambiguous planning/search tasks where multiple candidate paths matter.

Read [techniques.md](./references/techniques.md) for selection guidance.

### Ground answers with retrieval when facts matter

If correctness depends on external facts, recent information, policies, or proprietary documents, do not rely on memory alone. Use retrieval-grounded prompts, quote or cite the supplied sources when needed, and state what to do when the context is insufficient.

### Chain prompts for brittle workflows

Split complex tasks into sequential prompts when one prompt would mix incompatible goals, such as research -> synthesis -> formatting, or extraction -> validation -> reporting.

## Writing Rules

- Put the main instruction before the long context.
- Say what to do, not only what to avoid.
- Specify the target audience, tone, and verbosity only when they matter.
- Prefer constraints that can be checked mechanically.
- Keep variable parts parameterized so the prompt becomes reusable.
- If a role helps, make it operational, not theatrical.
- When the model must admit uncertainty, state that explicitly.

## Reusable Deliverables

When the user asks for a prompt-related artifact, default to one of these outputs:

- A final prompt ready to paste into a model.
- A parameterized template with placeholders.
- A short rationale explaining why the structure works.
- A test set with 3-5 cases if the prompt will be reused.

## Debugging Checklist

When a prompt underperforms, inspect these failure modes in order:

1. The task is underspecified.
2. The context is missing, noisy, or stale.
3. The output format is ambiguous.
4. The prompt is trying to do too many things at once.
5. The task actually needs examples.
6. The task actually needs retrieval, tools, or a prompt chain.

## Reference Files

- Read [templates.md](./references/templates.md) when you need reusable prompt templates for common task types.
- Read [techniques.md](./references/techniques.md) when you need a quick map from problem type to prompting technique.
- Read [chinese-templates.md](./references/chinese-templates.md) when the prompt will be written or used mainly in Chinese.
- Read [system-prompts.md](./references/system-prompts.md) when designing agent prompts, system prompts, tool-using assistants, or persistent operating instructions.
- Read [prompt-diffs.md](./references/prompt-diffs.md) when improving weak prompts through concrete before/after examples.
- Read [scenario-templates.md](./references/scenario-templates.md) when the prompt should match a business or workflow context such as support, sales, recruiting, coding, research, or RAG.
- Read [prompt-review-checklist.md](./references/prompt-review-checklist.md) when reviewing an existing prompt and returning fixed diagnostic output.
