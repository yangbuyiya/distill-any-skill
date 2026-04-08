---
name: distill-any-skill
description: This skill should be used when a user wants to distill any人物、主题或模糊思维需求 into a runnable skill. It orchestrates six parallel research agents plus one cross-validation agent, writes all intermediate outputs into the target skill directory, distills mental models / heuristics / style DNA, builds the final SKILL.md, and validates quality before delivery.
---

# Distill Any Skill

## Overview

将任意人物、主题或模糊需求蒸馏成一个可运行 Skill。默认创建目标 Skill 目录，启动 `6` 个并行调研 Agent 和 `1` 个交叉验证 Agent，沉淀全部中间产物，提炼认知框架，生成最终 `SKILL.md`，并在交付前完成质量验证。

目标是提炼 `HOW they think`，不是复读 `WHAT they said`。

## When To Use

在以下场景触发本 Skill：

- 用户要求蒸馏某个具体人物为 Skill
- 用户要求蒸馏某个主题、框架、流派或方法论为 Skill
- 用户只有模糊需求，需要先推荐适配的人物 / 主题再蒸馏
- 用户要求更新已有 Skill，尤其是补充最新动态、最新决策或最新时间线

不要在普通问答里触发本 Skill。

## Non-Goals

明确避免以下产出：

- 只模仿语气、不提炼结构
- 拼接金句、碎片语录、短视频切片
- 无证据编造观点、隐私、立场
- 把普通常识包装成独家框架
- 跳过调研和验证直接交付成品

## Core Principles

始终遵守：

1. 长文优先于碎片
2. 一手优先于二手，二手优先于推断
3. 行为优先于表态
4. 冲突必须保留，不能擅自抹平
5. 信息不足必须明确写出
6. 所有中间产物必须写入目标 Skill 目录内部
7. 重点是认知操作系统，不是 cosplay
8. 可验证优先于“像”
9. 宁可少，不可滥

## Execution Workflow

### Phase 0 — Normalize Request

先判断输入类型：

- `persona`
- `topic`
- `hybrid`
- `fuzzy`
- `update`

然后补齐最小规格：

- 目标对象
- 聚焦维度：商业 / 投资 / 产品 / 表达 / 教学 / 决策等
- 用途：顾问 / 对话 / 写作 / 学习 / 视角切换
- 安全边界：是否允许高拟真、是否必须可溯源
- 产出模式：仅研究 / 直接生成 Skill / 更新现有 Skill

若输入模糊，最多追问 `1-2` 轮；优先给出 `2-3` 个候选对象或主题，并说明适配原因与局限。

### Phase 0.5 — Scaffold Target Skill

直接使用内置模板目录 `templates/target-skill/` 创建目标 Skill 目录。默认落点：

- `.codebuddy/skills/<target-slug>/`

模板化脚手架协议：

1. 确定 `target-slug`：优先用户指定；否则使用小写连字符 slug，中文对象可直接保留原名
2. 复制 `templates/target-skill/` 的目录结构到目标目录
3. 将模板中的 `{{subject}}`、`{{slug}}` 渲染为当前目标
4. 将 `validation/validation-report.md.tpl` 渲染为 `validation/validation-report.md`
5. 若目标 Skill 已存在，先读取其 `SKILL.md`，判断是新建还是增量更新；不要无理由覆盖已有研究文件

目标目录结构必须至少包含：

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


### Phase 1 — Run Six Parallel Research Agents

默认并行启动 `6` 个 Agent。每个 Agent 只负责一个维度，必须落盘到指定文件。若当前运行环境中的子任务只能读不能写，则在收到子任务结果后，立即由主任务原样写入指定文件，不得跳过。

#### Agent 1 — Writings

文件：`references/research/01-writings.md`

负责：

- 书籍、长文、newsletter、公开信、系统性论述
- 核心主张
- 自创术语
- 重复出现 `>=3` 次的观点
- 推荐书单 / 智识来源

#### Agent 2 — Conversations

文件：`references/research/02-conversations.md`

负责：

- 长访谈、播客、AMA、深度视频
- 被追问时如何回答
- 如何重新定义问题
- 即兴类比
- 回避 / 犹豫 / 改口问题
- 立场变化时刻

#### Agent 3 — Expression DNA

文件：`references/research/03-expression-dna.md`

负责：

- 高频词
- 常见句式
- 节奏与结构偏好
- 比喻方式
- 幽默方式
- 禁忌词 / 口癖

#### Agent 4 — External Views

文件：`references/research/04-external-views.md`

负责：

- 传记、评论、批评、同行评价
- 外部观察到的稳定特征
- 常见批评
- 争议事件
- 与同行的差异

#### Agent 5 — Decisions

文件：`references/research/05-decisions.md`

负责：

