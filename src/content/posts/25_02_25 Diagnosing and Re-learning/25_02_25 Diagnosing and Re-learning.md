---
title: 25_02_25/Diagnosing and Re-learning
published: 2025-02-25
description: 'Diagnosing and Re-learning for Balanced Multimodal Learning'
image: 'img/head.png'
tags: ['imbalanced multimodal learning']
category: 每日阅读
draft: false 
---

# Diagnosing and Re-learning for Balanced Multimodal Learning



### 一句话概括

> [!IMPORTANT]
>
> 通过分别在训练数据集和测试数据集上运用聚类方法来判别不同encoder的训练状态，并通过重新初始化其中的部分参数来保持不同模态的训练平衡。



### 文章思路流程

1. #### 待解决问题：

   > 不同的模态会以不同的速度converge，这会导致训练端到端的多模态模型时会有一些模态并没有被完全训练，造成模型能力下降。

2. #### 先前方法

   ![prev](./img/prev.png)

   - **Gradient Blending**

   - **Distilling**

   - **OGM**（此文章解析详见“25_02_24 OGM”文章中的解析）

   > 但是这些方法都会在一定程度上损失某一较强模态的能力

3. #### 解决方法

   - *Preliminary*

     > Recent studies suggest that re-initializing the network parameters during training can effectively improve model performance and parameter utilization

   - *总体流程*

   ![head](./img/head.png)

   1. 先将不同模态的encoding对样本进行操作，记录结果：
      $$
      \phi_i^k=\theta_k(x_i^k)
      $$

      $$
      \phi_D^k=\{\phi_1^k,\phi_2^k,\dots,\phi_{N_{D}}^k\}
      $$

      

   2. 对每一个模态的训练集和测试集${\phi}$分别做聚类，计算purity，然后拿到两者之差，来代表这个模态的学习程度
      $$
      g^k=|P_D^k-P_V^k|
      $$

   3. 根据这个量化的学习程度，来动态的遗忘encoding内容（重新initialize）
      $$
      \alpha_k = \tanh(\lambda \cdot g^k)
      $$

      $$
      \theta_k = (1 - \alpha_k) \cdot \theta_k^{\text{current}} + \alpha_k \cdot \theta_k^{\text{init}}
      $$

      

4. #### 方法亮点

   - [ ] 将工作从之前的双模态推广到了n模态

   - [ ] 不会损失较优的模态的encoding能力（实验结果上看来是这样的，但是数学推导上存疑）
   - [ ] 理论上可以增强模型的泛化能力



### 实验结果

![exp](./img/exp.png)



### 思考

1. #### 
