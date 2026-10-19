# 企业级集成架构 — 面试问答

> 核心场景：对一个没有任何 AI 基础设施的银行，如何从零落地 AI 服务

## Q1：AI 基础设施从零落地路径

### 前提：LLM 接入方式的选择

银行合规要求下，直接调用 `api.openai.com` 不可行：
- 数据进入 OpenAI 服务器，可能用于训练
- 数据主权和驻留地无法保证
- 银行监管通常明确禁止

**三种合规方式：**

| 方案 | 代表产品 | 数据边界 | 适用场景 |
|---|---|---|---|
| 企业私有云网关 | Azure OpenAI、AWS Bedrock、Google Vertex AI | 数据留在客户云租户内 | 已有云合同的企业，主流选择 |
| 私有化部署开源模型 | Llama/Mistral + vLLM/TGI | 数据完全不出内网 | 合规要求极高，接受能力损失 |
| 企业 AI 平台 | SAP AI Core (BTP) | 数据留在 BTP 租户内 | 已有大量 SAP 业务系统需集成 |

**关键澄清：**
- Azure OpenAI ≠ api.openai.com：模型独立部署在 Azure 数据中心，请求发到 `your-resource.openai.azure.com`，OpenAI 不可见
- SAP BTP 不是云基础设施，而是运行在 Azure/AWS/GCP 之上的企业应用平台；SAP AI Core 本身也跑在某个超大规模云上
- 选哪个方案不是技术问题，核心看：银行已有云合同在哪、数据和业务系统在哪、监管对数据驻留地的要求

**对没有 AI 基础设施的银行，落地路径：**
1. 确认云战略（已有 Azure/AWS 合同 → 优先用对应的托管 LLM 服务）
2. 没有 SAP 深度绑定 → 不需要引入 BTP，直接用云厂商 AI 服务更简单
3. 有大量 SAP 财务/HR 数据需要接入 AI → SAP AI Core 集成成本更低

## Q2：IAM 与 AI 服务集成

## Q3：数据平台对接（数据权限、data lineage）

## Q4：Secrets management、logging/monitoring 设计

## Q5：多租户/联邦架构下的平台设计

---

## 待深入话题
