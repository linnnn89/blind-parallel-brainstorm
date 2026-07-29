# Blind Parallel Brainstorm

[English](README.md)

一个通过文件级隔离维持构思独立性的 Agent Skill。它用于生成彼此失明的编号构思、逐个验证指定编号、淘汰明显无效方向、归档正式建树前被终止的候选，并将通过初筛的大方向继续发展为 `001-01`、`001-02` 等受控分支。

## 为什么需要它

普通多轮头脑风暴很容易向最早出现的几个方案收敛：后续 Agent 读取了已有正文、术语和论证后，会不自觉地模仿、组合或围绕它们微调。

本 Skill 通过严格的上下文边界降低这种锚定：

- 创建根构思时，只读取公共题目与仅含标题的根索引；
- 验证时，只读取被点名的一个编号及其自身历史验证；
- 创建子构思时，只继承通过状态一致性检查的 `branch brief`，不读取父节点原始正文；
- 兄弟节点彼此只看到标题，不看到具体内容；
- 正式创建前触发门槛的候选使用独立 `ES-*` 记录归档，不进入构思树；
- 已失败结构只通过压缩的废案签名保留，不把完整失败论证塞回创造上下文；
- 用户明确批准前，所有构思都隔离在主项目之外。

隔离可以提高独立性，但不能自动证明想法新颖或正确。

## 核心操作

工作区完成一次性初始化后，每次运行只执行一种主要操作：

```text
CREATE ROOT
VERIFY 001
CREATE CHILD 001
SYNTHESIZE 001
```

成功的创建只写一个构思文件；有界尝试可以追加早期终止记录，但不会为这些候选创建构思或索引行。一次验证只检查一个编号。Skill 不会后台继续生长，也不会因为普通检索发现不确定性就擅自启动发散。

## 推荐工作节奏

```text
有限横向创建根构思
  -> 达到阈值后建议验证
  -> 逐项 VERIFY
  -> survives / weakened / blocked / busted
  -> 只从可行节点继续纵向分叉
  -> 用户明确触发综合与晋升
```

默认在以下任一条件达到时建议开始验证：

- 未验证根构思达到 6 个；
- 同一父节点下未验证子构思达到 3 个；
- 活跃未验证构思总数达到 8 个。

该提示不是硬性阻止。用户仍然可以明确要求继续创建新根方向。

当已经存在可行根节点时，普通的“继续头脑风暴”应优先建议验证或沿有效节点纵向深化，而不是无限增加根构思。

## 证据状态控制

证据成熟度必须逐级推进：

```text
speculative -> screened -> verified -> synthesis_ready -> protocol_ready
```

只有当前 `accepted` review 可以发布证据状态。branch brief 必须记录其来源 review 和证据版本；状态陈旧或来源不一致时，`CREATE CHILD` 必须停止。证据尚不成熟、新颖性不确定或证据池较小时，只产生需要用户确认的警告，不自动淘汰方向。科研证据闸门可以冻结分支，但不会删除它。

Review B 即使在第一次 review 中也必须挑战 Review A 的一个决定性主张，并记录该检查对
verdict 或 gate 的影响。

## 早期终止档案

`EARLY_STOPS.md` 保存因明确的创建前硬门槛而在正式建树前终止的完整候选。每条
`ES-YYYYMMDD-NN` 记录包含候选范围、停止理由、证据定位、不确定性、重开条件和压缩碰撞
签名。

早期终止不是构思状态、accepted review 或 busted verdict，不进入索引或分支。只有
唯一、完整、`source-checked` 且尚未解决的记录可以产生碰撞警告；`unverified` 或不完整
记录仅用于归档。重新考虑必须由用户点名一个 `ES-*` 记录、说明阻断条件的变化，并在新
idea 与索引提交后追加完整的 `ER-*` resolution event。

## 废案机制

明显不成立的构思保留稳定文件路径，但在索引中显示为：

```text
BUSTED.003
```

同时：

- 状态改为 `busted`；
- 扩展状态改为 `closed`；
- 在独立的 `BUSTED.md` 中追加失败类别、一句话理由、压缩碰撞签名和适用范围。

CREATE 操作先在不知道废案内容的情况下产生候选，再读取压缩废案账本进行碰撞检查。这样既能记住已经失败的路线，也不会让旧废案成为下一轮构思的起点。

## 仓库结构

```text
SKILL.md
references/
  workspace-and-isolation.md
  create-root.md
  verify-idea.md
  create-child.md
  lifecycle-and-governance.md
  anti-collapse-and-exploration.md
  synthesis-and-promotion.md
templates/brainstorm/
  AGENTS.md
  BRIEF.md
  EVIDENCE_GATE.md
  ROOT_INDEX.md
  BUSTED.md
  EARLY_STOPS.md
  idea.md
  review.md
  branch-brief.md
  child-index.md
  reservation.md
```

根 `SKILL.md` 检查 `AGENTS.md` 的 schema 标记和受管路径是否存在，但不读取这些文件的
正文。只有初始化、schema 不匹配、结构缺失或中断恢复时才加载修复手册。迁移先创建必需
路径，最后写入 schema 标记；未经用户明确确认，不覆盖已有但版本不匹配的 `AGENTS.md`。

## 关键边界

- 禁止递归读取整个 `brainstorm/`；
- 创建或验证时禁止读取兄弟节点正文；
- 原始构思不可修改，accepted review 正文和废案历史必须保留；
- 早期终止记录不进入构思索引，也不能发布证据状态；
- 不完整、重复、未核验或已经解决的早期终止记录不能过滤后续候选；
- draft 与 superseded review 不得发布证据状态；
- 陈旧或来源不匹配的 branch brief 不得创建子构思；
- `BUSTED` 只是索引显示标签，不重命名原构思文件；
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

```text
重新考虑 ES-20260729-01；它的重开条件可能已经满足，将其作为一个新根构思来源。
```

```text
继续头脑风暴。如果已经达到验证阈值，不要直接增加根构思，先建议应该验证哪些编号。
```

## 当前状态

这是第一版可运行规范。当前设计有意偏保守：优先保证隔离、可审计、有界探索和用户控制，而不是追求最大程度自动化。

## 许可证

MIT
