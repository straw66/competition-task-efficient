# Competition Task Efficient

一个面向 Codex / AI Coding Agent 的高质量、低 Token 竞赛任务执行 Skill。

它适用于：

- 算法竞赛
- 企业赛题
- 数据挖掘比赛
- 机器学习与深度学习项目
- 多文件工程任务
- 需要长期实验管理的复杂项目

核心目标是：

> 在保证任务完整实现、代码可运行、结果可复现和效果优先的前提下，减少无效文件读取、重复分析、重复计划和无依据试错造成的 Token 浪费。

---

## 特性

- 精简任务规划
- 局部文件读取
- Baseline 最小闭环
- 条件式 Skill 路由
- 实验版本管理
- 故障诊断
- 提交前审查
- 长会话交接
- 低 Token 输出规范
- 与 `AGENTS.md`、`planning-with-files` 等工作流兼容

---

## 推荐搭配

该 Skill 可以独立使用，也可以与以下 Skills 配合：

- `planning-with-files`
- `diagnosing-bugs`
- `codebase-design`
- `tdd`
- `review`
- `handoff`

这些 Skills 不会被无条件同时调用，而是根据任务阶段按需触发。

---

## 目录结构

```text
competition-task-efficient/
├── README.md
├── SKILL.md
└── AGENTS.example.md
```

---

## 安装方式

### 方法一：安装到通用全局目录

```bash
mkdir -p ~/.agents/skills/competition-task-efficient
cp SKILL.md ~/.agents/skills/competition-task-efficient/SKILL.md
```

然后重启 Codex。

### 方法二：安装到 Codex 全局目录

```bash
mkdir -p ~/.codex/skills/competition-task-efficient
cp SKILL.md ~/.codex/skills/competition-task-efficient/SKILL.md
```

然后重启 Codex。

### 方法三：项目级安装

在项目根目录执行：

```bash
mkdir -p .agents/skills/competition-task-efficient
cp SKILL.md .agents/skills/competition-task-efficient/SKILL.md
```

项目级安装只对当前项目生效，适合随仓库一起提交。

---

## 使用方式

### 显式调用

```text
$competition-task-efficient
```

然后描述任务：

```text
完成当前目录中的赛题。

先读取 AGENTS.md、赛题说明、README、baseline、数据目录结构和提交样例。
先跑通 baseline 和本地评测闭环，再分析评分瓶颈并实现改进。

最终交付：
1. 可运行完整代码；
2. 环境和依赖说明；
3. 训练、推理与评测命令；
4. 本地验证结果；
5. 合规提交文件；
6. 当前最佳版本；
7. 精简技术方案说明。

减少全仓扫描、重复读取、重复实验和冗长输出，但不得省略必要测试。
```

### 自然语言调用

```text
请使用 competition-task-efficient skill 完成当前赛题。
```

---

## 推荐启动提示词

```text
请使用 competition-task-efficient skill 完成当前赛题。

任务目标：
[填写具体目标]

赛题资料：
[填写赛题说明、README、数据、baseline 和提交样例的位置]

硬件与时间约束：
[例如：RTX 4090D 一张，7 天内完成]

最终交付：
[例如：完整代码、训练命令、推理命令、本地评测、提交文件、技术文档]

优先级：
1. 先完整跑通；
2. 再提高评分指标；
3. 保证提交合规；
4. 保证结果可复现；
5. 减少无效 Token 消耗。

请自动遵守项目 AGENTS.md。
复杂任务按需调用 planning-with-files，但计划最多六个阶段，只在主要阶段完成后更新。
不要同时无条件调用所有 Skill。
出现错误时调用 diagnosing-bugs。
确定性逻辑按需调用 tdd。
跨模块设计时调用 codebase-design。
候选提交完成后调用 review。
会话过长时调用 handoff。

现在先检查已有项目状态、赛题要求和 baseline，建立最小闭环，然后直接执行，不要只给方案。
```

---

## 工作流程

```text
赛题理解
  ↓
Baseline 最小闭环
  ↓
数据与指标分析
  ↓
核心方案实现
  ↓
针对性验证
  ↓
异常诊断
  ↓
候选提交审查
  ↓
版本保存与交接
```

---

## Token 节省策略

该 Skill 不通过降低任务质量来节省 Token，而是减少以下浪费：

- 默认扫描整个仓库
- 重复读取未修改文件
- 重复解释背景
- 每次工具调用都更新计划
- 同时加载多个无关 Skill
- 完整读取大型数据文件
- 对已失败方案重复实验
- 输出未修改的大段代码
- 生成不必要的中间文档
- 没有证据的盲目调参

---

## 完成标准

只有同时满足以下条件，任务才算完成：

- 主流程可以运行
- 输出格式正确
- 必要测试通过
- 结果可以复现
- 提交文件已经生成
- 与评分规则不存在明显冲突
- 关键命令、参数和结果已经记录

---

## 适用场景

### 推荐使用

- 完整赛题开发
- 多文件功能实现
- 长期实验优化
- 多轮提交与榜单迭代
- 复杂 Bug 定位
- 多模块工程重构
- 需要维护最佳版本的项目

### 不建议使用

以下简单任务通常不需要该 Skill：

- 修改一行代码
- 更改一个参数
- 修复明确的拼写错误
- 单纯解释一段代码
- 执行一次简单命令

---

## License

建议使用 MIT License。
