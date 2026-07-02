# 机器学习与深度学习知识分享

面向有一定编程基础的程序员，了解 Python，但不一定有 ML/DL 背景。  
每章先讲清楚核心概念与直觉，再配合 Python 代码示例加深理解。

📖 **在线阅读：[taosha121.github.io/ml_dl_notes](https://taosha121.github.io/ml_dl_notes)**

## 环境准备

### 第一步：安装 Python 3.11

推荐使用 **Python 3.11**（稳定性最佳，主流 ML 库已全面适配）。

通过 **Homebrew** 安装（macOS 推荐方式）：

```bash
brew install python@3.11
python3.11 --version   # 确认 3.11 已安装
```

### 第二步：创建虚拟环境

在项目目录下创建独立的 Python 环境，避免包版本冲突：

```bash
# 创建虚拟环境（固定 Python 3.11）
python3.11 -m venv .venv

# 激活（macOS / Linux）
source .venv/bin/activate

# 激活后确认版本
python --version    # 应输出 Python 3.11.x
```

> 如果使用 **Miniconda**，等效命令为：
> ```bash
> conda create -n ml_dl python=3.11
> conda activate ml_dl
> ```

### 第三步：安装依赖

```bash
pip install -r requirements.txt
```

> **注意**：`torch`、`transformers` 等大包合计约 3-5 GB，首次安装耗时较长。如只需运行第一部分（数学基础），可先只装轻量依赖：
> ```bash
> pip install numpy pandas scipy matplotlib seaborn scikit-learn jupyter
> ```

### 第四步：下载预训练模型（第二部分需要）

第二部分聚类算法用到 `text2vec-base-chinese`（768 维中文语义向量模型，约 400 MB）。模型通过 **ModelScope（魔搭社区）** 下载，无需注册，国内网络直接访问：

```python
from modelscope import snapshot_download
snapshot_download('Jerry0/text2vec-base-chinese')
```

> 也可以在 Notebook 中直接运行上面两行，首次执行时自动下载并缓存到本地，后续运行直接复用缓存。

### 第五步：注册 Jupyter kernel

```bash
python -m ipykernel install --user --name ml_dl --display-name "Python 3.11 (ml_dl)"
```

---

## 目录

### 第一部分：数学基础 → `ch1_math_foundations.ipynb`

- 1.1 线性代数 — 向量、矩阵运算、特征值分解、SVD
- 1.2 概率与统计 — 贝叶斯定理、常见分布、最大似然估计
- 1.3 微积分与优化 — 偏导数、梯度、链式法则、凸优化基础

### 第二部分：机器学习基础

**`ch2.1_overview.ipynb` — 概述与预处理**
- 2.1 机器学习概述 — 问题类型、学习范式、基本流程
- 2.2 数据预处理 — 缺失值处理、特征缩放、编码（LabelEncoder / OrdinalEncoder / OneHotEncoder）

**`ch2.2_unsupervised.ipynb` — 无监督学习**
- 2.3 降维 — PCA 原理、SVD vs PCA
- 2.4 聚类算法 — K-Means、DBSCAN

**`ch2.3_supervised.ipynb` — 监督学习**
- 2.5 线性模型 — 线性回归（单输出/多输出）、多项式回归、逻辑回归
- 2.6 树模型与集成学习 — 决策树（ID3/C4.5/CART）、随机森林、AdaBoost、GBDT
- 2.7 K 近邻（KNN） — 懒惰学习、K 值选择、距离度量、维度诅咒
- 2.8 支持向量机 — 核函数、支持向量、间隔最大化
- 2.9 模型评估 — 混淆矩阵、Accuracy/Precision/Recall/F1/ROC-AUC、MAE/RMSE/R²

### 第三部分：深度学习基础

**`ch3.1_nn_basics.ipynb` — 神经网络基础与训练**
- 3.1 神经网络基础 — 感知机、多层网络、激活函数
- 3.2 训练原理 — 前向传播、反向传播、梯度下降变体（SGD/Adam）
- 3.3 正则化与调参 — Dropout、BatchNorm、学习率调度、早停

**`ch3.2_cnn.ipynb` — 卷积神经网络（CNN）**
- 3.4 卷积神经网络 — 卷积层、池化、经典架构（LeNet → VGG → ResNet）、CIFAR-10 实战

**`ch3.3_rnn.ipynb` — 循环神经网络（RNN）**
- 3.5 循环神经网络 — 序列建模、梯度消失、LSTM/GRU、时序预测与情感分类实战

### 分享会材料

**`sharingsession_cart.ipynb` — CART 决策树**
- 决策树结构、Gini 不纯度、分裂准则对比（ID3/C4.5/CART）、剪枝演示

**`sharingsession_sentiment.ipynb` — 情感分析**
- 词袋模型的局限、Word Embedding 原理、LSTM 情感分类实战（IMDb 数据集）

---

> **计划中（尚未完成）**
>
> - 第四部分：现代深度学习 — Transformer、预训练模型（BERT/ViT）、生成模型（VAE/GAN/Diffusion）、LLM 简介
> - 第五部分：实践项目 — PyTorch 入门、图像分类、文本情感分类（Transformer 微调）、时序预测
