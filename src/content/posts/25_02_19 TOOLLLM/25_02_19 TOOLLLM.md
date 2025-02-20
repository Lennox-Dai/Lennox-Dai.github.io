---
title: 25_02_19/TOOLLLM
published: 2025-02-19
description: 'TOOLLLM: FACILITATING LARGE LANGUAGE MODELS TO MASTER 16000+ REAL-WORLD APIS'
image: 'img/head.png'
tags: ['Multiagent LLM']
category: 每日阅读
draft: false 
---

# TOOLLLM: FACILITATING LARGE LANGUAGE MODELS TO MASTER 16000+ REAL-WORLD APIS



### 一句话概括

> [!IMPORTANT]
>
> 目前的开源大语言模型并没有很好的外部工具使用能力，这篇文章通过提出相应的Benchmark（**ToolBench**）、Algorithm（**DFSDT**）、评估方法（**ToolEval**）来增强这方面的工作，并在LLaMA基础上训练了新的ToolLLaMA模型，在api和外部工具调用上达到了和ChatGPT差不多的效果



### 文章思路流程

1. #### 待解决问题：

   > 开源模型和close source模型在外部api调用上有gap

2. #### 先前方法问题

   - **limited APIs**：只在很小一部分api上做了工作
   - **constrained scenario**：用户不会指定用哪个api，常见情况下会有很复杂的多轮api调用
   - **inferior planning and reasoning**：现在用CoT和ReACT的比较多，但是这俩方法并不能完全解放模型效能

3. #### 解决方法

   ![head](../conten/posts/25_02_19 TOOLLLM/img/head.png)

   - [ ] 从RapidAPI拿api
   - [ ] 丢给GPT生成调用的指令，整理成**ToolBench**
   - [ ] 把整理完的数据集喂给LLaMA做SFT，得到T**oolLLaMA**

4. #### 方法优势

   ![compare](../content/posts/25_02_19 TOOLLLM/img/compare.png)
   
   ![compare](content/posts/25_02_19 TOOLLLM/img/compare.png)
   
   ![compare](posts/25_02_19 TOOLLLM/img/compare.png)
   
   ![compare](../content/posts/25_02_19%20TOOLLLM/img/compare.png)



### 文章贡献细则

1. #### ToolBench

   > API collection --> instruction generation --> solution path annotation 

   - 这里让gpt生成调用这组api的instruction，以及和这些api相关的其他api
   - api set不是随便选的，用了api库中的hierarchy信息

2. #### ToolEval

   - **pass rate**：有限资源能不能出结果

   - **win rate**：两者相比效果哪个好

3. #### Depth First Search-based Decision Tree

   ![DFSDT](../content/posts/25_02_19 TOOLLLM/img/DFSDT.png)

   > *CoT和ReACT的问题：*
   >
   > 1. error propagation
   > 2. limited exploration

   **把前面的节点当作prompt，用DFS的方法让agent不断寻找或者放弃节点。**



### 实验结果

![exp](../content/posts/25_02_19 TOOLLLM/img/exp.png)
