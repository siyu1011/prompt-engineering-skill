# Weak Prompt To Strong Prompt Examples

Use these examples to diagnose why a prompt is weak and how to strengthen it with task definition, constraints, and output contracts.

## 1. Summarization

Weak prompt:

```text
总结一下这篇文章。
```

Why it is weak:
- No target audience
- No length or structure
- No guidance on what matters most

Strong prompt:

```text
请阅读下面的文章，并用中文总结成 3 个部分：
1. 核心结论
2. 支撑结论的关键依据
3. 作者没有明说但值得注意的风险或局限

要求：
- 总字数控制在 300 字以内
- 不要照抄原文句子
- 如果信息不足以支持某个结论，请明确说明

文章：
"""
{article}
"""
```

## 2. Rewrite

Weak prompt:

```text
把这段话改好一点。
```

Why it is weak:
- "好一点" 没有标准
- 不知道面向谁
- 不知道是改语气、结构还是准确性

Strong prompt:

```text
请把下面这段话改写成适合发给客户的中文邮件。

要求：
- 语气专业、克制、礼貌
- 保留原意，不添加新承诺
- 删掉口语化表达和重复句
- 控制在 180 字以内

原文：
"""
{text}
"""
```

## 3. Extraction

Weak prompt:

```text
帮我把信息提取出来。
```

Why it is weak:
- 不知道提取哪些字段
- 不知道缺失值怎么处理
- 不知道结果格式

Strong prompt:

```text
请从下面文本中提取关键信息，并严格输出 JSON。

字段：
- company: string|null
- date: string|null
- amount: string|null
- action: string|null

规则：
- 仅使用文本中明确出现的信息
- 缺失字段填 null
- 不要输出额外解释

文本：
"""
{source}
"""
```

## 4. Classification

Weak prompt:

```text
判断这条工单属于什么问题。
```

Why it is weak:
- 标签集合不明确
- 决策标准不明确
- 没有置信度或证据

Strong prompt:

```text
请将以下工单分类到一个且仅一个标签：
- 账单问题
- 登录问题
- 功能故障
- 咨询需求

规则：
- 优先根据用户的直接诉求分类
- 如果同时涉及多个问题，选择主诉求
- 如果证据不足，仍需选择最接近标签，但将 confidence 设为 0.6 以下

输出 JSON：
{
  "label": "标签",
  "confidence": 0.0,
  "evidence": ["支持判断的短语"]
}

工单内容：
"""
{ticket}
"""
```

## 5. Coding Assistant Prompt

Weak prompt:

```text
帮我修一下这个 bug。
```

Why it is weak:
- 不知道现象、范围、约束
- 不知道是否允许改接口或改测试
- 不知道期望交付物

Strong prompt:

```text
请作为代码助手修复这个 bug。

问题现象：
{bug_description}

代码范围：
{allowed_files_or_modules}

约束：
- 优先做最小修改
- 不要改变现有公共接口，除非确有必要并说明原因
- 如果修复需要补测试，请一起补上

交付：
- 问题原因
- 修复方案
- 修改后的代码
- 验证方式
```

## 6. Research Prompt

Weak prompt:

```text
研究一下这个话题。
```

Why it is weak:
- 没有研究目标
- 没有深度要求
- 没有结果形式

Strong prompt:

```text
请研究这个话题：{topic}

研究目标：
- 说明它是什么
- 解释为什么重要
- 总结当前主要方案或观点
- 指出 3 个关键争议或风险

输出格式：
1. 概览
2. 关键观点
3. 风险与争议
4. 结论

要求：
- 优先给出结构化结论，而不是堆砌信息
- 如果证据不足，单独标记待确认点
```

## 7. System Prompt Improvement

Weak prompt:

```text
给我写一个 AI 助手的 system prompt。
```

Why it is weak:
- 助手的职责不清楚
- 缺少边界和失败处理
- 缺少输出契约

Strong prompt:

```text
请为一个“内部知识库问答助手”编写 system prompt。

助手职责：
- 依据检索到的内部文档回答问题
- 不使用未提供的外部知识补全事实
- 如果资料不足，明确说明

必须包含：
- 角色定义
- 目标与优先级
- 检索内容的使用规则
- 不确定时的处理方式
- 输出格式要求

输出：
- 先给出完整 system prompt
- 再用 5 条说明解释设计意图
```
