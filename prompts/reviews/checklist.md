# Prompt Review Checklist

Use this file when the user gives you an existing prompt and wants diagnosis plus improvements. Default to this fixed output structure unless the user asks otherwise.

## Fixed Review Output

```text
Prompt review

1. Task understanding
- What the prompt is trying to achieve
- Whether the task is clearly defined

2. Main problems
- Missing task definition
- Missing context
- Ambiguous output format
- Conflicting goals
- Lack of examples
- Missing retrieval/tooling requirements

3. Risk assessment
- What kinds of bad outputs this prompt is likely to produce

4. Improved prompt
- A revised version ready to use

5. Why the revision is better
- 3-5 concrete reasons

6. Suggested test cases
- 3-5 inputs that would expose weaknesses or verify correctness
```

## Review Procedure

1. Identify the actual job the prompt is supposed to do.
2. Check whether success can be evaluated from the prompt alone.
3. Look for missing context, undefined terms, and vague quality words such as "better" or "professional".
4. Check whether the output format is explicit enough for the downstream use.
5. Decide whether the prompt needs examples, decomposition, retrieval, or tools.
6. Rewrite with the smallest changes that materially improve reliability.

## What To Diagnose

### Task definition

Check:
- Is the task stated clearly?
- Is the target user or audience defined?
- Is the success criterion explicit?

Common failure:
- The prompt asks for "optimize", "analyze", or "improve" without saying by what standard.

### Context quality

Check:
- Is the model given the minimum necessary background?
- Is important context missing?
- Is there too much irrelevant context?

Common failure:
- The prompt includes a large dump of information with no instruction on what matters.

### Output contract

Check:
- Does the prompt specify sections, schema, labels, or formatting?
- If structured output is required, is type information clear?
- Is there a rule for missing values?

Common failure:
- The prompt expects machine-readable output but never defines the schema.

### Constraints and boundaries

Check:
- Does the prompt define what the model should not infer?
- Does it say how to handle uncertainty?
- Does it constrain tone, length, or evidence use where needed?

Common failure:
- The prompt wants confident output even when the evidence may be incomplete.

### Technique choice

Check:
- Would a direct prompt suffice?
- Does the task need few-shot examples?
- Does it need decomposition?
- Does it need retrieval or tool use?

Common failure:
- A complicated task is forced into one vague one-shot prompt.

## Minimal Review Template

```text
Please review the prompt below.

Prompt:
"""
{prompt}
"""

Return:
1. A short diagnosis of the main weaknesses
2. A revised prompt
3. A short explanation of why the revision is better
4. 3 test cases to validate it
```

## Chinese Review Template

```text
请评审下面这段提示词，并按固定结构返回结果。

提示词：
"""
{prompt}
"""

请输出：
1. 这段提示词想完成什么任务
2. 主要问题有哪些
3. 可能导致哪些错误输出
4. 优化后的提示词
5. 为什么这样改
6. 3 个测试用例
```
