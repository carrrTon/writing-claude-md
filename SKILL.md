---
name: writing-claude-md
description: Use when creating, reviewing, trimming, rewriting, or improving CLAUDE.md or CLAUDE.local.md files, especially when deciding what belongs in persistent project instructions versus skills, hooks, README docs, or one-off prompts.
---

# 编写 CLAUDE.md

## 核心原则

CLAUDE.md 会在每个相关的 Claude Code 会话中被加载，所以每一行都要值得占用上下文。只写入那些**持久适用、范围足够广、Claude 无法可靠地从代码中推断、并且会改变 Claude 行为**的指令。

判断每一条候选内容时，先问：**如果删掉这一行，Claude 是否很可能犯代价较高的错误？** 如果答案是否定的，就删除它，或移动到更合适的位置。

## 适合写入 CLAUDE.md 的内容

| 适合写入 | 原因 |
|---|---|
| 非显而易见的构建、测试、lint 或验证命令 | Claude 不一定能推断正确命令或执行范围 |
| 项目特有的工作流规则 | 会影响每次会话，并避免重复犯错 |
| 与默认习惯不同的代码风格规则 | 泛泛的风格建议会浪费上下文 |
| 仓库协作礼仪、分支、提交或 PR 约定 | 这是项目/团队约束，不是代码事实 |
| 开发环境特殊要求或必需设置 | 缺失会导致可避免的失败 |
| 常见陷阱或反直觉行为 | 这是高杠杆的持久上下文 |
| 代码中不明显的重要架构决策 | 帮助 Claude 避免破坏有意设计的约束 |

## 不适合写入 CLAUDE.md 的内容

| 应移出或删除 | 更合适的位置 |
|---|---|
| 很长的可复用工作流 | Skill |
| 每次都必须执行的确定性检查 | Hook 或脚本 |
| 详细 API 文档或教程 | README、docs 或引用链接 |
| 按文件逐项描述项目结构 | 让 Claude 在需要时读取代码 |
| 经常变化的状态、TODO 或计划 | issue、计划文档或当前 prompt |
| “写干净代码”这类通用建议 | 删除 |
| 偶尔才相关的领域知识 | Skill |
| 只对个人生效的项目笔记 | CLAUDE.local.md |

## 评审流程

1. 阅读目标 CLAUDE.md，先判断它真正想约束什么行为。
2. 在删减前提取用户的持久意图；压缩文字不能抹掉用户真正关心的行为。
3. 将每个部分归类为：
   - 保留在 CLAUDE.md；
   - 移到 skill；
   - 移到 hook 或脚本；
   - 移到 README 或 docs；
   - 移到 CLAUDE.local.md；
   - 删除。
4. 对重要约束，先尝试缩短表述，再决定是否删除。
5. 保留那些编码了用户意图、项目协作礼仪或非显而易见失败预防的指令。
6. 除非用户明确要求覆盖原文件，否则生成一个新的对比文件。

## 质量评估维度

| 维度 | 好的表现 | 警示信号 |
|---|---|---|
| 简洁性 | 规则短小、可扫读 | 长解释、重复措辞 |
| 具体性 | 命令、路径、行为明确 | 模糊建议或通用最佳实践 |
| 持久性 | 跨会话仍然成立 | 状态更新或临时计划 |
| 可执行性 | Claude 能直接照做 | 只有愿景式口号 |
| 放置位置 | 总是相关的规则留在这里 | 偶尔相关的流程挤占上下文 |
| 可验证性 | 需要时说明如何检查成功 | Claude 没有反馈闭环 |

## 推荐改写结构

除非项目有更合适的结构，优先使用：

```markdown
# Project Instructions

## Communication
- [适用于本项目的语言、语气或协作偏好]

## Project workflow
- [Claude 在每次会话中都应遵守的持久工作流规则]

## Verification
- [推荐的测试、lint、构建命令，以及何时运行]

## Project-specific constraints
- [非显而易见的架构、环境或安全约束]

## Related workflows
- [指向较长或偶尔才需要的 skills / docs]
```

只保留真正有内容的章节。空模板章节本身就是噪音。

## 常见错误

| 错误 | 修正 |
|---|---|
| 把 CLAUDE.md 写成项目手册 | 只保留持久规则；手册移到 docs 或 skill |
| 把长步骤工作流塞进 CLAUDE.md | 创建 skill，并在 CLAUDE.md 中简短引用 |
| 依赖 CLAUDE.md 强制执行自动化 | 用 hook 或脚本做确定性 enforcement |
| 罗列显而易见的代码结构 | 让 Claude 需要时自己读文件 |
| 保留过期状态 | 删除，或移动到当前任务跟踪系统 |
| 为了显得通用而写得很虚 | 写具体命令、路径和约束 |

## 评审或改写时的输出格式

评审或改写 CLAUDE.md 时，返回：

1. **结论**：好 / 可用但建议修改 / 过度膨胀 / 缺少关键上下文。
2. **应保留内容**：现有文件中高价值的指令。
3. **应移动或删除内容**：用表格说明目标位置和原因。
4. **建议改写版**：内联展示，或保存为新文件。
5. **后续建议**：是否值得创建 skill、hook 或补充 docs。
