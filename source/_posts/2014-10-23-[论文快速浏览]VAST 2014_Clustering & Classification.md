---
title: "[论文快速浏览]VAST 2014: Clustering & Classification"
tags: ["论文评述"]
date: 2014-10-23
author: 吴斐然
mathjax: false
---

文章列表：

1. 《A Five-Level Design Framework for Bicluster Visualizations》

2. 《Cupid: Cluster-Based Exploration of Geometry Generators with Parallel Coordinates and Radial Trees》

3. 《VarifocalReader — In-Depth Visual Analysis of Large Text Documents》

4. 《Visual Methods for Analyzing Probabilistic Classification Data》

---

## 《A Five-Level Design Framework for Bicluster Visualizations》

本文是为对 bicluster 这一常用的数据组织结构以及可视化形式的一篇 survey。当前对于 bicluster 可视化的设计没有一个系统化的设计守则，本文针对 bicluster 可视化总结了 5 层设计框架，调查了相关的最新设计方案和方法。

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/10/tu1.jpg)

<center>图1 bicluster数据组织</center>

bicluster 可视化的五层框架分别为 Entity Level、Group Level、Bicluster Level、Chain Level 以及 Schema Level，其区别如下表，通过 bicluster 中对应的对象不同加以区分。

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/10/biao1.jpg)

<center>表一</center>
对于不同的层次，本文给出了不同的可视化建议，如Entity Level和Group Level的关系较为简单，可以选择node-link。如果边、节点数量多，关系复杂，容易造成视觉混乱，可以采用边聚合、边绑定、选择高亮等手段。

但是对于 Bicluster Level 这样关系更为繁杂的层次，应该选择基于矩阵的方法，但是基于矩阵的方法在可视化较为简单层次的关系式较不直观。另外一个可以采用的选择是平行坐标。

对于 Chain Level 可以采用以上各种手段结合的方式，如下图所示。

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/10/tu2.jpg)

<center>图2 Chain Level的可视化表达。左：基于矩阵的表达和node-link结合；右：基于矩阵的表达和平行坐标结合</center>

Schema Level 由于其表现的关系数量不会多，可以参考 Group Level 等的设计方式。

下表为本文结论的浓缩。

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/10/biao2.jpg)

<center>表二</center>

---

## 《Cupid: Cluster-Based Exploration of Geometry Generators with Parallel Coordinates and Radial Trees》

在 Geometry generators 生成 mesh 的过程中，参数的调整会生成许多相似或者不想要的形状。本文要解决的问题是找到相似的生成形状和相关参数设定、找到错误和非真实的形状以及确定参数对结果的影响。作者用一个合成的可视化系统将参数空间和 3D 形状生成结果结合起来，采用层次聚类、表述性的平行坐标和放射状的树形结构，使用户通过放缩来选取相似的 3D 形状，最后用一个杯子的生成结果来评价方法，并得到专家的反馈。

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/10/tu3.jpg)

<center>图3 系统流程图</center>

首先本文对参数进行采样，生成相应的数据，再将结果配准并进行层次聚类。

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/10/tu4.jpg)

<center>图 4</center>

上图为作者设计的可视化界面，右侧为呈放射状布局的层次聚类结果，左侧的平行坐标标示了参数分布和生成结果之间的联系，颜色编码了层次聚类中的顶层聚类。以这两个可视化视图为核心，作者设计了一系列交互方式对结果进行选取和修改，最终评估了参数对生成模型的影响。

---

## 《VarifocalReader — In-Depth Visual Analysis of Large Text Documents》

本文是一篇致力于文本视觉抽象并可视化表达的论文，作者设计了名为 VarifocalReader 可视化工具帮助用户提取感兴趣的文本知识，以达到结合语义算法进行交互式的可视分析之目的。

首先作者对输入的一部书，进行多层可视化和浏览，这之前需要对整部书的文本进行自动分析。如主题分割，估计出文本的哪一段属于一个主题，主要主题的变化；词云的计算能够提取出文本段落中的关键词，作为用户深入分析的起点；此外该系统还采用了基于主动学习的自动标注方法等等。

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/10/tu5.jpg)

<center>图5</center>

上图为系统的概览，从左自右以章节、段落的层次结构依次展开，色块标识了用户选到的关键词在各个段落章节的分布，柱形图用相同的颜色编码方案对这些分布的统计信息予以了可视化。

---

## 《Visual Methods for Analyzing Probabilistic Classification Data》

本文致力于用交互式的可视化手段对分类结果进行分析，改进分类器，是一篇利用可视分析技术和理念对机器学习的经典方法进行改良的论文。文章涉及到了不少机器学习领域专业的概念，如在对分类结果进行表达的时候，编码了假阳、假阴等指标，综合地对分类结果进行了可视化，评估分类结果的可靠性和有效性。

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/10/tu6.jpg)

<center>图6</center>

上图为作者对左侧所示的分类结果重新用右侧专门设计的可视化编码方案进行可视化的结果。

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/10/tu7.jpg)

<center>图7</center>

系统概览如上图所示，除了左侧比较常规地利用直方图可视化了分类的统计信息以外，通过和中央主要可视化视图的交互，用户得以观察分类结果和预期结果的差别。右侧视图用盒须图的方式可以观察到原数据的特征对每一个分类的影响。
