---
title: "Embedded Merge & Split Visual Adjustment of Data Grouping"
tags: ["论文评述", "报告"]
date: 2018-12-09
author: 梅鸿辉
mathjax: true
---


论文：Embedded Merge & Split Visual Adjustment of Data Grouping

作者：Ali Sarvghad, Bahador Saket, Alex Endert, and Nadir Weibel

发表：IEEE InfoVis 2018



本文作者设计了一系列直观简便的操作，用于进行统计直方图或柱状图的调整，包括merge，split，和change number of bins
Histogram: merge
[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/11/%E5%9B%BE%E7%89%8711.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/11/图片11.png)
Histogram: split
[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/11/%E5%9B%BE%E7%89%8721.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/11/图片21.png)
Bar chart: merge
[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/11/%E5%9B%BE%E7%89%8731.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/11/图片31.png)
Bar chart: split
[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/11/%E5%9B%BE%E7%89%8741.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/11/图片41.png)

## 问题描述

分组统计在探索数据是是很常见且分组的好坏对数据的分析。很多可视化工具提供自动分组的方法，但调整分组却没有很好的手段。
常见的方法有两种，一是编程实现，二是WIMP(Window/Icon/Menu/Pointer)方法，即通过面板、菜单、对话框等进行设置。

## 本文方法

本文的方法更加直观，原因在于操作和提示均嵌入了可视化内，同时提供直接操作（Direct manipulation），使得用户可以一边操作一边观察效果。
[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/11/%E5%9B%BE%E7%89%878.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/11/图片8.png)

## 评估

对这个方法，作者进行了定量和定性的评估。
定量分析对比本文方法和Tableau，结果显示在时间和准确性上都有显著增强。
[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/11/%E5%9B%BE%E7%89%875.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/11/图片5.png)
定性研究5个HIV学者，记录他们在使用过程中的发现和想法（think-aloud）。
得到优点有：

- 与心理模型的一致性
- 无缝和流畅的互动

而缺点则是：

- 难以选择非常小的目标
- 难以选择重叠对象

此外，作者还讨论了本方法在其他类型图标上的可能应用
[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/11/%E5%9B%BE%E7%89%876.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/11/图片6.png)
[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/11/%E5%9B%BE%E7%89%877.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/11/图片7.png)

## 总结

- 直接操纵可视编码以调整数据分组
- 显着缩短交互时间
- 缩小执行鸿沟（所思即所做即所得）

