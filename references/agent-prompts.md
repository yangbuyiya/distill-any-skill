# 6 + 1 Agent 标准提示模板

## Shared Preamble

以下前置约束适用于所有 Agent：

- 只负责当前维度，不做最终 Skill 合成
- 输出必须写入指定文件；若子任务环境只读，则将完整结果返回给主任务，由主任务立即落盘
- 每条重要信息标注来源名或 URL
- 每条重要信息标注：`一手 / 二手 / 推断`
- 每个来源提供质量评分：权威性 / 一手性 / 完整性 / 时效性 / 综合
- 遇到冲突时保留冲突，不擅自统一
- 若信息不足，明确写 `信息不足` 与 `Gaps`
- 优先长文、完整访谈、原始材料；避免低质量碎片来源

共享输入参数：

- `subject`
- `subject_type`
- `focus`
- `goal`
- `output_file`
- `source_policy`
- `existing_skill_context`

统一输出结构：参考 `references/output-contracts.md`

---

## Agent 1 — Writings

```text
调研对象: {subject}
对象类型: {subject_type}
聚焦维度: {focus}
目标用途: {goal}
输出文件: {output_file}

任务：只研究“著作与系统性长文”。

必须完成：
1. 找出书籍、长文、公开信、newsletter、系统性论述
2. 提取核心主张、自创术语、重复出现 >=3 次的观点
3. 标注推荐书单 / 智识来源
4. 按统一结构写入结果

不要做：
- 长对话分析
- 表达风格分析
- 最终人物 / 主题画像合成
```

## Agent 2 — Conversations

```text
调研对象: {subject}
对象类型: {subject_type}
聚焦维度: {focus}
目标用途: {goal}
输出文件: {output_file}

任务：只研究“长对话与深度访谈”。

必须完成：
1. 找出播客、AMA、深度访谈、长视频对话
2. 提取被追问时的回答方式、问题重构方式、即兴类比
3. 标记回避 / 犹豫 / 改口问题
4. 标记立场变化时刻
5. 按统一结构写入结果
```

## Agent 3 — Expression DNA

```text
调研对象: {subject}
对象类型: {subject_type}
聚焦维度: {focus}
目标用途: {goal}
输出文件: {output_file}

任务：只研究“表达 DNA”。

必须完成：
1. 收集表达样本
2. 提取高频词、常见句式、节奏、比喻方式、幽默方式
3. 标记确定性强弱、禁忌词、口癖
4. 按统一结构写入结果
```

## Agent 4 — External Views

```text
调研对象: {subject}
对象类型: {subject_type}
聚焦维度: {focus}
目标用途: {goal}
输出文件: {output_file}

任务：只研究“外部评价与批评”。

必须完成：
1. 找出传记、评论、批评、同行评价、书评
2. 提取外部观察到的稳定特征
3. 提取常见批评、争议事件、与同行差异
4. 按统一结构写入结果
```

## Agent 5 — Decisions

```text
调研对象: {subject}
对象类型: {subject_type}
聚焦维度: {focus}
目标用途: {goal}
输出文件: {output_file}

任务：只研究“重大决策与行为记录”。

必须完成：
1. 找出关键决策、重大行为、战略取舍、失败案例
2. 写清决策背景、逻辑、结果、事后反思
3. 标记言行一致与不一致案例
4. 按统一结构写入结果
```

## Agent 6 — Timeline

```text
调研对象: {subject}
对象类型: {subject_type}
聚焦维度: {focus}
目标用途: {goal}
输出文件: {output_file}

任务：只研究“完整时间线”。

必须完成：
1. 建立从早期到近期的时间线
2. 标记重要节点与思想转折点
3. 覆盖近 12 个月动态
4. 标记重要合作、身份变化、作品变化
5. 按统一结构写入结果
```

## Agent 7 — Cross Validation

```text
调研对象: {subject}
对象类型: {subject_type}
聚焦维度: {focus}
目标用途: {goal}
输出文件: {output_file}
输入文件:
- references/research/01-writings.md
- references/research/02-conversations.md
- references/research/03-expression-dna.md
- references/research/04-external-views.md
- references/research/05-decisions.md
- references/research/06-timeline.md

任务：只做交叉验证与关系网络。

必须完成：
1. 检查时间线一致性
2. 标记不同来源对同一事件的差异
3. 提炼需要澄清的冲突点
4. 产出关键人物 / 组织 / 作品关系网络
5. 对前六个维度给出可信度调整建议
6. 给出是否需要第二轮补强的建议
7. 按统一结构写入结果

不要做：
- 最终 Skill 构建
- 心智模型提炼
- 风格化输出
```

## 主任务汇总模板

主任务在 Agent 7 完成后，先生成一份调研质量摘要，再决定是否进入二轮补强或提炼阶段。摘要至少包含：

- 每个 Agent 的来源数量
- 每个 Agent 的关键发现
- 明显冲突点
- 信息不足维度
- 一手来源占比粗估
- 质量热力图或简版评分判断
