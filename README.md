# Prompt Engineering Toolkit

> 一个面向多种 AI 工具的 Prompt 工具包，内置 Codex、ChatGPT、Claude、Cursor、Dify 适配层。

## 这个仓库是做什么的

很多 Prompt 资料要么绑定在某个产品里，要么只是零散笔记，不方便复用，也不方便分享。

这个仓库的目标很直接：

- 核心 Prompt 知识保持平台无关
- 按真实使用场景组织内容，而不是停留在抽象理论
- 为不同 AI 产品提供轻量适配层
- 既能当知识库，也能当可安装的 skill / instructions 包使用

## 什么是 Skill

Skill 可以理解为给 AI 工具使用的“能力包”。它通常把说明、模板、规则和参考资料组合在一起，让 AI 在一类任务上表现得更稳定。

这个仓库包含两层内容：

- 多平台都能直接使用的通用内容
- 面向具体产品的适配层，用于承接各平台自己的 instructions、rules 或 skill 机制

通用内容在 `prompts/` 和 `guides/` 下。  
Codex 专用 skill 在 `integrations/codex/prompt-engineering/` 下。  
其他平台则使用 `integrations/` 下面各自对应的适配文件。

## 快速开始

### 在任意 AI 工具中使用

直接打开 `prompts/` 和 `guides/` 下的文件，复制模板并按任务修改即可。

推荐入口：

- `prompts/general/`：通用 Prompt 模板
- `prompts/chinese/`：中文 Prompt 模板
- `prompts/system/`：System / Agent Prompt 模板
- `prompts/scenarios/`：客服、销售、招聘、代码、研究、RAG 等场景模板
- `prompts/reviews/`：Prompt 评审与审计模板
- `guides/techniques.md`：提示词技术选型
- `guides/prompt-diffs.md`：“差 Prompt -> 好 Prompt” 对照示例

### 在 Codex 中使用

把这个目录复制到全局 Codex skills 目录：

`integrations/codex/prompt-engineering/`

目标路径：

- Windows：`%USERPROFILE%\\.codex\\skills\\`
- macOS/Linux：`~/.codex/skills/`
- 或：`$CODEX_HOME/skills/`

复制后，重新开启一个新的 Codex 会话即可。

## 支持的平台适配

| 平台 | 适配形式 | 目录 |
| --- | --- | --- |
| Codex | 原生 skill | `integrations/codex/` |
| ChatGPT | Custom GPT Instructions | `integrations/chatgpt/` |
| Claude | Project Instructions | `integrations/claude/` |
| Cursor | 规则文件 | `integrations/cursor/` |
| Dify | Agent / System Prompt | `integrations/dify/` |

## 仓库里有什么

### Prompt 资产

- 通用 Prompt 模板
- 中文 Prompt 模板
- System / Agent Prompt 模板
- 按场景划分的 Prompt 模板
- Prompt 评审清单

### 指南

- Prompt 技术选型
- “差 Prompt -> 好 Prompt” 示例
- Prompt 问题诊断与改写结构

### 平台适配层

- Codex skill
- ChatGPT Custom GPT 说明
- Claude Project Instructions
- Cursor 规则文件
- Dify Agent 基础 Prompt

## 仓库结构

```text
prompt-engineering-toolkit/
|- README.md
|- .gitignore
|- prompts/
|  |- chinese/
|  |- general/
|  |- reviews/
|  |- scenarios/
|  `- system/
|- guides/
|  |- prompt-diffs.md
|  `- techniques.md
`- integrations/
   |- chatgpt/
   |- claude/
   |- codex/
   |- cursor/
   `- dify/
```

## 推荐使用方式

### 如果你是个人用户

建议从这里开始：

- `prompts/`：直接拿模板就能用
- `guides/`：想系统理解怎么优化 Prompt 时再看

### 如果你在做 AI 助手或工作流

建议从这里开始：

- `prompts/system/`
- `prompts/reviews/`
- `guides/techniques.md`
- `integrations/` 下对应的平台目录

### 如果你要分享给团队

可以有两种方式：

- 分享整个仓库，作为跨平台 Prompt 工具包
- 只分享 `integrations/` 下某个平台的目录

## 典型使用场景

- 设计一个中文客服分类 Prompt
- 评审一段效果差的 Prompt，并改写成可复用模板
- 为一个 RAG 助手设计 system prompt
- 给团队建立 Prompt 评审流程
- 把一套 Prompt 规范同时复用到多个 AI 平台

## 设计原则

- 先从简单 Prompt 开始，不默认上复杂技巧
- 优先使用清晰结构，而不是模糊措辞
- 只有在模式模仿真的重要时才引入 few-shot
- 只有在正确性依赖外部事实时才引入检索
- 尽量使用占位符，让模板可以长期复用

## 分享方式

这个仓库适合这样分享：

- 如果对方想在任意 AI 工具里使用这些 Prompt 资产，就分享整个仓库
- 如果对方只需要 Codex skill，就分享 `integrations/codex/prompt-engineering/`
- 如果对方只使用某一个平台，就分享对应的 `integrations/` 子目录

## 下一步怎么用

1. 先选对应平台或场景目录
2. 复制一个模板或集成文件
3. 按你的工作流改掉占位符
