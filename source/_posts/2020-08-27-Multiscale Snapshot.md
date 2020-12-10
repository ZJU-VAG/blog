---
title: "Multiscale Snapshots: Visual Analysis of Temporal Summaries in Dynamic Graphs"
tags: ["论文评述", "报告"]
date: 2020-08-27
author: 卢金璇
mail: 11821132@zju.edu.cn
mathjax: true
---

论文：Multiscale Snapshots: Visual Analysis of Temporal Summaries in Dynamic Graphs

作者：Eren Cakmak, Udo Schlegel, Dominik Jackle, Daniel Keim, and Tobias Schreck

发表：IEEE transactions on visualization and computer graphics. TVCG,2020

Multiscale Snapshots 是一种半自动视觉分析方法提供了动态图中结构和时间变化的多尺度概览。 本文将时间层次抽象与无监督图学习方法结合起来，以识别相似的演化图。

## Background

动态图模型将随着时间改变实体之间的关系。会面临着有效的探索（需要找出合适的分析方法并以可读，可扩展和表达方式）。以前用于动态图数据的可视化分析通常结合时间抽象方法（例如，时间聚合和降维）来提供随时间推移的高层结构的概述. 但是他们缺乏用于在不同时间抽象尺度上进行动态过程的视觉分析（多尺度分析）的方法，这使分析人员面临艰巨的任务。即手动区分重叠的时间变化

本文提出了 Multiscale Snapshots，这是一种新颖的视觉分析系统，可半自动提供动态图的结构和时间变化的多尺度概览。结合时间层次抽象+无监督图学习方法，以识别相似的演化图。

#### Challenge

-   数据的复杂性和大小带来了许多挑战，因为许多动态图可视化技术无法扩展
-   在显示每个时间步长的详细图形结构与呈现随时间变化的属性之间进行权衡
-   创建动态图的紧凑的时间抽象（总结）是用户任务相关的，并且依赖于应用程序域以及数据属性

#### Contribution

-   多尺度 snapshot 方法以可视方式来分析多个时间尺度和结构相似性
-   使用无监督图学习方法的时间分层抽象，以减少动态图的大小并加快分析任务的速度

## Related Work

### 已有研究相关工作分成 3 类

**Dynamic Graph Analysis and Visualization：**以前做动态图分析和可视化，经常用的方法将动态图显示为动画，时间轴和混合可视化。 （但是这些方法他们不能同时缩放到大量节点，边和时间步长）。因此，提出了将自动分析方法与交互式可视化相结合的可视化分析方法，以减少显示的数据并突出显示结构变化。

![](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/8/30/b45eb7af4eb9042537a9d707cf0114868e49b631.png)

**Visual Analytics of Dynamic Graphs**：动态图的可视化分析是把图分析方法与可视化技术无缝集成，以交互方式分析不断发展的结构特性 ：经常用抽象方法

数据空间抽象（例如，采样，聚类）减少了图形元素或时间步的数量。

![](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/8/30/4682aa6c4febd80d80da35eb797c7b30ab11ef78.png)

像这篇 snapshot to point ：提出了一种视觉分析方法，可以将图的序列分段和聚合为向量，并应用降维方法来获得动态图中的状态概览，他的问题就是降维很难解释，因为投影无法直观显示不断变化的图形结构

视觉空间抽象（例如缩放，焦点和上下文）可减少呈现的数据量。许多以前提出的方法主要集中在聚合上，并以一个尺度显示抽象的时间或结构维度，这使得研究抽象方法对所得可视化的影响变得困难，因为可能会在不同的尺度和间隔下找到模式。

![](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/8/30/e1d266378c3827c2f5bc7bf481d52a9935140725.png)

**Multiscale Dynamic Graph Visualizations**：多尺度动态图可视化以前的方法都集中在特定时间尺度上的动态图分析上，并且需要手动定义参数。跟本文有点不一样，他们建议使用时间层次抽象与无监督学习方法结合，以探索输入参数（例如离散化规模）并同时可视化不同时间抽象层次上的图序列

![](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/8/30/9107fc5c251978be3a1638e8a65b7bf8c69c7974.png)

## 方法

### Multiscale Snapshot

![](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/8/30/190ee990cb3664944253663a047cef6f693c120a.png)

这个可视化系统提供了大规模动态图的更高级别和更细粒度的时间间隔的概述。 通过在交互式多尺度可视化中集成时间抽象和图形嵌入，该方法降低了数据的复杂性

系统主要分成 3 各部分

1.将时间维转换为 snapshot 层次结构，将动态图的子集汇总为重叠的多尺度间隔

2.再通过将不断发展的拓扑的嵌入向量表示中来降低 snapshot 的复杂性。

3.将抽象的时间数据转换为交互式分层可视化，并支持必要的交互以及导航方法，以可视方式分析不断变化的图结构

此外通过在一致的界面中组合动态图的不同可视化来增加任务覆盖范围

### \***\*Temporal Hierarchical Snapshots\*\***

这个方法有两个步骤

![](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/8/30/31a07372c7ae7fa2296fdf0bab7b0f025c9fc876.png)

