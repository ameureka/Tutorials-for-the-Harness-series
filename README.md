# Harness Engineering for Production AI Agents

<p align="center">
  <strong>大模型智能体工程化交付指南：控制权三分编排 · 长上下文治理 · MCP 协议 · 对抗评测 (Eval) · SSD 全栈规范</strong>
</p>

<p align="center">
  <a href="./LICENSE"><img src="https://img.shields.io/badge/License-CC--BY--4.0-blue.svg" alt="License: CC-BY-4.0"></a>
  <img src="https://img.shields.io/badge/PRs-Welcome-brightgreen.svg" alt="PRs Welcome">
  <img src="https://img.shields.io/badge/Architecture-Control--Thirds-blueviolet.svg" alt="Architecture: Control-Thirds">
  <img src="https://img.shields.io/badge/Methodology-SSD-orange.svg" alt="Methodology: SSD">
  <img src="https://img.shields.io/badge/Modules-8%20Editions-success.svg" alt="Modules">
</p>

---

## 📌 系统定义：什么是 Harness Engineering？

在大模型驱动的应用架构中，单纯依赖 Prompt 调优无法保证生产级交付的确定性。

**Harness Engineering（工程地基）** 是包裹在大模型外部的确定性工程约束系统。它假定模型具备随机性与潜在脆弱性，通过**规范驱动 (Specification-Driven)、运行时状态机 (State Machine) 与闭环评测门禁 (Eval Gates)**，将大模型的概率推理收敛为高可用、具备防御能力的软件工程系统。

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                       Harness 生产级智能体运行时分层                          │
├─────────────────────────────────────────────────────────────────────────────┤
│  [应用层]  全栈客户端 (Next.js / SSR)  ──  服务端强类型 API Gateway          │
├─────────────────────────────────────────────────────────────────────────────┤
│  [控制层]  控制权三分编排器 (Workflow / Agent / Human 动态路由状态机)        │
├─────────────────────────────────────────────────────────────────────────────┤
│  [上下文]  长文本治理 (Sliding Window · Progressive Disclosure · Caching)    │
├─────────────────────────────────────────────────────────────────────────────┤
│  [工具层]  Model Context Protocol (MCP) 沙箱 · 强 Schema 校验 · 密钥物理隔离│
├─────────────────────────────────────────────────────────────────────────────┤
│  [防御层]  自动化评测断言 (Eval Gates) · 死循环熔断 · 分布式链路追踪 (APM)    │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## 🏛️ 核心架构模式：控制权三分矩阵 (Control-Thirds Matrix)

复杂业务交付的核心在于**执行控制权的精准切分**。避免在单 Agent 内混合确定性规则与模糊推理：

| 执行主体 | 适用边界 | 技术实现方式 | 典型反模式 (Anti-Pattern) |
|---|---|---|---|
| **确定性 Workflow** | 规则固定、数据流可预测、数学计算、格式转换、入库校验 | 原生代码 (TS/Python/Go)、状态机、定时批处理 | 用大模型算数学题、用 Agent 格式化标准 JSON |
| **自适应 Agent** | 开放语义理解、多策略推理、动态规划、代码生成 | 大模型推理引擎、反思重试机制 (Reflective Loop) | 让 Agent 直接持有生产数据库写权限或随意调外部系统 |
| **人类介入 (HITL)** | 资金支付、高危指令、合规审查、终审交付确认 | 阻塞式审批流、Webhook 回调、带签名确认凭证 | 允许 Agent 无人值守自主执行高危不可逆操作 |

---

## 🗺️ 全系列 8 期实战进阶路线图

本教程将企业级落地链路拆解为 8 个递进模块，提供公开课件、技术规范与导读：

```text
[001 起步构建] ──> [002 代码重构] ──> [003 模型分层] ──> [004 上下文工程]
                                                              │
[008 可观测性] <── [007 全栈实践] <── [006 任务编排] <── [005 Tools使用]
```

