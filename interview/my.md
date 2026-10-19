# AI Platform Technical Enablement - 面试准备

## 1. LLM/GenAI 技术深度

硬门槛，会追问具体实践：

- RAG 的完整链路（chunking、embedding、retrieval 策略、reranking）
- Prompt engineering / evaluation / guardrails 怎么做
- 生产环境 LLM 部署：latency、成本、可观测性怎么保证
- 向量数据库选型经验

---

## 2. 企业级集成架构

银行强调的 enterprise 场景：

- IAM（identity/access）如何与 AI 服务集成
- 数据平台对接（数据权限、data lineage）
- secrets management、logging/monitoring 的设计
- 多租户/联邦架构下的平台设计

---

## 3. Responsible AI（受监管行业）

HSBC 是银行，这块权重很高：

- model risk 怎么管理（模型审批、版本控制、回滚）
- 数据隐私合规（PII 处理、数据出境）
- auditability：决策可追溯性怎么设计
- 安全控制（prompt injection、数据泄露防护）

---

## 4. 跨团队影响力（行为面试）

这个角色不管人，靠影响力推动：

- 如何让不配合的团队采纳平台方案
- 如何把模糊的业务需求转化成技术方案
- 遇到不同团队标准冲突怎么处理

---

## 5. 规模化思维

不是解决一个问题，是建立可复用的模式：

- 你做过哪些"一次解决、多团队复用"的事
- 如何识别共性 friction point 并推动平台改进
- 内部知识沉淀（文档、模板、enablement 材料）怎么做
