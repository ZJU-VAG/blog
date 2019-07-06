---
title: "Refinery: Visual Exploration of Large, Heterogeneous Networks through Associative Browsing"
tags: ["论文评述"]
date: 2015-11-13
author: 郭方舟
mathjax: true
---

论文：Refinery: Visual Exploration of Large, Heterogeneous Networks through Associative Browsing

作者：S. Kairam , N. H. Riche , S. Drucker , R. Fernandez2 , and J. Heer

发表会议：EuroVis 2105

这篇文章提出了一种基于关联浏览的大规模异构网络可视探索的技术。浏览策略是电子书合集导航中的常用策略。关联浏览则是指以收集特定主题或是一般性知识为目的，按照环境线索不断迭代，最终完成探索目标的浏览过程。

作者首先提出了 4 个支持关联浏览的准则：

G1. 支持对异构动态集合的浏览。

G2. 在表达搜索意图时，平衡简洁性和表达性。

G3. 通过连续迭代的过程优化用户的搜索意图。

G4. 提供多种上下文线索以支持用户识别数据，发现规律。 文章在介绍系统时使用一个背景故事将系统中的所有视图串联起来，同时也给出了系统的使用流程。 Mae 最近参加了一个关于人机交互中的伦理学研究的会议，她想起会上有一个有趣的演讲，但是忘记了作者是谁。她只记得这篇文章赢得了 Honorable Mention。她想要找到这篇论文以及相关的论文。

[![QQ截图20151112142907](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/11/QQ%E6%88%AA%E5%9B%BE20151112142907.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/11/QQ截图20151112142907.png)

Mae 首先输入两个关键词：Ethics 和 Honorable Mention。所有相关的关键词就会出现在系统的边栏当中。在边栏中提供 upvote 和 downvote 功能，便于用户优化查询选择。Mae“upvote”了关键词 Design，“downvote”了关键词 End of Life 和 E-Government。在图视图中，与 Mae 选择的关键词相关的节点以及他们之间的连接被可视化出来。在图视图中，Mae 找到了一篇题为 Categorised Ethical Guidelines for Large Scale Mobile HCI 的文章，并阅读了摘要。她认为这篇文章已经十分接近她想要找的那篇文章，就将这篇文章添加到查询关键字中，这时，CHI2013: Ethics in HCI 出现在图视图中，Mae 将这个节点也添加进查询中。切换到列表视图后，Mae 最终找到了她想要的那篇文章 Benevolent Deception in Human Computer Interaction。

Refinery 的搜索过程基于一个随机游走算法：首先根据图结构构建一个概率图，概率图的结构与原始图相同，但边表示从节点 A 转移到节点 B 的概率，计算方法如下图公式所示：

[![QQ截图20151113161525](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/11/QQ%E6%88%AA%E5%9B%BE20151113161525.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/11/QQ截图20151113161525.png)

在只有一个查询节点时，计算这个节点到达其他节点的概率，并以这个概率作为相关系数。在多节点查询时，根据 upvote 和 downvote 的信息对每个查询节点产生的相关系数进行组合。

综上，本文的主要贡献包含三点：

1. 提出了支持关联浏览的可视化系统的设计准则。

2. 提出了 Refinery 系统，通过关联浏览支持高效的自底向上的异构网络探索。

3. 将随机游走算法应用的异构网络可视化中。
