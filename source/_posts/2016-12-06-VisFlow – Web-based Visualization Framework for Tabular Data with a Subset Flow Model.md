---
title: "VisFlow – Web-based Visualization Framework for Tabular Data with a Subset Flow Model"
tags: ["论文评述", "报告"]
date: 2016-12-06
author: 刘良军
mathjax: true
---

论文: VisFlow – Web-based Visualization Framework for Tabular Data with a Subset Flow Model

作者: Bowen Yu and Cláudio T. Silva Fellow

发表期刊: TVCG 2016

## 1 简介

数据流系统允许用户通过直接编辑流程图来对数据进行处理、过滤和展示。用户自定义的数据流有益于进行可视分析，包括按需要呈现多个图以及执行不同类型的交互性查询。本文提出了一个用于分析表格数据的 WEB 可视化框架 VisFlow，在这个框架中使用了一种叫 subset flow model 的的数据流模型。VisFlow 着眼于数据流的交互查询，克服了过去计算性数据流系统的交互问题。VisFlow 实现了数据的可视化，同时支持在数据流中进行交互选择，brushing 和 linking。同时本文实现了以 VisFlow 框架为基础的原型系统，并且通过案例分析来验证了 VisFlow 系统的有效性。

## 2 动机

目前存在许多基于数据流的系统，但是这些系统对于数据的可视分析来说都存在一些问题：

1. 许多数据流系统是以进行数据的计算与处理为目的进行设计的，在这些系统中，其数据流程图其实是程序的视觉抽象，比如它的输入与输出对应的是调用的程序方法的参数，因此使用这些系统需要用户具有一定的编程背景；

2. 对数据进行使用了数据流的分析平台通常并不是专门设计来进行可视化的，这些系统所得到的可视结果大部分都是数据的统计信息的可视展示，并不支持交互的数据探索。然而，能通过交互进行数据选择和过滤是可视分析的一个基本要求。

3. 那些针对可视化进行设计的数据流系统主要的目的也只是产生渲染的可视流程，在这些系统中，交互有限，通常仅仅只能进行浏览。

因此为了支持用户在可视分析系统中动态的查询以及自定义数据的分析过程，本文提出了 VisFlow 框架，支持用户以可视的方式直接自定义数据分析流程从而帮助用户的分析。

## 3 贡献

1. 提出可以使用 subset flow model 来处理以前的数据流系统中存在的交互性和复杂性问题，并以此提出了一个 WEB 可视化框架 VisFlow。

2. 基于 VisFlow 框架实现了一个原型系统，这个系统可以在浏览器上使用。

3. 通过专业领域数据分析的案例分析验证了该框架的有效性以及实用性。

## 4 相关工作

Domino 可视方法

![](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/12/001.png)

IBM SPSS Modeler 数据分析系统

![](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/12/002.jpg)

Voreen 一个用于体绘制的快速原型环境

![](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/12/003.gif)

ExPlates

![](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/12/004.png)

## 5 VisFlow 框架

### 5.1 数据

VisFlow 针对的是表格类型的数据。表格类型的数据可以分为两类：a)不同的数据项之间相互独立;b)不同的数据项之间存在关联

![](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/12/005.png)

Visflow 支持异构数据，可以对异构数据进行组合和可视化。比如，一个图通常用两个表格表示，节点表以及边表。VisFlow 支持将两个数据传入渲染生成图的可视化结果。

![](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/12/006.png)

### 5.2 流程图

VisFlow 中的流程图是由节点，端口，连接边三部分组成的一个有向无环图。

1. 节点包含六种类型：Data sources、Visualizations、Value generators、Filters、Property binders、Set operations。

2. 每个节点都有输入输出端口，左边的输入端口，右边的为输出端口。包含一个点的端口表示该端口只能连接一条边，包含三个点的端口表示该端口可以连接多条边。Visualizations 还会有一个选择输出端口。

3. 连接边上传输的数据一般有两类，第一类是子集数据，第二类是常量数据。

![](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/12/007.png)

### 5.3 用户界面

用户界面分为三个部分：左边的工具栏，中间的 SVG 画布，右边的节点设置栏。

![](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/12/008.png)

### 6 案例分析

#### 6.1 案例 1：基因调控网络分析

这个 case study 表明 VisFlow 能够辅助分析专业领域数据，并且不需要进行编程。

![](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/12/009.png)

### 6.2 案例 2:棒球投球分析

这个 case study 表明 VisFlow 可以直接交互分析同棒球数据一样复杂的特定领域数据，而且使用方便有效。

![](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/12/011.png)

## 7 总结

本文使用 subset flow model 平衡了数据处理、可视化交互性和易用性三者之间的关系，但也因此使得系统不支持对数据进行循环分析，也不支持迭代过滤。本文针对系统的易用性做了许多设计：

1. 流程图中使用的是相对通用的图表;

2. 流程图中任意两个结点之间最多一条边;

3. 可视结点都有一个选择输出端口，减少了对过滤的需求;

4. 系统使用简单，不需要大量的训练，学习成本低;

5. 没有大量的输入/输出值。
