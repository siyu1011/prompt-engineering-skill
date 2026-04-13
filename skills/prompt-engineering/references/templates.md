# Prompt Templates

Use these as starting points. Replace placeholders and delete instructions that are not needed.

## 1. General Task Prompt

```text
Task:
{what_to_do}

Context:
{relevant_context}

Input:
"""
{input}
"""

Requirements:
- Optimize for {goal}
- Respect these constraints: {constraints}
- If information is missing, say exactly what is missing instead of inventing it

Output format:
{format}
```

## 2. Rewrite / Transform

```text
Rewrite the following text for {target_audience}.

Goals:
- Preserve the original meaning
- Change the style to {style}
- Keep it within {length_constraint}

Text:
"""
{input_text}
"""

Return:
- Rewritten version
- Optional note: mention any ambiguity or information loss
```

## 3. Structured Extraction

```text
Extract the requested fields from the source text.

Rules:
- Use only information explicitly present in the source
- If a field is missing, return null
- Do not infer values that are not supported by the text

Return valid JSON with this schema:
{
  "field_1": "string|null",
  "field_2": "string|null",
  "field_3": ["string"]
}

Source:
"""
{source_text}
"""
```

## 4. Classification

```text
Classify the input into exactly one label from this set:
- {label_1}
- {label_2}
- {label_3}

Decision rules:
- {rule_1}
- {rule_2}
- If the input is ambiguous, choose the best label and set confidence below 0.7

Return valid JSON:
{
  "label": "one-of-the-allowed-labels",
  "confidence": 0.0,
  "evidence": ["short quote or reason"]
}

Input:
"""
{input}
"""
```

## 5. Few-Shot Pattern Prompt

```text
Follow the pattern shown in the examples.

Example 1
Input:
{example_input_1}
Output:
{example_output_1}

Example 2
Input:
{example_input_2}
Output:
{example_output_2}

Now perform the same transformation.

Input:
{new_input}
```

## 6. Stepwise Analysis

```text
Solve the task in stages.

Task:
{task}

Stages:
1. Identify the key facts, assumptions, or constraints.
2. Break the problem into smaller steps.
3. Produce the answer.
4. Briefly verify the answer against the original task.

Return:
- Assumptions
- Steps
- Final answer
- Verification
```

## 7. Step-Back Prompt

```text
First identify the higher-level principle or framework that should guide the answer.
Then use that principle to solve the concrete task.

Task:
{task}

Return:
- Principle
- Application to this case
- Final answer
```

## 8. Retrieval-Grounded QA

```text
Answer the question using only the supplied context.

If the context is insufficient, say "insufficient context" and list the missing facts.
Do not use unstated background knowledge.

Context:
"""
{retrieved_context}
"""

Question:
{question}

Return:
- Answer
- Evidence: cite the supporting passage or section
```

## 9. Prompt Debugging

```text
You are improving a prompt that is currently underperforming.

Current prompt:
"""
{current_prompt}
"""

Observed failure:
{failure_mode}

Task:
- Diagnose why the prompt fails
- Produce an improved prompt
- Explain the changes briefly
- Suggest 3 test cases

Return:
- Diagnosis
- Revised prompt
- Test cases
```

## 10. System Prompt Template

```text
You are a {role}.

Primary objective:
- {objective}

Operating rules:
- {rule_1}
- {rule_2}
- {rule_3}

Failure behavior:
- If required information is missing, {fallback_behavior}

Output contract:
- {format_requirements}
```