| 期次 | 专题名称 | 工业级核心议题 | 架构产物与文档 |
|:---:|---|---|---|
| **001** | [起步构建与架构通识](./001-AI%20时代第一步动起来/) | 从 Prompt 转向工程系统；MVP 极速开发链路；执行循环三要素 | [`课件 PPTX`](./001-AI%20时代第一步动起来/001-ai%20时代第一步动起来-公开幻灯片.pptx) · [`导读`](./001-AI%20时代第一步动起来/README.md) |
| **002** | [代码走查与架构重构](./002-作品点评/) | 真实应用评审四大维度；消除隐式修改；从 Demo 演进为高可用工程 | [`重构指南`](./002-作品点评/README.md) |
| **003** | [模型能力分层与评测](./003-Harness%20工程素养基础-模型/) | 旗舰模型与轻量模型分层路由；自动化 Eval 基准测试；语义断言 | [`课件 PPTX`](./003-Harness%20工程素养基础-模型/003-Harness%20工程素养基础-模型.pptx) · [`导读`](./003-Harness%20工程素养基础-模型/README.md) |
| **004** | [上下文工程实践](./004-上下文工程/) | 治理注意力稀释；滑动窗口状态压缩；Prompt Caching 成本控制 | [`课件 PPTX`](./004-上下文工程/004-上下文工程-公开幻灯片.pptx) · [`导读`](./004-上下文工程/README.md) |
| **005** | [Tools 与 MCP 协议集成](./005-Tools的使用/) | Model Context Protocol 标准化实现；入参强类型校验；沙箱隔离 | [`课件 PPTX`](./005-Tools的使用/005-tools使用-公开幻灯片.pptx) · [`导读`](./005-Tools的使用/README.md) |
| **006** | [任务编排与 Multi-Agent](./006-多agent%20协作/) | 控制权三分法则；Pipeline 到 Graph 图调度演进；收敛性治理 | [`课件 PPTX`](./006-多agent%20协作/006-多agent协同-公开幻灯片.pptx) · [`导读`](./006-多agent%20协作/README.md) |
| **007** | [SSD 全栈工程实践](./007-harness工程素养实践/) | Specification-State-Distill 落地；Next.js + Edge + D1 闭环交付 | [`课件 PPTX/PDF`](./007-harness工程素养实践/007-Harness与SSD全栈应用实战-公开幻灯片.pdf) · [`导读`](./007-harness工程素养实践/README.md) |
| **008** | [生产级可观测性设计](./008-可观测性/) | OpenTelemetry 链路追踪；Token 成本多维核算；死循环熔断断路器 | [`实践大纲`](./008-可观测性/README.md) |

---

## ⚙️ 规范先行：Specification-State-Distill (SSD) 工作流

本仓库遵循 SSD 软件工程体系：
1. **Specification（规范先行）**：
   任何功能实现前，必须冻结接口定义（Schema）、错误码体系与安全边界（Spec）。杜绝无约束的自然语言盲目生成。
2. **State（受控状态机）**：
   核心业务状态独立持久化于数据库或集中式状态机中。大模型仅作为无状态算子（Stateless Operator）参与处理。
3. **Distill（提炼沉淀）**：
   运行过程中的异常、边界缺陷与失败用例持续提炼沉淀为自动化 Eval 断言集，反哺工程防线。

---

## 🤝 贡献与参与 (Contributing)

欢迎提交 Issue 与 Pull Request：
* **课件修正**：若发现 PPTX / 导读中的技术要点存在表述歧义或版本滞后，欢迎提交修复；
* **案例扩充**：欢迎贡献真实的生产级代码走查案例（需脱敏）或 MCP Server 实现范式。

---

## 📜 许可证 (License)

本开源教程所有公开幻灯片、文档、讲义与导读均遵循 **[Creative Commons Attribution 4.0 International (CC-BY-4.0)](./LICENSE)** 知识共享许可协议。可在遵守署名要求的前提下自由分发、引用与演进。
