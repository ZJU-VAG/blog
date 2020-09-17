---
title: "egoSlider: Visual Analysis of Egocentric Network Evolution"
tags: ["论文评述"]
date: 2015-11-11
author: 陆俊华
mail: akiori@zju.edu.cn
mathjax: true
---

论文: egoSlider: Visual Analysis of Egocentric Network Evolution

作者: Yanhong Wu, Naveen Pitipornvivat, Jian Zhao, Sixiao Yang, Guowei Huang, and Huamin Qu

发表会议: VAST2015

## 简介

文章围绕 ego-network 的可视化展开. ego-network 是社会网络分析研究中一个重要的研究对象, 它由 ego(中心人物)和 alters(与 ego 相连的人)组成. 研究 ego-network 随着时间演化的模式在不同领域(社会学, 人类学等)都是很重要的课题, 也是具有挑战性的问题, 因其具有复杂的时变的图结构.

<div align="center">简单的带tag的ego-network</div>

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/11/%E5%9B%BE%E7%89%872.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/11/图片2.png)

在与专家讨论后, 文章从三个层次(macroscopic, mesoscopic, microscopic)来设定分析的问题(任务). 先前相关文献都没有从多层次的分析, 因而本文在这方面是考虑十分完善的.

macro:

1. 在每个时间段, 一大群人的 ego-networks 有怎样的 pattern?
2. 一大群人的 ego-networks 的演化趋势是怎样的?

meso:

3. 多人的 ego-networks 大体相似性?
4. 在特定时间点, 多人的 ego-networks 之间的区别?.

micro:

    5.   一个ego的1阶和2阶alters数目随时间的变化?

6.  ego 和它 alters 之间边强度随时间的变化?
7.  alters 和一个 ego 之间如何连接的?
8.  关系是如何生成的?

依照这些, 作者设计了一个系统 egoSlider, 三个视图 Data Overview, Summary Timeline View, Alter Timeline View 分别对应上面的 macro, meso, micro.

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/11/%E5%9B%BE%E7%89%871.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/11/图片1.png)

## 工作流程

### 系统界面

左边 macro 右上 meso, 单击一个人则出现 micro. 作者设计了展示关键信息的 glyph 来编码其中的特征. 左边用到了一些图相似性的定义与 MDS; 别的多为统计信息的展示以及简单的聚类. 提供了大量交互操作, 可以对不同时间段进行对比, 可以按照不同的分类目标用不同的颜色进行分类等等, 比较完备.

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/11/%E5%9B%BE%E7%89%8721.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/11/图片21.png)

### Evaluation

文章的 Evaluation 分为两部分, 一是应用场景, 即 dblp 中图形学, 可视化相关领域的专家的一个 ego-network 的分析, 从系统中得到大量问题并在实际生活中找到例子得以验证. 二是用户调研, 体现其系统的高效性.

作者没有具体的夸奖自己, 倒是提了一些缺点, 比如 MDS 导致上下图的点不一致性, 比如使用该系统还需要一定的不小的学习成本, 比如有些组件还是具有一些迷惑性. 从我的角度看, 这篇文章写的比较完备(分析的多层次多角度), 然后系统的美观性强, 紧扣分析任务. 对于 ego-network 的展示和简单的分析到位.
