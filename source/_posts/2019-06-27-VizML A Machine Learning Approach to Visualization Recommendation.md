---
title: "VizML: A Machine Learning Approach to Visualization Recommendation"
tags: ["论文评述", "报告"]
date: 2019-07-08
author: 陆俊华
mail: akiori@zju.edu.cn
mathjax: true
---

# VizML: A Machine Learning Approach to Visualization Recommendation

本文发表于 CHI 2019. 作者来自 MIT Media Lab 和 MIT CSAIL.

## 简介与背景

很多可视化工具学习曲线很陡, 往往需要人为指定: 如写代码或各种点击.

![1561879652903](http://www.cad.zju.edu.cn/home/vagblog/images/20190708/1561879652903.png)

然而, 在初步的数据探索以及创建基本可视化的时候, 往往探索的**速度**与**广度**比人为指定的定制性更重要. 可视化系统可以利用“数据集的性质会影响它被如何可视化”来支持这些基本需求.

现有的可视化推荐系统分为两类: 基于**规则**的与基于**机器学习**的. 前者一般是根据专家经验或实验得到的可视化准则; 后者则是直接学习从数据到可视化的模型. 本文属于后者. 本文将可视化定义为一个做可视化选择(**making design choice**)的过程, 这个过程让人来做是耗时耗力的. 为了减少人的工作量, 一个常用办法就是推荐, 具体来说是机器学习模拟逼近来模拟人做最优选择的过程.

在可视化中, 可视化编码包含了标记 marks (如点、线、矩形) 与通道 channels/retinal properties (如位置、长度、颜色等). 而创建可视化就是结合数据选择这些标记、通道的过程. 下图是一个简单的例子.

![1561881383307](http://www.cad.zju.edu.cn/home/vagblog/images/20190708/1561881383307.png)

如果用形式化的定义就是, 给定数据集$d$ , 一系列内在关联的设计选择$C=\{c\}$以及上下文信息$T$(美观性、任务、领域、受众). 人进行可视化设计的目标就是$C_{max} = \arg\max_CEff(C~|~d, T) $. 我们可以用神经网络来逼近它.

本文与近期其他一些基于机器学习方法区别在于以下三点:

-   学习的任务

    -   DeepEye 学习分类与排序可视化、Data2Vis 学习端到端生成模型、Draco-Learn 学习软限制
    -   本文学习的是**设计选择**

-   数据量

    -   比 DeepEye 和 Data2Vis 多了几个数量级
    -   能表征数据集的更多方面、并支持深度网络

-   数据质量
    -   数据集在形状、结构、分布上十分**多元化**
    -   基于真实的用户对自己数据可视分析的结果

## 方法概览

本文从*Plotly community feed*上爬取了大量数据集与对应的可视化作品.

![1561881498089](http://www.cad.zju.edu.cn/home/vagblog/images/20190708/1561881498089.png)

### 数据准备

主要分为模型**输入**和**输出**两方面的准备.

输入数据是被可视化的数据集的特征, 具体分为单维度、双维度以及数据集整体层面的特征. 经过处理后一共有 841 个标量值组成特征. 下图做了简单的示意.

![1561881837006](http://www.cad.zju.edu.cn/home/vagblog/images/20190708/1561881837006.png)

输出数据当然是可视化设计选择, 他也是可以被量化的. 下图简单示意了这个抽取过程, 分为可视编码层面的选择和可视化层面的选择.

![1561881999729](http://www.cad.zju.edu.cn/home/vagblog/images/20190708/1561881999729.png)

我们训练模型的预测任务就是基于可视化设计选择的预测任务, 分为可视化层面的预测任务和可视编码层面的预测任务.

![1561882104280](http://www.cad.zju.edu.cn/home/vagblog/images/20190708/1561882104280.png)

![1561882111144](http://www.cad.zju.edu.cn/home/vagblog/images/20190708/1561882111144.png)

### 神经网络与基线模型

-   全连接前向神经网络模型
    -   三个隐藏层, 每层 1000 个神经元、ReLU 激活函数
-   Naïve Bayes、_k_-nearest neighbors、logistic 回归和随机森林 (Random Forest)

实验结果表明, 神经网络模型几乎全方位碾压其余模型

## 模型评估

### 特征重要性解读

-   本文抽取了大量特征, 有些是前人用过的、有些是本方法才使用的, 那么:

    -   这些特征重要性如何?
    -   是否和一些（经验性的）规则一致?
    -   是否一些先前没用过的特征也很重要?

-   利用 Random Forest 模型的 MDI 指标来发现不同任务最重要的特征

    -   出于可解释性与稳定性的考虑

-   确实发现了许多和前人研究的感知相关的准则或者经验比较一致的特征

    -   统计性的特征（多是通过**聚合**步骤生成的）很重要, 但是已有方法用的不多
    -   例如偏态、峰态、熵等高阶性质

-   有序性（没有人用过）

    -   排序性（原数据和排序后数据的相关系数）
    -   单调性

-   数据变化的尺度是线性还是对数（没有人用过）

-   结论:
    -   基于规则的推荐系统需要更多的数据特征作为规则;
    -   任务特定的特征排序、非线性的依赖关系使得基于规则的系统更难跨任务跨领域使用 → 更需要基于 ML 的方法

### 结合众包打分对模型**Benchmarking**

对于 effectiveness:

-   在前面训练模型时, 默认 Plotly 用户上传的就是 effective 的. → 本文处理时认为 effectiveness 是二元的

-   但以往研究表明他是连续值; 以往研究还发现同一个数据及可能有多种同等 effective 的可视化方式 → 连续且要能反应可视化的不明确性

-   同样预测任务，进行众包打分. 该打分最后用于比较人对设计选择与机器学习算法选择的性能.

    ![1561882778566](http://www.cad.zju.edu.cn/home/vagblog/images/20190708/1561882778566.png)

## 讨论

-   不足

    -   数据偏向于 Plotly 这个平台本身
    -   不管是众包用户还是 Plotly 作者都不是真专家
    -   只关注了可视化推荐的一部分任务

-   未来工作
    -   更全面的数据收集 → 减少 bias、更完整去度量 task 相关的 effectiveness
    -   收集客观的 effectiveness 度量
    -   用 representation learning 学习特征而不是手动去挑选

## 题外话

本文项目代码以及数据集地址: https://github.com/mitmedialab/vizml

本文作者以及其他一些大佬在今年 CHI 上同一个 panel 下还有一篇文章收集了大量可视化研究中的数据集、期望用于可视化研究的 benchmark 问题 **VizNet: Towards A Large-Scale Visualization Learning and Benchmarking Repository**
