# Blind Parallel Brainstorm

[English](README.md)

一个通过文件级隔离维持构思独立性的 Agent Skill。它用于生成彼此失明的编号构思、逐个验证指定编号，并将通过初筛的大方向继续发展为 `001-01`、`001-02` 等受控分支。

## 为什么需要它

普通多轮头脑风暴很容易向最早出现的几个方案收敛：后续 Agent 读取了已有正文、术语和论证后，会不自觉地模仿、组合或围绕它们微调。

本 Skill 通过严格的上下文边界降低这种锚定：

- 创建根构思时，只读取公共题目与仅含标题的根索引；
- 验证时，只读取被点名的一个编号及其自身历史验证；
- 创建子构思时，只继承经验证生成的 `branch brief`，不读取父节点原始正文；
- 兄弟节点彼此只看到标题，不看到具体内容；
- 用户明确批准前，所有构思都隔离在主项目之外。

隔离可以提高独立性，但不能自动证明想法新颖或正确。

## 核心操作

工作区完成一次性初始化后，每次运行只执行一种主要操作：

```text
CREATE ROOT
VERIFY 001
CREATE CHILD 001
```

- `CREATE ROOT`：创建一个新的独立根方向；
- `VERIFY 001`：只验证编号 001；
- `CREATE CHILD 001`：只基于 001 的受控分支摘要创建一个子方向。

一次创建只写一个构思文件，一次验证只检查一个编号。Skill 不会后台继续生长，也不会因为普通检索发现不确定性就擅自启动发散。

## 演化方式

```text
001 根构思
  -> VERIFY 001
  -> 生成受控 branch brief
  -> 创建 001-01 / 001-02
  -> 子节点分别验证
  -> 仅在仍有信息增量时继续向下分叉
```

系统先形成彼此隔离的“构思森林”。跨分支比较与综合只有在用户明确点名已验证节点后才允许进行。

## 仓库结构

```text
SKILL.md
references/
  workspace-and-isolation.md
  create-root.md
  verify-idea.md
  create-child.md
  lifecycle-and-governance.md
templates/brainstorm/
  AGENTS.md
  BRIEF.md
  ROOT_INDEX.md
  idea.md
  review.md
  branch-brief.md
  child-index.md
  reservation.md
```

根 `SKILL.md` 采用按需读取：当前执行什么操作，就只读取对应的一份手册，避免把全部规则和历史内容同时塞入上下文。

## 关键边界

- 禁止递归读取整个 `brainstorm/`；
- 创建或验证时禁止读取兄弟节点正文；
- 原始构思创建后不可修改，验证记录只能追加；
- 逻辑自洽、语言自信和听起来新颖都不等于证据；
- `survives` 仅表示当前值得保留，不表示已证实；
- 未经用户点名批准，构思不得进入主项目；
- 常规检索、总结和事实核查不会自动触发本 Skill。

## 示例指令

```text
使用 blind-parallel-brainstorm 初始化这个项目，并创建一个独立根构思。
```

```text
验证 brainstorm 中的 003，不要读取其他构思正文。
```

```text
只使用 003 的 branch brief，创建一个新的子方向。
```

## 当前状态

这是第一版可运行规范。当前设计有意偏保守：优先保证隔离、可审计和防止上下文污染，而不是追求最大程度自动化。

## 许可证

MIT