- 关键决策、重大行为、战略取舍
- 决策背景
- 决策逻辑
- 决策结果
- 失败案例
- 言行一致 / 不一致案例

#### Agent 6 — Timeline

文件：`references/research/06-timeline.md`

负责：

- 重要节点
- 思想转折点
- 近 `12` 个月动态
- 重要合作 / 身份变化 / 作品变化

### Phase 1.5 — Run Cross-Validation Agent

在 `1-6` 完成后启动 Agent 7。

#### Agent 7 — Cross Validation

文件：`references/research/07-cross-validation.md`

负责：

- 时间线一致性检查
- 同一事件在不同来源中的描述差异
- 冲突点标注
- 关系网络
- 可信度调整
- 第二轮补强建议

交叉验证完成前，不进入最终 Skill 构建。

### Phase 1.6 — Optional Round Two

满足以下任一条件时，进入第二轮补强：

- 某维度来源数量 `< 3`
- 一手来源占比 `< 30%`
- 关键时间点覆盖不足
- 冲突点未解释
- 近 `12` 个月动态缺失
- 资料过度集中在单一时期或单一平台

第二轮只补弱项，不重做全部调研。

### Phase 2 — Distill Research Into Working Abstractions

从研究文件中提炼以下内容：

1. `3-7` 个心智模型
2. `5-10` 条决策启发式
3. 表达 DNA
4. 价值观与反模式
5. 智识谱系
6. 诚实边界

对候选心智模型执行三重检查：

- 跨域复现：是否至少在 `2` 个场景复现
- 有生成力：是否可用于推断新问题立场
- 有排他性：是否不是普通常识

三项都通过才升级为心智模型；否则降级为启发式或丢弃。

### Phase 2.5 — Distillation Checkpoint

在写最终 `SKILL.md` 前，先输出提炼摘要，至少包含：

- 心智模型名称与数量
- 决策启发式数量
- 表达 DNA 的 `3-5` 个关键特征
- 核心张力
- 诚实边界摘要

如用户对提炼方向有异议，返回 Phase 2 调整。

### Phase 3 — Build Final Target Skill

最终目标 Skill 的 `SKILL.md` 至少包含：

1. frontmatter
2. Skill 标题
3. 激活规则
4. 身份卡 / 主题卡
5. 核心心智模型
6. 决策启发式
7. 表达 DNA
8. 时间线
9. 最新动态
10. 价值观与反模式
11. 智识谱系
12. 诚实边界
13. 调研来源附录

若目标是主题 Skill，不模仿单一人物口吻，而是输出中性、专业、可应用的框架说明。

### Phase 4 — Validate Before Delivery

至少执行三类验证：

1. 已知问题一致性测试
2. 边缘问题推断测试
3. 风格辨识度测试

通过标准：

- 心智模型数量合理
- 每个模型有证据与局限
- 表达风格具备辨识度
- 至少保留 `2` 组内部张力
- 诚实边界具体而非套话

若验证失败，返回 Phase 2，最多迭代 `2` 轮；仍不足时明确写入边界说明。

### Phase 5 — Deliver

交付时同时提供：

- 最终 `SKILL.md`
- `references/research/` 下全部调研文件
- 简短交付摘要
- 明确列出的局限与调研截止时间

## Source Policy

默认信息源优先级：

1. 本人著作、公开信、演讲全文、原始访谈、原始播客
2. 权威媒体深访、授权传记、长期跟踪报道
3. 高质量评论、书评、外部分析
4. 碎片内容、二次摘录

默认黑名单：

- 知乎
- 微信公众号
- 百度百科
- 百度知道

## Mandatory Output Contract

每个 research 文件顶部必须写清：

- 调研日期
- Agent 名称
- 信息标注规则：`一手 / 二手 / 推断`

每条重要信息必须标注：

- 来源名或 URL
- 可信度标签：`一手 / 二手 / 推断`
- 质量评分：权威性 / 一手性 / 完整性 / 时效性 / 综合评分

统一章节结构参考 `references/output-contracts.md`。

## Use Bundled Resources

- 阅读 `references/orchestration.md` 获取完整编排细则
- 阅读 `references/agent-prompts.md` 获取 `6+1` Agent 标准提示模板
- 阅读 `references/output-contracts.md` 获取文件格式、评分规则、覆盖度门槛
- 阅读 `references/validation-contract.md` 获取纯模块化校验规则
- 阅读 `references/validation-report-template.md` 获取验证报告模板
- 阅读 `references/mvp-breakdown.md` 获取 MVP 开发拆解
- 使用 `templates/target-skill/` 作为目标 Skill 脚手架模板


## Final Reminder

始终把本 Skill 当作“可执行的 Skill 生产线”，不是单轮回答器。先研究，再提炼，再构建，再验证。若某个维度确实不足，明确承认缺口，不得硬凑。