<div align="center">

# 蒸馏.SKILL

> *面向人物、主题与模糊需求的通用 Skill Builder*

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Skill-blueviolet)](https://claude.ai/code)
[![Skills](https://img.shields.io/badge/skills.sh-Compatible-green)](https://skills.sh)

<br>

**它不是模仿口气的提示词集合，而是一条可执行的 Skill 生产线。**

- 先定义目标
- 再并行调研
- 再交叉验证
- 再提炼认知框架
- 最后构建并验证最终 SKILL.md

**核心目标：提炼对象的认知操作系统，而不是复读原话。**

<br>

[安装](#安装) · [适用场景](#适用场景) · [工作原理](#工作原理) · [如何使用](#如何使用) · [目录结构](#目录结构)

</div>

---

## 效果示例

**用户输入**：蒸馏一个乔布斯风格的 Skill

**系统响应**：

```
Phase 0 — 归一化需求
  ✓ 输入类型：persona
  ✓ 目标对象：史蒂夫·乔布斯
  ✓ 聚焦维度：产品哲学、决策模式、表达风格

Phase 1 — 六路并行调研
  ✓ Agent 1 — Writings：分析斯坦福演讲、公开信、产品发布会
  ✓ Agent 2 — Conversations：访谈记录、内部会议纪要
  ✓ Agent 3 — Expression DNA：简洁有力、反问句、insanely great
  ✓ Agent 4 — External Views：传记、同行评价、批评者视角
  ✓ Agent 5 — Decisions：砍掉项目、专注策略、端到端控制
  ✓ Agent 6 — Timeline：NeXT → Apple → Pixar 三个阶段

Phase 1.5 — 交叉验证
  ✓ 时间线一致性：通过
  ✓ 冲突点：记录并标注
  ✓ 来源可信度：加权调整完成

Phase 2 — 提炼认知框架
  ✓ 心智模型：聚焦即说不、端到端控制、品味至上
  ✓ 决策启发式：如果不够 great 就不做、做减法不做加法
  ✓ 表达 DNA：短句、重复、否定对比
  ✓ 价值观：完美主义、反妥协、用户至上
  ✓ 智识谱系：受禅宗、包豪斯、斯金纳影响
  ✓ 诚实边界：无法捕捉直觉和灵感

Phase 3 — 构建最终 SKILL.md
  ✓ 生成 Skill 定义

Phase 4 — 验证
  ✓ 已知问题测试：通过
  ✓ 边缘问题推断：通过
  ✓ 风格辨识度：通过

Phase 5 — 交付
  ✓ SKILL.md
  ✓ references/research/*（7个调研文件）
  ✓ validation/validation-report.md
  ✓ 交付摘要
```

**最终效果**：

```
用户      ❯ 我们这个产品功能太少了，竞争对手都有20+功能

乔布斯    ❯ 你在数功能。我在数用户会真正用的功能。

            20个功能，用户只会用3个。其他17个是噪音。
            噪音让用户困惑，困惑让用户离开。

            Focus means saying no to a hundred good ideas.
            做减法，不做加法。

            把那3个功能做到 insanely great。
```

---

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

---

## 工作原理

### Phase 0 — 归一化需求

先判断输入类型：`persona` / `topic` / `hybrid` / `fuzzy` / `update`

并补齐：目标对象、聚焦维度、目标用途、安全边界、产出模式。

### Phase 0.5 — 模板化脚手架

直接使用 `templates/target-skill/` 初始化目标 Skill：

1. 确定 `target-slug`
2. 复制模板目录到 `.codebuddy/skills/<target-slug>/`
3. 渲染 `{{subject}}` 与 `{{slug}}`
4. 生成 `validation/validation-report.md`

### Phase 1 — 六路并行调研

默认并行启动以下六个 Agent：

| Agent | 职责 |
|-------|------|
| Agent 1 — Writings | 著作、公开信、演讲全文 |
| Agent 2 — Conversations | 访谈、对话记录、内部会议 |
| Agent 3 — Expression DNA | 表达风格、语气、用词偏好 |
| Agent 4 — External Views | 传记、同行评价、批评者视角 |
| Agent 5 — Decisions | 决策记录、关键选择 |
| Agent 6 — Timeline | 人生时间线、关键事件 |

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

---

## 这版的特点

- `6` 个并行调研 Agent
- `1` 个交叉验证 Agent
- 中间产物全部落盘
- 模板驱动，不依赖 Python 初始化脚本
- 规则驱动，不依赖外部校验脚本
- 支持新建与增量更新

---

## 核心原则

1. 长文优先于碎片
2. 一手优先于二手，二手优先于推断
3. 行为优先于表态
4. 冲突必须保留
5. 信息不足必须明确写出
6. 所有中间产物必须写入目标 Skill 目录
7. 重点是认知框架，不是 cosplay
8. 可验证优先于"像"
9. 宁可少，不可滥

## 工作流

完整流程参考上方的[工作原理](#工作原理)章节。

## 目录结构

```
.
├── SKILL.md                         # 主 Skill 定义
├── README.md
├── references/
│   ├── agent-prompts.md             # 6+1 Agent 标准提示模板
│   ├── orchestration.md             # 编排规则、目录协议
│   ├── output-contracts.md          # 研究文件格式、来源评分
│   ├── validation-contract.md       # 纯模块化校验规则
│   └── validation-report-template.md # 验证报告模板
└── templates/
    └── target-skill/                # 目标 Skill 脚手架
        ├── SKILL.md.tpl
        ├── references/
        │   ├── research/            # 7个调研文件模板
        │   └── sources/
        └── validation/
            └── validation-report.md.tpl
```

---

## 关键资源说明

| 文件 | 说明 |
|------|------|
| `SKILL.md` | 主 Skill 定义与完整运行流程 |
| `references/orchestration.md` | 编排规则、目录协议、失败兜底、更新模式 |
| `references/agent-prompts.md` | 6+1 Agent 标准提示模板 |
| `references/output-contracts.md` | 研究文件格式、来源评分、覆盖度门槛 |
| `references/validation-contract.md` | 纯模块化校验规则 |
| `references/validation-report-template.md` | 验证报告模板 |
| `templates/target-skill/` | 目标 Skill 脚手架模板 |

---

## 安装

```bash
npx skills add yangbuyiya/distill-any-skill
```

然后在任意 IDE 里使用，如 Claude Code：

```
> 蒸馏一个乔布斯
> 做一个张雪峰的 Skill
> 帮我蒸馏芒格的思维方式
```

蒸馏完成后直接调用：

```
> 用乔布斯的视角分析这个产品
> 张雪峰会怎么建议这个专业选择？
> 切换到芒格，帮我分析这个投资决策
```

---

## 如何使用

### 方式一：作为 Skill 直接使用

当用户要求"蒸馏某个人物/主题为 Skill"时，触发本 Skill，按 `SKILL.md` 的分阶段流程执行。

### 方式二：手动按模板运行

1. 从 `templates/target-skill/` 复制一份目标模板目录
2. 替换 `{{subject}}`、`{{slug}}`
3. 按 `references/agent-prompts.md` 并行执行 `6` 个研究 Agent
4. 运行 `Agent 7` 做交叉验证
5. 按 `references/output-contracts.md` 提炼最终 Skill
6. 按 `references/validation-contract.md` 生成 `validation/validation-report.md`
7. 验证结论为 `Pass` 后再交付

---

## 输出协议

每个 `references/research/*.md` 文件都必须包含：

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

---

## 验证机制

纯模块化验证：

- 不依赖 `coverage_report.py`
- 不依赖外部脚本
- 主任务必须依据 `references/validation-contract.md` 完成检查
- 检查结果必须写入目标 Skill 的 `validation/validation-report.md`

最终验证结论只有三种：

- `Pass`
- `Needs round two`
- `Needs rewrite`

---

## 信息源策略

**默认优先级：**

1. 本人著作、公开信、演讲全文、原始访谈、原始播客
2. 权威媒体深访、授权传记、长期跟踪报道
3. 高质量评论、书评、外部分析
4. 碎片内容、二次摘录

**默认黑名单：**

- 知乎
- 微信公众号
- 百度百科
- 百度知道

---

## MVP 范围

**已覆盖：**

- 目标 Skill 模板化初始化
- `6+1` Agent 并行研究框架
- 研究文件落盘
- 交叉验证
- 提炼与最终 `SKILL.md` 构建
- 模块化验证与验证报告输出

**暂未自动化但可扩展：**

- 自动二轮任务调度
- 视频 / 播客自动转录
- 关系网络可视化
- 自动打包发布
- 更细粒度增量更新策略

---

## 仓库定位

这是一个：

- 可复用的 `meta-skill`
- 人物 / 主题 Skill 生产线
- 研究、提炼、构建、验证的一体化标准

不是一个：

- 单轮回答器
- 低质量角色扮演器

---

<div align="center">

**MIT License** — 随便用，随便改，随便造。

</div>
