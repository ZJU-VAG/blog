---
title: " Trust, but Verify: Optimistic Visualizations of Approximate Queries for Exploring Big Data"
tags: ["论文评述", "报告"]
date: 2018-06-01
author: 张天野
mail: zhangtianye1026@zju.edu.cn
mathjax: true
---

论文：Trust, but Verify: Optimistic Visualizations of Approximate Queries for Exploring Big Data

作者：Dominik Moritz, Danyel Fisher, Bolin Ding, Chi Wang

发表：CHI 2017

## 简介：

探索式数据分析可以理解为一个分析多维数据的过程，主要通过探索数据分布及不同维度之间关联关系来完成分析过程。在这个过程中，最重要的两个要素是迭代探索与探索速度。近似查询（Approximate Query）是在探索式数据分析中常用的查询方法，能够在交互级别的响应时间内建立一个基于近似的可视化结果，但查询结果往往具有不确定性。本文提出了乐观可视化（Optimistic Visualization）的概念方法，并通过实验验证了其有效性。

## 乐观可视化

乐观可视化的前提假设是，近似结果与真实结果非常接近。其概念框架如下：

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/05/1.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/05/1.png)

用户在近似查询的结果上进行探索、分析，选择某些查询的结果向后台请求精确查询的结果，在等待精确查询结果的同时继续在近似查询的结果上探索，待精确查询的结果得到后，再与原先的结果进行对比分析。

## 近似查询

本文的近似查询方法基于 Sample+Seek，将所有查询根据查询结果的数量分为大规模查询与小规模查询。对大规模查询的结果进行均匀采样与方法无偏采样，对小规模的查询结果进行索引，从而达到加速查询速度但同时保证不会产生太高的不确定性。本文使用的不确定性通过两种方式度量：置信区间与分布不确定性，其中，分布不确定性的计算方法如下：

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/05/2.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/05/2.png)

## 系统界面

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/05/3.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/05/3.png)

上图为系统界面，其中 A-D 分别为维度选择、维度绑定、过滤、缩放等功能区，E 和 F 分别展示了近似查询的可视化结果与基于近似查询的不确定性结果。G 区域提供文本框对探索结果进行记录，并可以点击记忆按钮向后台发送进行精确查询的请求，精确查询的结果会展示在 H 部分。系统的颜色映射是统一的，橙色表示近似查询结果，蓝色表示精确查询结果。

其中，H 部分的精确结果可视化为了与近似结果进行区别并对比，做了如下处理：

（1）查询增加的组添加阴影背景

（2）近似查询值直接用橙色刻度条画在精确结果可视化视图中

（3）固定各组的宽度保持不变

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/05/4.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/05/4.png)

## 用户调研

用于用户调研的数据为 BTS Flight Delays dataset，共 70GB，包含 170 million 条记录。被试包括 5 名数据科学家，他们都熟悉运用 tableau 等探索式可视分析工具。每个实验过程包括简单的系统介绍、1.5h 的用户探索。实验中得到了若干对乐观可视化概念的评估结果：

-   被试最初对记录并查询精确结果表示抗拒，在实验过程中逐渐习惯
-   1 名被试拒绝使用查询精确结果的功能
-   1 名被试在精确结果出来前不继续在近似值上探索
-   被试往往选择记录不确定性较大的结果

## 案例分析

本文抽取了三位参与用户调研的数据科学家，对他们平时所使用的真实数据集做了案例分析。案例分析中，用户的部分反馈如下：

-   系统响应速度快
-   需要适应记录的过程
-   精确结果对部分数据有决定性的帮助
-   可以发现有意义的事件

## 总结：

本文提出了乐观可视化的概念方法以及若干基于近似查询结果的可视化决策与方案。
