---
title: "AmbiguityVis: Visualization of Ambiguity in Graph Layouts"
tags: ["论文评述", "报告"]
date: 2016-06-25
author: 王叙萌
mail: wangxumeng@zju.edu.cn
mathjax: true
---

论文：AmbiguityVis: Visualization of Ambiguity in Graph Layouts

作者：Yong Wang, Qiaomu Shen, Daniel Archambault, Zhiguang Zhou, Min Zhu, Sixiao Yang, Huamin Qu

发表会议：InfoVis 2016

## 1. 动机

对于目前被广泛应用的节点链接图来说，由模糊信息导致的歧义很难避免。除此之外，当图结构比较复杂时，用户经常需要边捆绑和点聚合等方法来简化它。

## 2. 贡献

该工作的贡献包括一些可以量化图结构中的歧义的度量方法，可以基于度量方法得到的结果来可视化图结构中歧义的系统以及相关案例和专家建议。

## 3. 相关工作

本文的相关工作从图的绘制，图的可读性度量以及社团的分离性度量三个方面进行了比较充实的讨论。

## 4. 度量方法

-   关于边长：一般认为与一点直接相连的点应距离该点比较近，作者对所有点到对象的距离进行了排序，若与其相连的点的次序超过了与其相连点的总数，将被任务是有歧义产生，并进行相应计算。
-   关于社团分离性：本文提供两种度量社团分离性的方法，分别是基于熵和自相关的。

![](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/06/QQ%E5%9B%BE%E7%89%8720160625160546.png)

-   关于边捆绑，本文从边的距离，长度相似性以及平行度三个方面来计算一对边之间的差异，之后通过 MDS 方法将它们展现出来。

![](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/06/QQ%E5%9B%BE%E7%89%8720160625161423.png)

-   关于点聚合的度量方法比较简单，只是列出聚合内节点的数量、聚合内边的数量、该聚合和其他点间的边数量以及图的密度等统计信息。

## 5. 可视设计

本文的可视设计十分简单，主要是由上述度量方法定义的热点位置及用户定义的热点范围结合得到的热力图。整体界面包括八个子视图，一次是选择歧义类型和调节参数的控制面板、原始布局、边捆绑布局、热力图选择器、点聚合视图和两个相关信息评价图。

![](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/06/%E5%9B%BE%E7%89%871.png)

## 6. 总结

本文的想法十分新颖，调研十分全面，最终成型的系统比较方便使用，而且易于和其他系统结合。但是也存在如下不足：其系统的任务驱动性有待提高；度量方法没有经过以人为中心的评估验证；布局和方法比较简单。
