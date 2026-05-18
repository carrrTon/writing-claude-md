# writing-claude-md

一个简单的优化`CLAUDE.md`skill

## 为什么需要它

`CLAUDE.md` 会在每个相关的 Claude Code 会话中被加载。这个 skill 帮助判断哪些内容值得占用持久上下文，哪些应该移动到别处，哪些应该直接删除。
膨胀的 CLAUDE.md 文件会导致 Claude 忽略你的实际指令

## 核心理念

如果删掉某一行并不会显著增加 Claude 犯高成本错误的概率，那它很可能不属于 `CLAUDE.md`。

## 它能做什么

- 评审膨胀的 `CLAUDE.md`，区分持久指令、临时状态和可从代码推断的信息
- 将项目说明改写成更短、更高信噪比的结构
- 判断内容更适合放在 skill、hook、README、docs 还是 `CLAUDE.local.md`

## 规则来源

- Best practices for Claude Code 
https://code.claude.com/docs/en/best-practices



