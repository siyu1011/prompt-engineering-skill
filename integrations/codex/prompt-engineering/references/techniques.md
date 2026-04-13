# Technique Guide

This file maps common prompt problems to the simplest effective technique.

## Core Principles

- Start simple and add complexity only when failure proves it is needed.
- Place instructions before long context.
- Make outputs explicit and checkable.
- Prefer positive directions over long "do not" lists.
- Use delimiters for source text and schemas for outputs.

## Choose the Technique

### Zero-shot

Use when the task is familiar and the desired output is obvious from the instruction.

Typical cases:
- Summarization
- Rewriting
- Basic drafting
- Short explanation

### Few-shot

Use when the task depends on a specific pattern that is easier to show than describe.

Typical cases:
- Labeling
- Tone imitation
- Format transfer
- Data normalization

Risk:
- Bad examples teach the wrong rule.

### Chain-of-thought style scaffolding

Use when accuracy improves if the task is decomposed into visible steps.

Typical cases:
- Multi-constraint reasoning
- Analysis with tradeoffs
- Logic-heavy tasks

Implementation note:
- Ask for concise intermediate steps or a reasoning summary, not hidden internal reasoning.

### Self-consistency

Use only when a single reasoning path is brittle and you can afford repeated attempts. Generate multiple candidate reasoned answers and pick the most consistent result.

Typical cases:
- Hard reasoning
- Edge-case math or logic

### Least-to-most

Use when the task can be solved reliably by handling simpler subproblems first.

Typical cases:
- Long reasoning chains
- Planning from prerequisites
- Compound questions

### Step-back prompting

Use when the model jumps into details too early. Ask for the governing principle first, then the case-specific answer.

Typical cases:
- Strategy
- Architecture
- Policy interpretation
- Teaching explanations

### Tree-of-thought style branching

Use sparingly for search-style or planning-style tasks where multiple branches should be compared before committing.

Typical cases:
- Planning with alternatives
- Puzzle-like search
- Strategy exploration

### Generated knowledge

Use when the answer benefits from first producing relevant background statements, heuristics, or facts and then using them in the final answer.

Typical cases:
- Domain reasoning
- Concept explanation
- Tasks needing intermediate knowledge recall

### Prompt chaining

Use when one prompt is overloaded.

Typical cases:
- Research -> synthesis -> formatting
- Extraction -> validation -> summary
- Planning -> execution -> review

### Retrieval-augmented generation

Use when correctness depends on facts outside the model's reliable memory or on proprietary/current documents.

Typical cases:
- Policy QA
- Documentation assistants
- Knowledge base search
- Up-to-date factual answers

## Escalation Ladder

Use this order unless you have a clear reason not to:

1. Direct instruction
2. Add explicit output format
3. Add examples
4. Add decomposition
5. Split into prompt chain
6. Add retrieval or tools

## Anti-Patterns

- One prompt trying to research, reason, write, and format all at once
- Missing schema for machine-consumed output
- Overly theatrical role-play that adds no operational guidance
- Large irrelevant context dumps
- Negative-only instructions without a positive target
- Asking for certainty where the evidence is incomplete
