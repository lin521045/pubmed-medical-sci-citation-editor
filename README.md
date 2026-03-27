# PubMed Medical SCI Citation Editor / PubMed 医学 SCI 引文编辑技能

This repository contains a Codex skill for inserting precise, PubMed-verified citations into medical SCI manuscripts and producing a `Nature Communications`-style reference list.

本仓库提供一个 Codex skill，用于在医学 SCI 稿件中插入精准、经 PubMed 核验的参考文献，并输出符合 `Nature Communications` 风格的参考文献列表。

## Overview / 项目概览

The skill is designed for high-standard medical academic editing scenarios such as Introduction and Discussion citation enrichment, Methods source normalization, and full-manuscript reference auditing.

该 skill 面向高标准医学学术编辑场景，适用于引言与讨论部分补充引文、方法学来源规范化，以及整篇稿件的参考文献合规审计。

## Core Guarantees / 核心约束

- PubMed tool or API use is mandatory for every reference.
- No hallucinated citations and no citation dumping.
- Evidence hierarchy is enforced.
- Citation recency, section distribution, and single-use rate are audited mathematically.
- Introduction citation insertions are constrained to 12-18, and Discussion must contain at least as many insertions as Introduction.
- In-text citations use superscript numbering after punctuation.
- Reference lists follow `Nature Communications` style.

- 每一条参考文献都必须通过 PubMed 工具或 API 核验。
- 严禁虚构引文，严禁无关文献堆砌。
- 严格遵循证据等级优先原则。
- 对文献时效性、章节分布和单次使用率进行数学审计。
- `Introduction` 的引文插入数限制在 12-18 之间，且 `Discussion` 的引文插入数不得少于 `Introduction`。
- 文内引文采用标点后上标编号。
- 参考文献列表遵循 `Nature Communications` 格式。

## Repository Layout / 仓库结构

```text
.
├── README.md
└── pubmed-medical-sci-citation-editor
    ├── SKILL.md
    ├── agents/openai.yaml
    └── references/pubmed-query-and-audit.md
```

## How To Use / 使用方式

1. Place the `pubmed-medical-sci-citation-editor` folder inside `~/.codex/skills`, or symlink it there.
2. Invoke the skill with `$pubmed-medical-sci-citation-editor`.
3. Paste your manuscript draft or target section and let Codex execute the four required phases.

1. 将 `pubmed-medical-sci-citation-editor` 文件夹放入 `~/.codex/skills`，或建立软链接。
2. 使用 `$pubmed-medical-sci-citation-editor` 调用该技能。
3. 粘贴你的论文草稿或目标章节，让 Codex 按四个阶段执行。

## Example Prompt / 示例调用

```text
Use $pubmed-medical-sci-citation-editor to revise the Introduction and Discussion of my manuscript, insert precise PubMed-verified citations, and output the final compliance audit.
```

```text
使用 $pubmed-medical-sci-citation-editor 修改我的论文引言和讨论部分，插入经过 PubMed 核验的精准引文，并输出最终合规审计。
```

## Notes / 说明

The skill is intentionally strict: if a PubMed tool is unavailable, it should stop rather than invent references.

该 skill 的设计目标是“宁缺毋滥”：如果没有 PubMed 工具，它应当停止执行，而不是虚构参考文献。
