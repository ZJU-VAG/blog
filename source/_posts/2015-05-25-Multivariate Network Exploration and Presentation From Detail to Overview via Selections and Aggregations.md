---
title: "Multivariate Network Exploration and Presentation From Detail to Overview via Selections and Aggregations"
tags: ["论文评述","报告"]
date: 2015-05-25
author: 胡万祺
mathjax: true
---

## 简介
该工作首先展示给用户一副明细的多维网络图，并允许用户通过选择等交互操作对网络图进行聚集，以构造高层次结构的概览图。该论文挑战了可视化研究领军人物Ben Shneiderman所提出的可视化设计“魔咒”：首先查看概览，通过缩放和过滤，再继续按需查看细（overview first, zoom and filter, then details on demand）。文章中提出，对于复杂多变量点连接图来说，自动识别出用户感兴趣的聚类和模式并生成概览图是很难做到的；而且对于大部分非专家用户来说，网络图的概览图才是他们最终想要的结果。本文提出的可视化系统提供了两个联动的视图：节点连接图和生成的概览图，用户先查看网络图的细节内容，再根据自己对网络图的初步了解和认识通过交互生成概览图，并在该过程中逐步理解图的网络结构。

下图是本文提出的可视分析系统界面截图。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/%E5%9B%BE%E7%89%8712.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/图片12.png)

## 系统界面

其中A窗口为网络节点图的细节视图，B窗口为用户的交互生成的概览图，C窗口提供当前选中区域的点和边的过滤筛选功能，D为选中区域管理窗口，E和F分别为A和B窗口的属性编辑区。系统操作流程如下图所示：开始先生成一副明细的多位网络图，并隐藏所有的链接边。用户在细节图窗口框选节点、改变节点的投影方式、用特定的条件对节点或对链接边进行过滤等最终筛选出感兴趣的点，系统会自动对每个区域中的点和链接边进行聚合统计并生成概览图，并展示出不同选择区域的统计信息和链接关系（包括方向、大小等），另外节点的其他维度信息也可以选择用不同的可视化视图进行展示。通过A和B窗口中左右两个细节图和概览图做到同时将网络图中的拓扑结构和节点、链接的其他维度信息同时展现给用户。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/%E5%9B%BE%E7%89%8721.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/图片21.png)

## 系统操作流程图

本文获得了InfoVis2014的最佳论文奖，表明大会不仅仅希望研究人员能够在可视化设计上做出突破，更是在鼓励研究者积极参与到可视化领域的基础研究中去。