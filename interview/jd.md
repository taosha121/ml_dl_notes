# JD 原文 + 解析

---

## What you'll do

### 1. Lead technical engagement for onboarding and adoption

- **Act as the primary technical point of contact for multiple use case teams adoption to the AI platform.**
  > 你是各业务团队接入 AI 平台的第一个技术窗口。意味着你要同时服务多个团队，节奏快、上下文切换频繁，沟通能力和技术广度缺一不可。

- **Run discovery sessions to understand business objectives, data constraints, risk posture, and non-functional requirements (e.g., security, latency, availability).**
  > Discovery session 是你主导的技术摸底会议，目标是把业务方的模糊需求翻译成技术约束条件。要问的不只是"你想做什么"，还有数据在哪、敏感程度如何、对延迟/可用性的要求、以及风险容忍度。

---

### 2. Provide platform capability advice and solution consultancy

- **Recommend the best-fit AI platform capabilities (e.g., model development, LLM enablement, deployment patterns, monitoring) for each use case.**
  > 平台提供多种能力，你要根据具体 use case 判断用哪个。比如：这个需求是 fine-tune 模型、还是用 RAG、还是直接 prompt 工程就够了？部署用 serverless 还是 dedicated endpoint？

- **Help teams choose the right capability and appropriate tooling aligned to platform standards.**
  > 不是推荐最先进的，而是推荐符合平台标准的。银行有统一的工具链和合规要求，你要在"团队想用"和"平台允许用"之间找到平衡点。

---

### 3. Accelerate delivery with reusable patterns

- **Support teams to integrate with platform services (identity/access, data sources, model, observability) and troubleshoot onboarding blockers.**
  > 这里列出的四类集成（IAM、数据源、模型服务、可观测性）是 AI 接入平台最常见的卡点。你的价值在于帮团队快速通过这些障碍，而不是让他们自己摸索。

---

### 4. Scale AI adoption across the bank

- **Identify common friction points and feed them back into the platform roadmap with clear evidence and prioritised recommendations.**
  > 你服务的是多个团队，天然能看到共性问题。这些问题要整理成有证据支撑的建议推给平台团队，而不是口头抱怨。

- **Build communities of practice: knowledge sharing sessions, office hours, internal enablement materials, and practical examples that raise the bar across teams.**
  > 这是规模化的关键——不是每次都手把手帮，而是把知识沉淀成文档、模板、示例代码，让团队自助。Office hours 是低成本高产出的机制。

---

### 5. Drive responsible and secure implementation

- **Encourage sound engineering practices and responsible AI behaviours, ensuring solutions align with HSBC's control expectations (e.g., security, model risk, data privacy).**
  > HSBC 有自己的 AI 控制框架（control expectations），你要确保各团队的实现符合这些要求，包括模型风险管理、数据隐私处理、安全工程实践。

- **Partner with risk, security, and governance stakeholders to help use case teams navigate the required approvals efficiently.**
  > 银行的审批流程复杂，风险/安全/合规部门各有诉求。你要帮业务团队搞清楚需要哪些审批、怎么走流程最快，而不是让他们在官僚体系里迷路。

---

### 6. Measure and improve outcomes

- **Track onboarding progress and adoption metrics (e.g., time-to-onboard, reuse of templates, deployment success rates) and continuously improve the engagement model.**
  > 用数据驱动改进。time-to-onboard（接入耗时）、模板复用率、部署成功率是典型的使能效率指标，说明你的工作是否真正降低了团队的摩擦。

---

## What you will need to succeed in the role

### 1. 学历要求

**Bachelor's/Master's/PhD degree in Machine Learning, Natural Language Processing, Computer Science, Data Science, Statistics, or related fields.**

> 门槛不算高，重点在后面的技术广度。学历本身不是筛选重点，但 ML/NLP 背景会让你在 LLM 技术问题上更有说服力。

---

### 2. Strong technical breadth across AI engineering and platforms

- **Experience with LLM enablement (prompting patterns, RAG, vector search, evaluation/guardrails) and productionising GenAI use cases.**
  > 这是最核心的技术要求。不只是"用过 ChatGPT"，而是把 LLM 应用推上生产的完整经验：RAG 怎么做、怎么评估效果、怎么加防护。

- **Experience working in large-scale, federated enterprises with shared platforms and diverse engineering standards.**
  > 大型联邦企业（各部门技术标准不统一）的工作经验。这说明你要能在"不是一个代码库、不是一个团队"的环境里推动事情。

- **Practical knowledge of modern AI stacks (e.g., Python, APIs/microservices, containers, cloud and hybrid environments).**
  > 生产环境的技术栈：Python + API 服务 + 容器化 + 云/混合云部署，这是把模型从 notebook 变成真实服务的基础能力。

---

### 3. Consultative engagement and stakeholder management

- **Proven ability to work with multiple delivery teams in parallel, translate ambiguous requirements into actionable technical recommendations, and influence without formal authority.**
  > 这个角色最难的部分：你没有直接管理权，但要影响多个团队的技术决策。"translate ambiguous requirements" 说明你要能处理业务方说不清楚需求的情况。

- **Strong communication skills—able to explain trade-offs clearly to engineers, product owners, and governance partners.**
  > 同一个方案要对三类人讲清楚：工程师（技术细节）、产品负责人（业务影响）、合规伙伴（风险控制）。语言要能切换。

---

### 4. Architecture and integration mindset

- **Experience designing integration patterns with enterprise services (identity and access management, data platforms, logging/monitoring, secrets management).**
  > 企业级集成的四个关键维度。IAM 决定谁能访问什么；数据平台决定数据怎么流；logging/monitoring 决定出问题能不能发现；secrets management 决定密钥怎么安全传递。

- **Ability to develop and socialise reference architectures and reusable implementation patterns.**
  > "Socialise" 是英式英语，意思是推广/让人接受。你不只是设计架构，还要让其他团队理解、接受并采用它。

---

### 5. Delivery focus and problem solving

- **Comfortable operating at pace: diagnosing onboarding issues, unblocking teams, and driving pragmatic solutions while maintaining standards.**
  > 速度和质量的平衡。"at pace" 说明节奏快，但 "maintaining standards" 说明不能为了快而走捷径绕过合规要求。

- **A continuous improvement approach—turning recurring issues into templates, documentation, and automation.**
  > 同一个问题解决两次是浪费，解决完要沉淀成模板/文档/自动化，让它不再是问题。

---

### 6. Risk-aware engineering

- **Awareness of key controls relevant to AI delivery in a regulated environment (security, privacy, resilience, model risk, auditability), and the discipline to build with these in mind.**
  > 在受监管环境（银行）里交付 AI，需要从设计阶段就把五类控制考虑进去：安全性、隐私、弹性、模型风险、可审计性。这不是事后打补丁，而是 built-in。
