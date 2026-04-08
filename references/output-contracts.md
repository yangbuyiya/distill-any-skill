# Output Contracts

## Research File Header

每个 research 文件顶部必须包含：

```md
# 调研日期
YYYY-MM-DD

# Agent
Agent X - <name>

# 信息标注规则
- 一手：本人原话、原文、原始视频/音频、官方材料
- 二手：权威媒体深访、授权传记、长期跟踪报道
- 推断：基于现有材料的合理归纳，不冒充事实
```

## Canonical Sections

所有 `references/research/*.md` 文件统一使用以下结构：

```md
## Summary
3-8 条本维度核心结论

## Key Findings
- 结论
- 证据摘要
- 标签：一手 / 二手 / 推断

## Evidence
- [E1] 证据摘要
- [E2] 证据摘要

## Sources
**来源**: <名称>
**URL**: <链接或注明离线来源>
**质量评分**: 权威性X | 一手性X | 完整性X | 时效性X | 综合X

## Contradictions
- 冲突点
- 可能解释

## Gaps
- 信息缺口
- 建议补强方向

## Confidence
- 高置信：
- 中置信：
- 低置信：
```

## Source Scoring

每个来源都按四个维度打分：

### 1. 权威性
- `5`：本人著作、官方档案、授权传记
- `4`：权威媒体深访、知名播客完整访谈
- `3`：高质量评论、书评、外部分析
- `2`：一般媒体报道、普通博客
- `1`：零散片段、低质量整理

### 2. 一手性
- `5`：本人原话、原文、原始音视频
- `4`：第一手观察者记录
- `3`：基于一手材料的分析
- `2`：二手转述
- `1`：多次转述

### 3. 完整性
- `5`：完整书籍 / 完整访谈 / 全文
- `4`：主要内容保留
- `3`：关键片段
- `2`：摘要或节选
- `1`：零散引文

### 4. 时效性
- `5`：近 `6` 个月
- `4`：`6-12` 个月
- `3`：`1-3` 年
- `2`：`3-5` 年
- `1`：`5` 年以上

## Coverage Floors

### Agent 1 — Writings
- 至少 `3` 本核心著作或等量系统性长文
- 至少 `2` 个自创术语
- 至少 `5` 个重复出现 `>=3` 次的观点

### Agent 2 — Conversations
- 至少 `3` 个深度访谈
- 至少 `2` 个立场变化时刻
- 至少 `1` 个即兴类比

### Agent 3 — Expression DNA
- 至少 `20` 个表达样本
- 至少 `10` 个高频词
- 至少 `3` 个常见句式

### Agent 4 — External Views
- 至少 `3` 个不同角度的外部评价
- 至少 `2` 个常见批评
- 至少 `1` 个争议事件

### Agent 5 — Decisions
- 至少 `3` 个成功案例
- 至少 `2` 个失败案例
- 至少 `1` 个言行不一致案例

### Agent 6 — Timeline
- 至少 `10` 个重要节点
- 至少 `3` 个思想转折点
- 近 `12` 个月至少 `3` 个动态

### Agent 7 — Cross Validation
- 至少 `5` 个关键人物关系
- 至少 `2` 个冲突或验证点
- 至少 `1` 份第二轮建议

## Distillation Output Contract

提炼阶段至少产出：

- `3-7` 个心智模型
- `5-10` 条决策启发式
- `3-5` 个表达 DNA 关键特征
- 至少 `2` 组内部张力
- 明确的诚实边界

## Validation Contract

最终 Skill 至少完成：

1. 已知问题一致性测试 `3` 条
2. 边缘问题推断测试 `1` 条
3. 风格辨识度测试 `1` 条

若任一测试失败，返回提炼阶段修正，不直接交付。

## Module-First Validation Workflow

验证阶段不得依赖任何外部 Python 脚本。主任务必须：

1. 读取 `references/validation-contract.md`
2. 检查必需文件是否存在
3. 检查每个 research 文件是否具备统一 heading
4. 检查来源标记与 Coverage Floors 是否达标
5. 按 `references/validation-report-template.md` 将结果写入目标 Skill 的 `validation/validation-report.md`
6. 只有当验证结论为 `Pass` 时才允许交付
