# Orchestration Reference

## Default Runtime Model

主任务负责四件事：

1. 创建目标 Skill 目录
2. 并行发起 `6` 个调研 Agent
3. 在 `1-6` 完成后发起 `1` 个交叉验证 Agent
4. 汇总、提炼、构建与验证最终 Skill

默认顺序：

- Phase 0：归一化需求
- Phase 0.5：初始化目录
- Phase 1：六路并行调研
- Phase 1.5：交叉验证
- Phase 1.6：按需二轮补强
- Phase 2：提炼
- Phase 3：构建
- Phase 4：验证
- Phase 5：交付

## Directory Rules

目标 Skill 必须放在：

```text
.codebuddy/skills/<target-slug>/
```

并至少包含：

```text
<target-skill>/
├── SKILL.md
├── references/
│   ├── research/
│   │   ├── 01-writings.md
│   │   ├── 02-conversations.md
│   │   ├── 03-expression-dna.md
│   │   ├── 04-external-views.md
│   │   ├── 05-decisions.md
│   │   ├── 06-timeline.md
│   │   ├── 07-cross-validation.md
│   │   └── shared-knowledge-base.md
│   └── sources/
│       ├── books/
│       ├── transcripts/
│       └── articles/
└── validation/
    └── validation-report.md
```

所有中间产物都必须在目标 Skill 目录内；不得散落到外部目录。

## Template-First Scaffold Protocol

禁止依赖外部初始化脚本。主任务必须：

1. 读取 `templates/target-skill/`
2. 创建 `.codebuddy/skills/<target-slug>/`
3. 渲染模板中的 `{{subject}}` 与 `{{slug}}`
4. 将 `validation/validation-report.md.tpl` 渲染为目标 Skill 中的 `validation/validation-report.md`
5. 若目标 Skill 已存在，则以增量更新方式保留已有研究结果

## Validation Without Scripts

禁止依赖外部校验脚本。主任务必须：

1. 读取 `references/validation-contract.md`
2. 逐项检查 research 文件存在性、章节结构、来源标记与覆盖度门槛
3. 按 `references/validation-report-template.md` 生成 `validation/validation-report.md`
4. 若结果不是 `Pass`，则回到补强或提炼阶段，不直接交付

## Parallel-Agent Contract

每个 Agent 只研究一个维度，不做最终合成。

每个 Agent 输出只允许包含：

- 关键发现
- 证据
- 冲突
- 缺口
- 来源质量判断

每个 Agent 都必须产出到指定文件。若子任务环境不支持直接写文件，则主任务必须在子任务完成后立刻将其原始结果落盘，再继续下一阶段。

## Shared Knowledge Base

文件：`references/research/shared-knowledge-base.md`

用途：

- 记录已发现的高质量来源
- 避免多 Agent 重复搜索同一素材
- 沉淀关键人物、关键事件、关键转折点
- 标注可以被其他 Agent 复用的线索

建议结构：

```md
# Shared Knowledge Base

## High-Value Sources
- 来源
- 质量评分
- 可复用维度

## Key Entities
- 人物 / 组织 / 作品

## Key Events
- 时间点
- 事件
- 涉及维度

## Open Questions
- 待验证问题
```

## Second-Round Triggers

出现以下情况时，进入第二轮调研：

- 某 Agent 来源不足 `3` 个
- 一手来源占比不足 `30%`
- 关键时间点前后缺乏材料
- Agent 7 标出严重冲突
- 时间线缺少最近 `12` 个月动态
- 来源类型过度单一

第二轮只针对薄弱点加配额，不整体重做。

## Update Mode

当用户要求更新已有 Skill 时：

1. 先读取现有 `SKILL.md`
2. 确认上次调研截止时间
3. 重点刷新以下部分：
   - 最新对话 / 访谈
   - 最新决策与行为
   - 最新时间线
4. 判断新信息是：
   - 强化旧模型
   - 修正旧模型
   - 形成新模型
5. 只增量更新相关 section，不重写无关部分

## Failure Handling

如果某个子任务失败：

- 不阻塞整体流程
- 立即将该维度标记为“信息不足”
- 继续推进其余维度
- 在最终 Skill 的诚实边界中显式写出缺口

## Delivery Checklist

交付前确认：

- 研究文件已全部落盘
- 交叉验证已完成
- 至少完成一轮质量验证
- 最终 `SKILL.md` 不是草稿
- 局限、冲突、时效边界写清楚
