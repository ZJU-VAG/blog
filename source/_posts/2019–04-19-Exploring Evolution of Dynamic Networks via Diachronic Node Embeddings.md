---
title: Exploring Evolution of Dynamic Networks via Diachronic Node Embeddings
tags: ["论文评述", "报告"]
date: 2019-04-19
author: 潘嘉铖
mathjax: true

---

论文：Exploring Evolution of Dynamic Networks via Diachronic Node Embeddings
作者：Jin Xu, Yubo Tao, Yuyu Yan, and Hai Lin
发表刊物/会议：TVCG 2018



文章提出了一种利用graph embedding的方法来探索动态图的方法。

一般而言，传统的动态图可视化方法可以分成三大类，基于动画的方法（animation），基于时间轴的方法（timeline），以及其他方法（如投影 projection）。基于动画的方法，往往会高亮相邻两帧之间的变化，但是当时间比较长的时候无法追踪变化；基于时间轴的方法，则将所有内容一起显示在同个视图中，但空间是个问题；基于投影的方法，把每一帧当做一个点，用投影的方法投影在一个视图中，但是很难展现图的结构的信息；

文章提出了一种同时展示结构属性和动态属性的可视分析方法。具体步骤如下：

![image-20190419093928524](http://jackie-image.oss-cn-hangzhou.aliyuncs.com/19-04-19/image-20190419093928524.png)

A生成动态图，B为动态图每一帧的每个节点生成embedding向量，C将这些embedding向量对齐到同一向量空间中，DEF利用embedding向量可以做的数据挖掘（节点分类，节点聚类，动态轨迹聚类），G可视交互分析；

文章的主要贡献有：

1. 提出了一种新的节点embedding的方法
2. 提出了两种基于节点embedding的动态图聚类方法
3. 一个可视分析交互系统



### 动态图的构建

首先，将动态图按照$\Delta t$的时间间隔，划分成多个时间片段，然后将$[t_i-\omega/2, t_i+\omega/2)$作为$t_i$时刻对应的动态图。

![image-20190419094742711](http://jackie-image.oss-cn-hangzhou.aliyuncs.com/19-04-19/image-20190419094742711.png)

### 节点embedding向量的生成

文章利用了skip-gram模型为单帧图的每一个节点生成embedding向量；

skip-gram模型可以理解为，当你输入一系列句子（sentences），以及包含这些句子中的词的语料库（corpus），skip-gram模型会为你预测语料库中的单词出现在某个指定的单词（word）附近的概率；这个过程中，会有一个重要的产物，叫做词向量，利用两个词向量的内积，我们就可以看到两个词在句子中共同出现的概率有多高；

skip-gram模型的目标函数，可以看做在最大化，同个句子中的相邻词汇的词向量的内积。

![image-20190419095824934](http://jackie-image.oss-cn-hangzhou.aliyuncs.com/19-04-19/image-20190419095824934.png)

文章同样利用了skip-gram模型，做了如下修改：

用节点（node）替代词（word），用路径（path）替代句子（sentence），用节点集合（nodes set）代替语料库（corpus），于是也可以产生节点向量。

值得注意的有：

1. path的生成，靠的是random walk，假如图是一个有权图（weighted），那么random walk也需要依赖边权重。并且，为了提高效率，文章使用了负采样。

2. skip-gram模型的目标函数的修改。这里不仅仅要使得同一路径上的节点出现概率高，还要使得不相邻的节点共同出现的概率低：

   ![image-20190419102118181](http://jackie-image.oss-cn-hangzhou.aliyuncs.com/19-04-19/image-20190419102118181.png)

3. 将上一帧产生的embedding向量，传入下一帧的skip-gram模型中，用以保持两帧之间的连续性：

   ![image-20190419124832137](http://jackie-image.oss-cn-hangzhou.aliyuncs.com/19-04-19/image-20190419124832137.png)

### embedding向量对齐

为了使得所有的embedding向量能够对齐到同一个向量空间中，方便比较和计算。所以这一步要对embedding向量进行正交变换，使得下面这个矩阵范数最小（也即差异最小）：
$$
\left\|M_{i} \Omega-M_{b}\right\|_{F}
$$
其中$M_i$表示第$i$帧的向量构成的矩阵（$n \times d$）；$\Omega$指的是正交变换矩阵；$M_b$指的是基准矩阵，也就是所有embedding向量都要对齐到这个基准矩阵上来；$\left\|*\right\|_{F}$则是Frobenius矩阵范数。

关于$M_b$的选取，有三种不同的方法：

1. 对齐到节点数最多的一帧（适合于变化较小的动态图）
2. 对齐到前一帧（因为两帧之间的变化不大，所以误差会较小，但是不断对齐的过程中，误差就会累计）
3. 将所有帧分成好几段，每一段都对齐到其中的某一帧（解决了上面的问题）

### 节点分类和聚类

1. 节点的分类：

   根据前后两帧之间节点embedding的变化，可以判断这个节点是dynamic（动态）还是stable（稳定）。

   当前后两帧的节点之间的欧氏距离（文中叫做evolution value）,大于阈值$\theta$时，则认为其为dynamic；

2. 节点聚类：

   可以用于揭示某一段时间内，稳定的社团结构。文章提出了稳定的概念，也就是大部分节点在这段时间内维持一个stable的状态。那么，在一段稳定时间内，将同一节点不同时间的所有向量求均值，就作为这段时间内该节点的向量。然后利用这些节点进行k-means聚类，即可得到不同的聚类（社团）。

3. 趋势聚类：

   如何对节点随时间变化的趋势进行聚类。两个节点随时间演化产生的两条轨迹，可以利用如下方法判断距离：

   ![image-20190419150937094](http://jackie-image.oss-cn-hangzhou.aliyuncs.com/19-04-19/image-20190419150937094.png)

   同一时刻，两个节点的向量求欧氏距离；所有时刻的所有欧氏距离的平均值，作为两条轨迹的距离。

   利用knn graph，就可以对这些轨迹进行聚类。

### 系统界面

![image-20190419151704779](http://jackie-image.oss-cn-hangzhou.aliyuncs.com/19-04-19/image-20190419151704779.png)

文章提出五个分析目标：

1. 整体网络的演化分析
2. 动态节点的演化分析
3. 动态社团的时序分析
4. 稳定社团的结构分析
5. 将分析与网络的整体进行关联

分析系统的视图与这五个目标对应：

#### 控制面板（A）

#### 统计视图（B）

对应目标1

横轴表示时间，纵轴表示网络的平均演变值（evolution value），用以刻画网络的整体趋势；其中的统计直方图分别用红、绿、紫分别表示动态节点数量，新出现节点数量和消失的节点数量。

#### 节点视图（D）

对应目标2

横轴表示时间，纵轴则表示节点的演变值从低到高。只展示动态的节点，并且用黄到红的颜色映射来表示节点的演变值。

#### 趋势视图（C）

对应目标3

横轴：时间；纵轴：利用PCA，将节点向量投影至1维，并用线连起来。可以看到很多不同的社团演化，其中比较特殊的有如下：

![image-20190419152305401](http://jackie-image.oss-cn-hangzhou.aliyuncs.com/19-04-19/image-20190419152305401.png)

#### 结构视图（E）

对应目标4

用PCA按照节点向量，投影至二维。

灰色表示稳定的节点，并且用大小来表示稳定的持续时间；动态节点则用了粉色-绿色的颜色映射来展示演变值。凸包围盒则用以概括不同的社团。

#### snapshot视图（F）

对应目标5

将以往探索过的结构记录在最右方。

