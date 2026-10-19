# JD 原文 + 解析：Senior Manager AI Initiatives

**Business:** Finance COO

---

## 职责（Principal Responsibilities）

### 1. Platform architecture & core capability design
> 主导 AI Agent 平台的整体架构设计和核心能力建设，涵盖任务编排、工具调用、上下文管理、记忆机制和多智能体协作。

这是整个 JD 的核心职责。不是用 AI 工具，而是**造平台**——把 LLM 底座、agent 框架、工具层、记忆层这些东西组合成一个企业级可运营的系统。每个子能力（task orchestration / tool invocation / context management / memory / multi-agent）都是独立的技术深度方向，面试时会逐一被追问设计思路。

---

### 2. AI-native engineering integration
> 将 AI 原生能力嵌入工程流程，包括 AI 辅助编码、技术方案生成、测试用例生成、测试报告生成、环境自动化配置/编排。

Finance COO 下的 engineering team 要用 AI 提效。这里列出的五类场景（coding、方案生成、test case、test report、环境编排）本质上是把 LLM/agent 接入 SDLC 各阶段。需要既懂 AI 能力边界，又懂工程研发流程的人来做接入设计。

---

### 3. Knowledge augmentation layer design
> 设计、集成和应用企业级知识增强能力，包括：RAG、GraphRAG、知识图谱（设计、集成与应用）。

三项能力递进：RAG 是基础，GraphRAG 是在图结构上做检索增强，知识图谱是更底层的结构化知识表示。把三项都列出来说明不满足于基础 RAG，需要有处理复杂实体关系的能力。GraphRAG 和知识图谱在银行场景（客户关系、合规规则、产品依赖图）有很强的落地动机。

---

### 4. Runtime governance & operational framework
> 建立 AI Agent 运行时和治理框架，包括：隔离与沙箱化、访问控制与权限管理、可审计性与可追溯性、评估与质量度量、稳定性/可靠性/成本管理。

这是银行场景特有的重量级要求。Agent 在生产环境里运行会调用真实工具（API、数据库、代码执行），必须有沙箱边界和权限最小化。可审计性在银行是合规红线。五项要求里每一项都有对应的工程设计选择，面试会考你具体怎么做。

---

### 5. Cross-functional delivery
> 与产品、工程、QA、运营、平台团队合作，将平台能力标准化并推向生产，提升交付质量和工程效率。

Senior Manager 的跨职能协作要求。不只是自己设计，还要推动多团队对齐标准、共同交付。这里的关键词是 "standardise and productionise"——把能力从 PoC 状态变成可重复使用的生产级服务。

---

## 要求（Requirements）

### 学历
**Bachelor's degree or above（计算机/软件工程/AI 相关专业优先）**

> 学历门槛不高，专业方向是加分项而非硬卡点。

---

### 经验
**8+ 年后端/平台工程、架构或同等企业级交付经验；近 3 年有 AI 生产落地经验。**

> 8 年是资历门槛，说明这个职位要求有完整的系统演进经历，不只是项目经验。近 3 年 AI 生产经验是实质筛选点——不能只是研究或 PoC，必须有真实系统上线运营的案例。面试时要准备具体的生产项目：上线了什么、规模多大、遇到什么生产问题、怎么解决的。

---

### 系统思维（System thinking）
**具备设计和演进复杂系统的能力，关注可扩展性、可维护性和性能。**

> "Evolve"是关键词——不只是设计初版，还要能随业务变化迭代架构。银行 AI 平台会从小规模 PoC 扩展到全行使用，架构要能支撑这个演进路径。面试中可能会问：如果用户量 10 倍增长，你的设计哪里会先崩？

---

### 工程能力（Engineering strength）
**精通 Java/Python，有扎实的编码功底和架构判断力；有复杂系统交付的实践经验。**

> 同时列 Java 和 Python 说明是银行技术栈（Java 是传统后端主力，Python 是 AI 栈），要能在两者之间切换。"Architectural judgment"比编码速度更重要——面试会考你在给定约束下怎么做技术选型。

---

### AI/Agent 架构（Must Have）
**深入理解 LLM 和 agent 架构，包括：**
- **任务分解与规划（Task decomposition & planning）**
- **工具使用/函数调用模式（Tool use / function calling patterns）**
- **上下文与会话管理（Context and session management）**
- **记忆设计（Memory design）**
- **执行循环与异常处理（Execution loops and exception handling）**

**有 LangChain 和/或 LangGraph（或同类编排框架）的实践经验。**

**熟悉主流 AI 编码和开发工具（如 Claude Code、Codex、Cursor、Copilot 等）。**

> Must Have 意味着这是硬筛点，没有直接淘汰。五个子能力方向：
> - **Task decomposition**：ReAct / Plan-and-Execute / Tree of Thoughts 等范式，以及在 agent 失败时怎么降级
> - **Tool use**：function calling 的设计，工具描述怎么写、schema 怎么定义、错误怎么处理
> - **Context/session management**：长对话的 context window 管理，multi-turn 状态怎么维护
> - **Memory design**：short-term（in-context）vs long-term（外部存储）vs episodic memory，分别用在什么场景
> - **Execution loops & exception handling**：agent 卡死、工具调用失败、结果不符合预期时的重试/回滚/人工介入机制
>
> LangGraph 尤其重要——它是目前企业级 stateful multi-agent 的主流选择，要能说清楚为什么选 LangGraph 而不是单纯的 LangChain。
>
> AI 编码工具的熟悉度要求符合职责 2（AI-native engineering integration），面试时可以结合自己用 Claude Code/Cursor 的实际体验来回答。

---

### 知识与检索工程（Strong Plus）
**有企业级 RAG、GraphRAG 或知识图谱解决方案的实际设计和落地经验。**

> "Strong Plus"不是可选项，几乎是必备——因为职责 3 整个模块都围绕这个展开。重点是"enterprise"场景的经验：数据权限隔离（不同团队只能检索自己的数据）、大规模 embedding 更新策略、GraphRAG 在有复杂关系的业务场景（如合规规则图、客户关系图）的落地。

---

### 平台与云工程（Strong Plus）
**具备 DevOps 思维；有 DevOps 实践、CI/CD、Kubernetes、云原生技术经验。**

**能驱动跨团队执行，在生产环境交付结果。**

> AI Agent 平台要跑在 K8s 上，要有 CI/CD 保障，要做成云原生服务。这不是 AI 算法工程师的工作范围，而是强调平台工程能力。"Drive cross-team execution"和跨职能交付（职责 5）呼应，说明这个人既要能写架构，也要能推动别人按架构落地。

---

## 整体判断

这个职位和上一个的核心差异：

| | 上一个职位（AI Platform Enablement）| 本职位（Senior Manager AI Initiatives）|
|---|---|---|
| 定位 | 使能顾问，帮各团队接入平台 | 平台建设者，设计并交付 agent 平台 |
| 技术深度方向 | LLM 应用 + 企业集成 | Agent 架构 + 知识图谱 + 治理框架 |
| 领导力要求 | 影响力领导（无直接管理权）| Senior Manager，跨职能交付 |
| 核心产出 | 接入加速 + 最佳实践沉淀 | 可运营的 AI Agent 平台 |

**最需要补强的准备方向：**
1. LangGraph stateful agent 的具体设计案例（multi-agent + 状态管理）
2. Agent 治理框架的具体实现方案（沙箱、权限、审计）
3. GraphRAG 或知识图谱的实际落地案例（有或没有，如果没有要想好如何回答）
4. Senior Manager 层面的跨团队交付案例（推动了什么标准落地、解决了什么跨团队摩擦）
