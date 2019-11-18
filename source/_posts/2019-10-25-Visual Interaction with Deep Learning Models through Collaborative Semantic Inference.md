---
title: "Visual Interaction with Deep Learning Models through Collaborative Semantic Inference"
tags: ["论文评述", "报告"]
date: 2019-10-25
author: 卢家品
mathjax: true
---

论文: Visual Interaction with Deep Learning Models through Collaborative Semantic Inference

作者:  Sebastian Gehrmann*, Hendrik Strobelt*, Robert Kruger, Hanspeter Pfister, Alexander M. Rush

发表会议/期刊: VAST 2019

## 简介

人失去决策过程的主导能力时，任务的自动执行会导致严重的后果。深度学习模型则尤其可疑，因为最近的黑盒方法缺乏可解释的推理过程。本文主张视觉接口和深度学习系统的模型结构需要同时考虑进（方法的）交互设计中。为了共同设计（深度学习）模型与交互以使人与算法可视地合作，本文提出了一个协同语义推理（Collaborative Semantic Inference, CSI）的框架。该方法展示出了模型的中间推理过程。该过程能够让用户与问题的视觉标志（metaphors）做语义交互。这意味着用户可以同时理解和控制模型的部分推理过程。本文通过一个共同设计的文档摘要系统的案例研究来证明CSI的可行性。

### 动机

1. 深度学习逐渐变成一个通用的工具
2. 深度模型是复杂的黑盒模型，强制信任
3. 多个学课的专家提出这些模型作为团队的一个部分，协作

### 想法

1. 提出了一个框架——Collaborative Semantic Inference，能让用户控制模型的预测过程
2. 该过程需要揭露模型的内部推理过程，要符合人对问题的心理模型
3. 通过可视分析专家，交互设计专家，机器学习专家的紧密合作来完成整体框架的设计

### 本文贡献

1. 提出将hook机制整合进模型中来解释（理解）模型的推理过程
2. 在概念上拓展了人与模型的协作机制，拓宽了可视化与交互的设计空间
3. 设计了一个用于概括文档的Case case来证明本文提出的理念

## 相关工作

本文将深度学习模型的理解及可视化相关的研究分成三个等级：Passive Observation, Interactive Observation, Interactive Collaboration.

#### Passive Observation

![1573978733481](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/11/18/197ca68aca7f3f3782858c81b5e71ac66a1efc38.png)

1. 模型理解（Model-Understanding）——可视化结果，如Loss 函数

   ![1573978709512](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/11/18/59d8698a47764d585dd726d176fae7d381bbf432.png)

2. 决策理解（Decision-Understanding）——可视化输入对结果的影响

   ![1573978720244](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/11/18/284c9904d33fc74002161899da361acf0f265d0b.png)

### Interactive Observation

![1573978813534](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/11/18/f7bc758e6c57fd9ed2c87d30665842ef553b10b8.png)

1. 模型理解（Model-Understanding）——可视化模型内部各层激活情况

![1573978804207](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/11/18/a1ef7dd22f5643e1e7a2aafecb803e2bdafe2b0d.png)

2. 决策理解（Decision-Understanding）——理解模型内部激活的过程

![1573978882580](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/11/18/7f0a12a4839395b148c7fc68af6ad583e70a30f0.png)

### Interactive Collaboration

![1573978968870](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/11/18/ab518c18c3452ab0126dd09b342314ef2e3e1d12.png)

1. 模型形成（Model-Shaping）——通过调整训练数据，改变训练的模型。

   ![1573978960742](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/11/18/90a647cb9e03c727a998b380f730cb11ec9ac9ea.png)

2. 决策形成（Decision-Shaping）——本文方法。其它方法均无法协作地。

## Method

本文提出的核心方法比较简单，即Hook机制。类似于火车的闸门，引入中间节点，即Hook。每个输入必须先生成Hook，再输出结果。而Hook是有语义的，因而知道了Hook的激活情况就可以理解模型内部的推理过程。Hook机制由可视分析专家，交互设计专家，机器学习专家的合作设计出来。通过Hook是否被激活，可以预测模型的每个输入对最终结果是否有贡献，有何种贡献。

本文说明了有效的Hook节点设计比较困难，而本文属于开创性工作，因而对于每一个输入只设计了单hook节点，语义为是否使用该输入。

本文设计的Hook机制可形象地理解为火车的闸门，Hook是否被激活就意味着火车的闸门是否被打开。

![1573979734521](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/11/18/54cd90751f1579b70df3c2633737f08793825794.png)

通过将hook的输出加入条件概率来预测模型的输出

![1573979922780](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/11/18/0a367dce8126b9bbb582cdfe760abd67b769d829.png)

结果上：

1. 准确度略微降低
2. 可解释性极大增强
3. 是人可干预模型的结果输出过程

## Case study

#### 未引入本文方法前：

1. 无法理解结果与文档内部词汇之间的对应关系

2. 无法可视化编辑后的结果与输入之间的关系（我觉得可以用Attention机制可视化出来）
3. 无法调整结果

#### 系统界面：

![1573980068112](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/11/18/98506a07ab859cd9dfa244a9fe0b524ed89c991f.png)

#### 系统的迭代设计：

本文前文提到“该方法需要可视分析专家，交互设计专家，机器学习专家的紧密合作”。因为该Case系统的需要迭代的设计过程（所谓迭代，无非就是刚开始需求不清晰所采取的迫不得已的方法），如下：

![1573980225785](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/11/18/1f10153c32428153041fef922b447a082da7ff2c.png)

## 结论

#### 优点：

1. 提出了Hook机制，提供了可控的机器学习模型推理过程;

2. 选择的切入点合适，文档而不是其它更复杂的案列，降低了响应时间、Hook设计的要求;
3. 相比与自动生成的结果，用户可与模型进行协作，增加了结果的可信度;
4. 提出的交互符方法合用户对问题的理解过程 ，不突兀。而非可视化神经网络模型的参数;
5. 极大地扩充了深度学习模型的可视化设计、交互空间。				

#### 缺点：

1. 缺乏对结果的系统评估，比如没有做调查问卷，没有做user study，仅仅做了case study;
2. 不适用于大数据的推理，如文档分类;
3. 设计更多的Hook会带来模型和交互复杂度的提升，使得Hook机制能解决的机器学习结果干预问题有限。

### PPT

