# Validation Contract

## Goal

在不依赖任何外部脚本的前提下，主任务必须基于本文件完成目标 Skill 的最低覆盖度检查，并把结果写入 `validation/validation-report.md`。

## Step 1 — Confirm Required Files

以下文件必须存在：

- `SKILL.md`
- `references/research/01-writings.md`
- `references/research/02-conversations.md`
- `references/research/03-expression-dna.md`
- `references/research/04-external-views.md`
- `references/research/05-decisions.md`
- `references/research/06-timeline.md`
- `references/research/07-cross-validation.md`
- `references/research/shared-knowledge-base.md`

缺少任一文件，都不得直接交付。

## Step 2 — Confirm Canonical Headings

以下章节必须出现在每个 research 文件中：

- `## Summary`
- `## Key Findings`
- `## Evidence`
- `## Sources`
- `## Contradictions`
- `## Gaps`
- `## Confidence`

如果某个章节不存在，必须先补齐结构，再继续验证。

## Step 3 — Confirm Source Tags

每个 research 文件至少出现 `1` 组来源标记：

- `**来源**:`
- `**URL**:`
- `**质量评分**:`

如果只写结论不写来源，视为未通过。

## Step 4 — Check Coverage Floors

按 `references/output-contracts.md` 中的 Coverage Floors 逐项检查。重点看：

- 来源数量是否达标
- 一手来源是否不足
- 是否覆盖冲突与缺口
- 是否有近 `12` 个月动态
- 交叉验证是否给出第二轮建议

若未达标，必须标记为 `Needs round two` 或 `Needs rewrite`。

## Step 5 — Check Distillation Outputs

最终目标 Skill 至少应满足：

- `3-7` 个心智模型
- `5-10` 条决策启发式
- `3-5` 个表达 DNA 关键特征
- 至少 `2` 组内部张力
- 明确的诚实边界

若任何一项缺失，不得判定 `Pass`。

## Step 6 — Write the Validation Report

主任务必须将检查结果写入：

- `validation/validation-report.md`

报告结构参考：

- `references/validation-report-template.md`
- `templates/target-skill/validation/validation-report.md.tpl`

## Allowed Decisions

最终结论只允许三种：

- `Pass`
- `Needs round two`
- `Needs rewrite`

禁止写模糊结论，例如“差不多可以”“大致完成”。
