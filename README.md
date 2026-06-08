# 机器学习与深度学习知识分享

面向有一定编程基础的程序员，了解 Python，但不一定有 ML/DL 背景。  
每章先讲清楚核心概念与直觉，再配合 Python 代码示例加深理解。

📖 **在线阅读：[taosha121.github.io/ml_dl_notes](https://taosha121.github.io/ml_dl_notes)**

## 环境准备

```bash
pip install -r requirements.txt
python -m ipykernel install --user --name ml_dl --display-name "Python (ml_dl)"
```

详见各 notebook 开头的「环境准备」小节。

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

### 第四部分：现代深度学习 → `part4_modern_dl.ipynb`

- 4.1 Transformer 与注意力机制 — Self-Attention、位置编码、Encoder-Decoder
- 4.2 预训练与迁移学习 — BERT、ViT、Fine-tuning 范式
- 4.3 生成模型概览 — VAE、GAN、Diffusion Models（概念介绍）
- 4.4 大语言模型简介 — GPT 架构、Scaling Law、提示工程（概念介绍）

### 第五部分：实践 → `part5_practice.ipynb`

- 5.1 PyTorch 入门 — Tensor、Dataset/DataLoader、训练循环
- 5.2 实战项目一：图像分类（CNN + CIFAR-10）
- 5.3 实战项目二：文本情感分类（Transformer 微调）
- 5.4 实战项目三：时序预测（LSTM）