1. 初始有 T 个静态图， 使用不同时间片生成并堆叠多个分区。我们按层次结构组织堆叠的分区，该层次结构对从粗糙到精细的时间表示形式的抽象（离散化）的不同级别进行排序。时间重叠的宽度是 2^(l-1), 层次结构的高度是 log T

一个单图形指标不可以捕获所有不断发展的图形结构。

2.抽象方法，本文使用设置操作（联合，交集，不交集图）将间隔默认转换为图抽象

结果是时间 snapshot 的层次结构，其中包含多个抽象图（例如，并集，相交和不相交图）。

通过将每个抽象映射到其向量表示，动态图的结果时间层次结构将在多尺度 snapshot 方法的下一步中使用。

### **Multiscale Dynamic Graph Index**

多尺度动态图指数，学习所得的分层 snapshot 并将其嵌入到低维空间中，以降低图形的复杂性并加快分析任务（例如，相似性搜索）。

![](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/8/30/7fd0ff070b92d19f1e0e18e01a4888e9b3491ff3.png)

把图形嵌入以将所有 snapshot 图（例如联合和不相交图）映射到向量表示。

本文应用的嵌入方法有 ： graph2vec ，GL2Vec 和 FGSD

然后用嵌入指数计算 knn 搜索查询，查询结构有 2 组：

间隔树，用于支持对间隔的有效时态查询，每个级别都有一个单独的索引结构

### **Multiscale Snapshots Visualization**

![](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/8/30/03bc44c58ec23ea4e017794b2b17da15fd69bf09.png)

应用可视化映射以多尺度可视化形式组织时间 snapshot，以对生成的 snapshot 进行可视化分析，并将图形嵌入用于分析任务。

最高级别（根）显示整个动态图（例如并集图）的聚合版本，最低级别使我们能够描绘每个时间步的有限数量。中间的级别允许在 snapshot 视图（并置的小倍数）中可视化所生成 snapshot 的子集。

snapshot 视图在一致的界面中结合了不同的视觉隐喻，以扩大任务覆盖范围并显示图之一（例如并集图）每个视图都使用户能够使用四种视觉隐喻（节点链接，邻接矩阵，动画以及图形指标的时间序列）。

显示空间有限，本文就设定了显示空间的数量。如果显示的总结图的大小超过特定阈值（超过 100 个节点）本文使用社区检测算法来减少节点的 snapshot 图视图

抽象的 snapshot 显示为紧凑的彩色矩形，没有任何视觉表示。可以将背景色映射到所选图的提取图度量，例如，节点数以及边数，平均聚类系数，密度和可传递性。

### **Multiscale Snapshots Prototype**

多尺度 snapshot 界面 包含了两个组件：“多尺度 snapshot”可视化和查询界面。

![](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/8/30/e1bcc6c6d845ba552cba4c57172a7f699be8cd40.png)

多尺度 snapshot 可视化：在时间维度上水平（时间）或垂直（对细节进行概述），每个 snapshot 视图都可以通过缩放，平移，笔刷和更改所有视图中的布局进行可视化分析。

![](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/8/30/b54da8e81f2cbe71beee0c2d248318151945404e.png)

查询界面：应用特定的 knn 查询在所有或特定级别的时间粒度上搜索相似的抽象图。。图里面显示不通时间分成的相似关系。

## 评估

1.演示如何利用视觉分析方法获得动态图中的时间抽象

本文用 Reddit 数据来做 case , reddit 是一个社交新闻聚合网站:界面的结果使用 Graph2Vec 嵌入方法计算了 80 个时期的动态图索引，并为每个 snapshot 生成了三个抽象图（联合图，交点图和不相交图）。A 显示的节点是 subreddits，边缘是带有正（蓝色）或负（红色）情感的 subredd 之间带有时间戳的超链接。该示例以 2016 年美国大选为例，说明了该方法如何允许在动态图中搜索相似的时间状态。分析人员发现，查询结果在第二级（2 小时周期）和第三级（4 小时周期）上是相似的嵌入，这意味着这些相当短的图序列由与超链接相似的超链接子集组成在选举周期间。在 D 中，显示了通过相似度搜索进行的视觉分析的结果，这是总统选举时间轴上的重要事件。这表明这些政治事件似乎也讨论了不同时期。不同的视觉隐喻使分析人员可以将事件置于较低的层次上，并置于整个时间范围内，例如，分析人员可以关联子丑闻之间的联系行为在政治丑闻之后如何下降

![](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/8/30/d3d7c7459a455093276ebe98528d2b1b48a75c3a.png)

2.使用合成数据集和真实数据集评估图嵌入的相似度（knn）搜索。

![](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/8/30/3ae5a58ec6fd57d2e7492d1222ec2bc0c2693d19.png)

在描述的数据集上使用了三种无监督的图学习方法。图嵌入仅在有考虑和不考虑多尺度时间建模的情况下应用。本文使用中位数作为嵌入的平均值，因为它们可能导致嵌入空间中的潜在失真。通过与真实历史新闻报道的地面事实进行比较，对检测到的发现进行验证。

## 总结

**不足：** 缺乏正式的比较研究将多尺度 snapshot 与其他视觉分析方法进行比较。如果跟图形编辑距离（GED）的计算方法相比，图形嵌入会牺牲信息的损失
