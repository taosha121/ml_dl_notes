# LLM/GenAI 技术深度 — 面试问答

## Q1：RAG 系统完整链路设计

**问题：** 给内部业务部门搭一个 RAG 系统，让他们查询内部文档。描述完整链路设计。

**回答要点：**

### 文档处理阶段
- 分块策略用 **Recursive Character Splitting**：按 `\n\n` → `\n` → `. ` → ` ` 优先级递归切，保证自然边界且不超过 max_chunk_size
- 对结构复杂的银行文档（合规、产品说明），可用 **Parent-Child Chunking**：小块用于检索精度，大块（parent）送给 LLM 提供完整上下文
- 切块后调用 embedding 模型向量化，存入向量数据库，同时保留 **metadata**（来源文档、页码、章节）

### 检索阶段
- 用户 query 向量化后不能只做纯向量搜索，要用 **Hybrid Search**：
  - 向量搜索负责语义相似
  - BM25 负责精确词命中（产品代码、人名、金融术语）
  - 两路结果用 **RRF（Reciprocal Rank Fusion）** 合并排序
- 召回 20~50 条后用 **Cross-Encoder Reranker** 精排，取 Top 3~5

### 生成阶段
- 检索结果 + 用户问题组成 prompt，要求模型：严格按检索内容回答，标注答案出处，查不到则明确说不知道
- 返回答案时附带 **citation**（文档名、页码），支持用户核查

---

## Q2：RAG 答案质量不稳定，如何排查

**问题：** 上线后业务反馈答案质量不稳定，有时答非所问。如何排查解决？

**回答要点：**

### 第一步：隔离问题层
- 检索失败（相关文档没召回）vs 生成失败（召回了但 LLM 答错）
- 手动抽查：看检索结果是否已包含正确答案，以此判断问题出在哪一层

### 第二步：构建评估集
- **合成数据（上线前）**：用 LLM 对每个文档块生成 3~5 个问题，形成 `query → ground truth chunk` 的测试集，覆盖面广，不需要人工标注
- **用户反馈（上线后）**：收集业务部门报告的失败案例并打标，补充真实边界情况

### 第三步：量化评估

| 层 | 指标 |
|---|---|
| 检索 | Recall@K、MRR、NDCG |
| 生成 | Faithfulness（答案是否忠于检索内容）、Answer Relevance |

- 工具：**RAGAs** 框架专门做 RAG 全链路评估

### 第四步：针对性优化
- 检索问题：调整 chunking 策略、引入 hybrid search、优化 reranker
- 生成问题：调整 prompt、优化上下文拼接方式、考虑领域微调

---

## Q3：生产环境 LLM 部署——延迟、成本、可观测性

### 延迟优化
- **Prompt caching**：对重复的 system prompt 前缀缓存，Azure OpenAI 原生支持，延迟和成本同时降
- **流式输出（Streaming）**：边生成边返回，用户感知延迟大幅降低
- **Embedding 缓存**：相同 query 的向量化结果缓存，避免重复调用
- **异步并行**：query embedding 与其他预处理并行跑，不串行
- 注意：Azure OpenAI 有 **TPM/RPM 配额限制**，高峰打满会 429，需提前申请配额或做限流

### 成本管理
- 按需选模型：简单问答用 GPT-4o-mini，成本比 GPT-4 低 10 倍以上
- 控制 context 长度：召回文档块设 token 上限，超了截断
- 监控每次请求 token 消耗，按部门/用户设配额防滥用
- 上线前估算：日均查询量 × 平均 token 数 = 月度账单预测

### 可观测性（应用层，云服务商不提供）
云服务商只给 API 层指标（调用量、错误率），应用层需自建：
- 记录完整链路：query → 召回 chunks → rerank 结果 → prompt → LLM 输出 → 最终答案
- 关键指标：端到端延迟、各步骤耗时分布、召回相关性分数、用户反馈（点赞/踩）
- 工具：LangSmith（LangChain 生态）、Arize Phoenix（开源）、或自建结构化日志到 Elasticsearch

---

## Q4：Prompt Engineering / Evaluation / Guardrails

### Evaluation

**检索层：**
- Recall@K：Top-K 结果里有没有包含正确答案
- MRR（Mean Reciprocal Rank）：正确文档排在第几位
- NDCG：考虑排序质量的综合指标

**生成层：**

| 指标 | 含义 |
|---|---|
| Faithfulness | 答案是否只用了检索内容，没有编造 |
| Answer Relevance | 答案是否真正回答了用户问题 |
| Context Precision | 召回内容中真正有用的比例 |

- 打分方式：小批量人工标注 + LLM-as-judge（RAGAs 框架）批量评分，两者结合做校准
- 工具：**RAGAs**

**银行场景额外指标：**
- **Hallucination rate**：LLM 编造数字（利率、费用）是高风险事件，单独追踪
- **Refusal rate**：查不到时模型有没有正确说"不知道"

### Guardrails

**输入层（query 进来时）：**
- Prompt injection 检测：识别嵌入指令（"忽略之前的指令..."），用分类模型或规则
- 话题过滤：竞争对手、不相关话题直接拒绝
- PII 检测：身份证号、卡号等敏感信息脱敏或拒绝

**输出层（LLM 生成后）：**
- Azure AI Content Safety：内置内容审核，开箱即用
- Faithfulness 检查：输出有没有超出 source chunks 的内容
- PII 泄露检测：检索文档里的敏感信息不能出现在答案里

**System Prompt 设计：**
- 明确角色边界，限定回答范围
- 关键指令放 prompt 末尾（靠近 user input，比放开头更难被覆盖）

**工具选型：**
- Azure AI Content Safety（已在 Azure 团队首选）
- Guardrails AI / NeMo Guardrails（开源，可自定义规则）
- LlamaGuard（Meta 开源，专用 input/output 安全分类模型）

**生产运营要点：** Guardrails 不是一次性设计好就完，需持续收集被拦截 case，分析误拦和漏拦，定期迭代规则。

---

## Q5：向量数据库选型

### 多租户场景（多部门文档隔离）
用 metadata 过滤做逻辑隔离可行，但需区分两件事：
- **逻辑隔离**：查询时加 metadata 过滤条件，A 部门只查 A 的数据
- **权限隔离**：A 部门的人在技术上无法访问 B 部门数据，需要数据库层权限控制

### 各数据库对比

| 数据库 | 特点 | 适用场景 |
|---|---|---|
| **HANA** | 企业数据库附带向量能力，非专用 | 已有 license，数据量不大，团队熟悉 |
| **Qdrant** | Rust 实现，性能好，向量+metadata 同时过滤不降速 | 性能要求高、过滤条件复杂 |
| **Weaviate** | 内置 hybrid search（向量+BM25），GraphQL API | 希望开箱即用 hybrid search |
| **Milvus** | 十亿级向量，架构复杂（存储/计算/消息队列分离） | 超大规模，有专职运维团队 |
| **ChromaDB** | 轻量，易用 | 本地开发和原型验证，不适合生产 |

### 银行场景选型原则
不是哪个最好，是哪个最适合现有基础设施和团队能力。引入新组件意味着新的运维负担和安全审批——在银行这个成本很高。