# distill-any-skill

一个面向人物、主题与模糊需求的通用 `Skill Builder`。

它不是一个“模仿口气”的提示词集合，而是一条可执行的 Skill 生产线：

- 先定义目标
- 再并行调研
- 再交叉验证
- 再提炼认知框架
- 最后构建并验证最终 `SKILL.md`

核心目标是提炼对象的 **认知操作系统**，而不是复读原话。

## 适用场景

适用于：

- 蒸馏某个具体人物为 Skill
- 蒸馏某个主题、框架、流派或方法论为 Skill
- 面对模糊需求，先推荐适配对象再蒸馏
- 更新已有 Skill，补充最新动态、决策和时间线

不适用于：

- 普通闲聊问答
- 只想做语气模仿
- 无依据编造观点或立场
- 跳过调研直接交付成品

## 这版的特点

- `6` 个并行调研 Agent
- `1` 个交叉验证 Agent
- 中间产物全部落盘
- 模板驱动，不依赖 Python 初始化脚本
- 规则驱动，不依赖外部校验脚本
- 支持新建与增量更新

## 核心原则

1. 长文优先于碎片
2. 一手优先于二手，二手优先于推断
3. 行为优先于表态
4. 冲突必须保留
5. 信息不足必须明确写出
6. 所有中间产物必须写入目标 Skill 目录
7. 重点是认知框架，不是 cosplay
8. 可验证优先于“像”
9. 宁可少，不可滥

## 工作流

### Phase 0 — 归一化需求
先判断输入类型：

- `persona`
- `topic`
- `hybrid`
- `fuzzy`
- `update`

并补齐：目标对象、聚焦维度、目标用途、安全边界、产出模式。

### Phase 0.5 — 模板化脚手架
直接使用 `templates/target-skill/` 初始化目标 Skill：

1. 确定 `target-slug`
2. 复制模板目录到 `.codebuddy/skills/<target-slug>/`
3. 渲染 `{{subject}}` 与 `{{slug}}`
4. 生成 `validation/validation-report.md`
5. 如果目标已存在，则按增量更新模式处理

### Phase 1 — 六路并行调研
默认并行启动以下六个 Agent：

1. `Agent 1 — Writings`
2. `Agent 2 — Conversations`
3. `Agent 3 — Expression DNA`
4. `Agent 4 — External Views`
5. `Agent 5 — Decisions`
6. `Agent 6 — Timeline`

### Phase 1.5 — 交叉验证
启动 `Agent 7 — Cross Validation`，检查：

- 时间线一致性
- 同一事件在不同来源中的差异
- 冲突点
- 关系网络
- 可信度调整
- 是否需要第二轮补强

### Phase 1.6 — 第二轮补强
以下情况触发补强：

- 某维度来源数量不足
- 一手来源占比过低
- 关键时间点覆盖不足
- 冲突未解释
- 最近 `12` 个月动态缺失
- 来源类型过于单一

### Phase 2 — 提炼
从研究文件中提炼：

- `3-7` 个心智模型
- `5-10` 条决策启发式
- 表达 DNA
- 价值观与反模式
- 智识谱系
- 诚实边界

### Phase 3 — 构建最终 Skill
生成目标对象的最终 `SKILL.md`。

### Phase 4 — 验证
验证至少包括：

1. 已知问题一致性测试
2. 边缘问题推断测试
3. 风格辨识度测试

### Phase 5 — 交付
交付时至少包含：

- 最终 `SKILL.md`
- 全部 `references/research/*`
- `validation/validation-report.md`
- 简短交付摘要
- 局限与调研截止时间

## 目录结构

```text
.
├── SKILL.md
├── README.md
├── references/
│   ├── agent-prompts.md
│   ├── mvp-breakdown.md
│   ├── orchestration.md
│   ├── output-contracts.md
│   ├── validation-contract.md
│   └── validation-report-template.md
└── templates/
    └── target-skill/
        ├── SKILL.md.tpl
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
        └── validation/
            └── validation-report.md.tpl
```

## 关键资源说明

- `SKILL.md`：主 Skill 定义与完整运行流程
- `references/orchestration.md`：编排规则、目录协议、失败兜底、更新模式
- `references/agent-prompts.md`：`6+1` Agent 标准提示模板
- `references/output-contracts.md`：研究文件格式、来源评分、覆盖度门槛
- `references/validation-contract.md`：纯模块化校验规则
- `references/validation-report-template.md`：验证报告模板
- `references/mvp-breakdown.md`：MVP 开发任务拆解
- `templates/target-skill/`：目标 Skill 脚手架模板

## 如何使用

### 方式一：作为 Skill 直接使用
当用户要求“蒸馏某个人物/主题为 Skill”时，触发本 Skill，按 `SKILL.md` 的分阶段流程执行。

### 方式二：手动按模板运行
1. 从 `templates/target-skill/` 复制一份目标模板目录
2. 替换 `{{subject}}`、`{{slug}}`
3. 按 `references/agent-prompts.md` 并行执行 `6` 个研究 Agent
4. 运行 `Agent 7` 做交叉验证
5. 按 `references/output-contracts.md` 提炼最终 Skill
6. 按 `references/validation-contract.md` 生成 `validation/validation-report.md`
7. 验证结论为 `Pass` 后再交付

## 输出协议

每个 `references/research/*.md` 文件都必须包含统一结构：

- `## Summary`
- `## Key Findings`
- `## Evidence`
- `## Sources`
- `## Contradictions`
- `## Gaps`
- `## Confidence`

每条重要信息都要标注：

- 来源名或 URL
- `一手 / 二手 / 推断`
- 质量评分：权威性 / 一手性 / 完整性 / 时效性 / 综合

## 验证机制

本仓库已经改为纯模块化验证：

- 不依赖 `coverage_report.py`
- 不依赖外部脚本
- 主任务必须依据 `references/validation-contract.md` 完成检查
- 检查结果必须写入目标 Skill 的 `validation/validation-report.md`

允许的最终验证结论只有三种：

- `Pass`
- `Needs round two`
- `Needs rewrite`

## 信息源策略

默认优先级：

1. 本人著作、公开信、演讲全文、原始访谈、原始播客
2. 权威媒体深访、授权传记、长期跟踪报道
3. 高质量评论、书评、外部分析
4. 碎片内容、二次摘录

默认黑名单：

- 知乎
- 微信公众号
- 百度百科
- 百度知道

## MVP 范围

当前 MVP 已覆盖：

- 目标 Skill 模板化初始化
- `6+1` Agent 并行研究框架
- 研究文件落盘
- 交叉验证
- 提炼与最终 `SKILL.md` 构建
- 模块化验证与验证报告输出

暂未自动化但可扩展：

- 自动二轮任务调度
- 视频 / 播客自动转录
- 关系网络可视化
- 自动打包发布
- 更细粒度增量更新策略

## 仓库定位

这个仓库更适合作为：

- 可复用的 `meta-skill`
- 人物 / 主题 Skill 生产线
- 研究、提炼、构建、验证的一体化标准

而不是一个单轮回答器或低质量角色扮演器。
