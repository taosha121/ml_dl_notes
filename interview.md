# AI 算法工程师 & Agent 开发工程师面试题库

> 整理自互联网大厂（字节、阿里、腾讯、百度、美团、华为）公开面经与技术文档，2024–2025

---

## 目录

1. [机器学习基础](#1-机器学习基础)
2. [深度学习基础](#2-深度学习基础)
3. [Transformer 与注意力机制](#3-transformer-与注意力机制)
4. [大模型预训练与微调](#4-大模型预训练与微调)
5. [模型压缩与推理优化](#5-模型压缩与推理优化)
6. [分布式训练](#6-分布式训练)
7. [RAG 与向量检索](#7-rag-与向量检索)
8. [Agent 开发](#8-agent-开发)
9. [多模态](#9-多模态)
10. [系统设计](#10-系统设计)
11. [算法与编程题](#11-算法与编程题)
12. [行为题与项目深挖](#12-行为题与项目深挖)

---

## 1. 机器学习基础

### 评估指标
- AUC 和 LogLoss 分别衡量什么？业务上如何选择？
- Precision/Recall/F1 的区别，什么场景下更关注 Recall？
- ROC 曲线怎么画？AUC=0.5 意味着什么？
- 多分类问题如何计算 Macro-F1 和 Micro-F1？

### 过拟合与正则化
- L1 和 L2 正则化的区别？L1 为什么会产生稀疏解？
- Dropout 的原理？训练和推理时的行为有何不同？
- Batch Normalization 和 Layer Normalization 的区别？各适用于什么场景？
- 什么是 Early Stopping？有什么风险？

### 优化器
- SGD、Adam、AdamW 的区别？大模型训练为什么常用 AdamW？
- 学习率 warmup 的作用是什么？
- 梯度消失和梯度爆发如何解决？
- 余弦退火学习率调度怎么工作？

### 经典模型
- 逻辑回归和 SVM 的区别？
- 随机森林和 GBDT 的区别？XGBoost 的核心优化点是什么？
- K-Means 的缺点？如何选择 K 值？
- 朴素贝叶斯的"朴素"假设是什么？什么时候会失效？

---

## 2. 深度学习基础

### 基础网络
- CNN 中 1x1 卷积的作用？
- ResNet 残差连接解决了什么问题？原理是什么？
- LSTM 相比 RNN 的改进？各个门（遗忘门、输入门、输出门）的作用？
- Batch Size 对训练的影响？大 Batch 训练有什么问题，如何缓解？

### 训练技巧
- 权重初始化为什么重要？Xavier 和 He 初始化分别适用什么情况？
- 混合精度训练（FP16/BF16）原理是什么？为什么 BF16 比 FP16 更稳定？
- 梯度累积的作用是什么？
- Label Smoothing 的作用？

### Loss 函数
- 交叉熵损失的推导？
- Focal Loss 解决什么问题？如何调整 α 和 γ？
- 对比学习中的 InfoNCE Loss 原理？

---

## 3. Transformer 与注意力机制

### 核心原理
- Self-Attention 的 Q/K/V 是怎么来的？为什么要除以 sqrt(d_k)？
- Multi-Head Attention 的作用？多个 head 各自关注什么？
- Self-Attention 的计算复杂度是多少？有哪些优化方式（稀疏注意力、线性注意力等）？
- Encoder-Decoder Attention 和 Self-Attention 的区别？

### 位置编码
- 为什么 Transformer 需要位置编码？
- 绝对位置编码和相对位置编码的区别？
- RoPE（旋转位置编码）的原理是什么？相比 ALiBi 有什么优势？
- 如何让模型支持比训练时更长的上下文（长度外推）？

### GPT / BERT 系列
- BERT 和 GPT 的架构区别？各适合什么任务？
- GPT 的 Causal Mask 是怎么实现的？
- BERT 的 MLM 和 NSP 任务分别是什么？为什么后来 NSP 被去掉？
- GPT-2 到 GPT-3 的主要变化？

### KV Cache
- KV Cache 的原理是什么？节省了什么计算？
- KV Cache 占用多少显存？如何计算？（以一个具体模型举例）
- PagedAttention 解决了 KV Cache 的什么问题？
- Prefix Caching 的原理与适用场景？

### 现代 LLM 架构改进
- GQA（Grouped Query Attention）和 MQA（Multi-Query Attention）的区别？
- SwiGLU 激活函数相比 ReLU 的优势？
- RMS Norm 和 Layer Norm 的区别？
- Llama 系列架构有哪些关键设计选择？

---

## 4. 大模型预训练与微调

### 预训练
- 大模型预训练的数据配比（代码/网页/书籍等）如何影响模型能力？
- Tokenization 中 BPE、WordPiece、SentencePiece 的区别？
- 为什么大模型词表通常在 32K–100K 之间？词表大小的权衡是什么？
- 预训练阶段的 Loss 曲线异常（spike）如何处理？

### SFT（监督微调）
- SFT 和预训练的区别？SFT 数据量需要多少？
- 为什么 SFT 之后模型有时会"遗忘"预训练知识（灾难性遗忘）？如何缓解？
- Chat 模板（System/User/Assistant）在训练时如何处理？

### RLHF / 对齐
- RLHF 的完整流程（SFT → Reward Model → PPO）是什么？
- DPO（Direct Preference Optimization）和 RLHF 的区别？DPO 有什么优缺点？
- PPO 在 RLHF 中的 KL 惩罚项是做什么的？
- ORPO、SimPO 等新方法相比 DPO 的改进是什么？

### PEFT / 参数高效微调
- LoRA 的数学原理是什么？A 矩阵和 B 矩阵的初始化方式？
- LoRA 的 rank 如何选择？rank 越大越好吗？
- QLoRA 相比 LoRA 的改进是什么？NF4 量化是怎么工作的？
- Adapter、Prefix Tuning、Prompt Tuning、LoRA 的对比？
- LoRA 合并到原始权重的方式？合并后推理有额外开销吗？
- 什么是 DoRA？相比 LoRA 的改进点？

---

## 5. 模型压缩与推理优化

### 量化
- PTQ（训练后量化）和 QAT（量化感知训练）的区别？
- INT8 量化的原理？对称量化和非对称量化的区别？
- GPTQ、AWQ、SmoothQuant 各自的核心思路？
- 4-bit 量化对模型精度的影响？哪些层更敏感？
- 如何用校准集（calibration set）做 PTQ？

### 剪枝与蒸馏
- 结构化剪枝和非结构化剪枝的区别？
- 知识蒸馏的原理？温度参数 T 的作用？
- 如何设计蒸馏损失（软标签 + 硬标签的组合）？
- 中间层蒸馏（feature distillation）和输出层蒸馏的区别？

### 推理加速
- Flash Attention 的原理？解决了什么问题？
- Speculative Decoding 的原理？draft model 如何选择？
- Continuous Batching（连续批处理）相比 static batching 的优势？
- Tensor Parallelism 和 Pipeline Parallelism 在推理中如何使用？
- vLLM、TensorRT-LLM、TGI 的区别与适用场景？

---

## 6. 分布式训练

### 并行策略
- 数据并行（DP）、模型并行（MP）、流水线并行（PP）的区别？
- Tensor Parallelism 如何切分 Transformer 的矩阵乘法？
- ZeRO（Zero Redundancy Optimizer）的三个阶段各优化了什么？
- DeepSpeed 和 FSDP（Fully Sharded Data Parallel）的区别？

### 通信优化
- All-Reduce 和 All-Gather 的区别？各在什么场景使用？
- 梯度压缩（gradient compression）的方法有哪些？
- 训练时 GPU 之间的通信瓶颈如何分析和优化？

### 工程实践
- 如何估算训练一个 7B 模型所需的显存？
- 大规模训练中如何做 Checkpoint 和断点续训？
- 训练数据去重的方法（MinHash、ExactDedup 等）？

---

## 7. RAG 与向量检索

### 基础架构
- RAG 的完整流程是什么（索引、检索、生成）？
- Dense Retrieval（向量检索）和 BM25（稀疏检索）的区别？如何混合使用？
- 什么是 Hybrid Search？如何融合两种检索的分数（RRF 等）？
- Reranker 的作用是什么？Cross-encoder 和 Bi-encoder 的区别？

### 工程细节
- 文档分块（chunking）策略有哪些？chunk size 如何选择？
- 如何处理长文档（超过 chunk 大小）的跨块语义？
- 向量数据库（Milvus、Qdrant、Pinecone、Weaviate）的选型考量？
- Embedding 模型如何选择？如何做领域适配？
- 如何处理向量库的在线更新（增量索引）？

### 质量优化
- RAG 的评估指标有哪些（RAGAS、Context Precision、Answer Faithfulness 等）？
- 检索不到相关内容时如何处理（fallback 策略）？
- Query 改写（HyDE、Step-back prompting）的原理？
- 如何减少 RAG 中的幻觉？
- GraphRAG 相比普通 RAG 的优势和适用场景？

---

## 8. Agent 开发

### Function Calling / Tool Use
- Function Calling 的工作原理？LLM 如何"执行"函数？
- JSON Schema 在工具定义中的作用？如何设计好的 tool description？
- 工具调用幻觉（hallucination）如何检测和缓解？
- 如何设计工具调用的重试和降级策略？
- Parallel Tool Calling 的实现与注意事项？

### Agent 架构
- ReAct（Reasoning + Acting）框架的原理？
- Plan-and-Execute 和 ReAct 的区别？各适合什么场景？
- Agent 的 Memory 系统如何设计（短期/长期/episodic/semantic）？
- 如何设计 Agent 的终止条件？防止无限循环？
- Tool Gateway（工具网关）在生产环境中的作用？

### Multi-Agent
- 多 Agent 系统的常见拓扑（中心化、去中心化、分层）？
- MCP（Model Context Protocol）和 A2A（Agent-to-Agent）协议是什么？
- Supervisor + Worker 模式如何实现？
- 多 Agent 之间如何传递上下文？如何避免上下文爆炸？
- 多 Agent 系统的冲突解决策略？

### 工程与生产
- 如何给 Agent 调用添加权限控制和安全沙箱？
- Agent 的可观测性（observability）如何实现？需要 trace 哪些信息？
- 如何评估 Agent 的效果？常用 benchmark（GAIA、AgentBench 等）？
- LangChain、LangGraph、AutoGen、CrewAI 的区别？各自的适用场景？
- 流式输出（streaming）在 Agent 中如何实现？断点续传怎么处理？

### Prompt Engineering
- System Prompt 的设计原则？
- Few-shot 和 Zero-shot 的选择时机？
- Chain-of-Thought（CoT）提示的原理？什么时候 CoT 会失效？
- 如何防止 Prompt Injection 攻击？
- 如何管理生产环境中的 Prompt 版本？

---

## 9. 多模态

### 视觉-语言模型
- CLIP 的预训练方式？对比学习在多模态中如何应用？
- LLaVA 的架构是什么？视觉特征如何接入 LLM？
- Q-Former（BLIP-2）如何桥接视觉编码器和 LLM？
- 多模态模型中图像分辨率和 patch size 对性能的影响？
- 如何处理多图或视频输入？

### 多模态 RAG
- 如何对图文混合文档做向量化和检索？
- 多模态 RAG 中图像内容如何表示（Caption、CLIP embedding、OCR）？

---

## 10. 系统设计

### LLM 推理服务设计
- 设计一个支持高并发的 LLM 推理服务，需要考虑哪些组件？
- 如何估算 LLM 推理服务的 QPS 上限和显存需求？
- KV Cache 的内存管理策略？如何处理显存 OOM？
- 如何实现请求调度（优先级队列、抢占式调度）？
- 如何设计灰度发布和 A/B 测试框架？

### RAG 系统设计
- 设计一个百万文档规模的企业知识库问答系统
- 如何保证检索结果的实时性（新文档秒级索引）？
- 如何处理多租户场景下的数据隔离？

### 推荐/搜索系统
- 召回和排序各自的职责？如何设计 Embedding 召回？
- 向量召回和协同过滤召回如何融合？
- 特征工程中如何处理用户行为序列？

---

## 11. 算法与编程题

### 高频数据结构
- 二叉树的各种遍历（递归与迭代）
- 链表：反转、检测环、合并有序链表
- 图：BFS/DFS、拓扑排序、最短路径
- 堆：TopK 问题、合并 K 个有序数组

### 高频算法
- 动态规划：背包、最长公共子序列、编辑距离
- 二分查找：边界条件处理
- 滑动窗口：最长无重复子串系列
- 回溯：全排列、组合、子集

### AI 相关编程题
- 手写 Attention 机制（numpy 实现）
- 手写 Softmax（数值稳定版本）
- 手写 K-Means
- 手写 Tokenizer 的 BPE 算法
- 手写 Mini RAG pipeline（分块、向量化、检索、生成）
- 实现一个简单的工具调用路由器（根据 intent 选择 tool）

---

## 12. 行为题与项目深挖

### 常见行为题
- 介绍你做过的最复杂的 AI 项目，遇到了什么技术挑战，如何解决的？
- 描述一次模型上线后效果不达预期，你是如何排查和优化的？
- 你如何在技术方案不确定的情况下推进项目？
- 如何平衡模型效果和工程成本？

### 项目深挖方向（面试官常问）
- 数据怎么来的？质量如何保证？
- 为什么选这个模型/框架，有没有对比过其他方案？
- 模型的离线指标和线上指标是否一致？不一致怎么处理？
- 训练用了多少资源，耗时多久？有没有做过优化？
- 如果重新做这个项目，你会改变什么？

---

## 各大厂侧重点

| 公司 | 重点方向 |
|------|---------|
| 字节跳动 | 算法题（LeetCode 高频）、LLM 推理平台工程、DeepSpeed/PyTorch 工程能力 |
| 阿里 | 分布式训练、RLHF/DPO 对齐、数据工程（去重/合成数据）、Qwen 相关技术栈 |
| 腾讯 | 在线服务化、低延迟部署、推荐搜索系统、Agent/RAG 产品化 |
| 百度 | 文心系列技术、飞桨框架、NLP 基础扎实 |
| 美团 | 推荐系统与 LLM 结合、搜索召回排序、系统设计 |
| 华为 | 多模态、CUDA/NPU Kernel 优化、硬件感知推理优化、分布式训练工具链 |

---

## 推荐复习顺序

**第一轮（打基础）**
1. ML 评估指标 + 优化器
2. Transformer 原理 + KV Cache
3. LoRA / PEFT 原理
4. RAG 基础架构
5. LeetCode 中等题 × 50

**第二轮（提升）**
1. 量化方法（PTQ/QAT/GPTQ/AWQ）
2. RLHF / DPO 完整流程
3. Agent 架构（ReAct / Function Calling / Multi-Agent）
4. 推理加速（Flash Attention / Speculative Decoding / vLLM）
5. 系统设计：LLM 推理服务 + RAG 系统

**第三轮（冲刺）**
1. 分布式训练（ZeRO / Tensor Parallelism）
2. 多模态（CLIP / LLaVA / Q-Former）
3. 手写代码题（Attention / Softmax / Mini RAG）
4. 整理 2-3 个项目的 STAR 模板
