---
title: "Graphiti: Interactive Specification of Attribute-based Edges for Network Modeling and Visualization"
tags: ["论文评述", "报告"]
date: 2017-10-31
author: 韩东明
mail: dongminghan@zju.edu.cn
mathjax: true
---

论文：Graphiti: Interactive Specification of Attribute-based Edges for Network Modeling and Visualization

作者：Arjun Srinivasan, Hyunwoo Park, Alex Endert, Rahul C. Basole

发表：VAST2017

## 作者

1. Arjun Srinivasan

    - Georgia Institute of Technology.
    - PhD.
    - VA.lab Georgia Tech Visual Analytics Lab.
    - language interfaces, mixed-initiative systems.

2. Hyunwoo Park

    - The Ohio State University.
    - Translational Data Analytics InstituteAssistant Professor.
    - Management Sciences, business and data analytics.

3. Alex Endert
    - Georgia Institute of TechnologyAssistant.
    - Professor.
    - VA.lab Georgia Tech Visual Analytics Lab.
4. Rahul C. Basole
    - Georgia Institute of TechnologyAssociate.
    - Professor.
    - Computational enterprise science.

## 动机

1. 网络构建
    - 点边关系复杂，种类多。
    - 分析任务多样，不同的分析任务构建出的网络不一样。
    - 数据了解困难，用户往往很难了解数据，构建起来就更加困难。
2. 基于示范的交互
    - 用户演示一次，机器跟着做。

## 贡献

1. **基于示范的交互** `demonstration-based interaction`通过研究网络可视化，增强对于此的理解。

2. 交互系统 Graphiti

## 相关工作

1. 网络可视化和分析工具（16 篇）
    - 本工作关注的是网络构建的任务
2. 基于示范的交互
   Wrangler: Interactive Visual Specification of Data Transformation Scripts
   Visualization by Demonstration: An Interaction Paradigm for Visual Data Exploration
3. 网络构建工具
    - 本工作关注在网络建模中应用基于示范的交互

## 总览

### 总览分析

-   用户先确定需要构建的网络的节点类型。
-   用户选择想要进行连接的两个节点进行边创建，此时会提示可以成为边的条件。
-   选择成为边的条件，进行边的生成。
-   之后可以选点节点进行相同边的拓展，或者应用从全局。
-   已有边上的条件可以进行增减及帅选

边的类型确定

1. 分析节点属性
    - numerical
    - categorical
    - list
    - textual
2. 节点的属性表
    - 不同存储方式(例如 textual 进行主题模型的抽取存储)

确认边的类型

1. 识别边

    - 四种属性的相似性

2. 展示边
    - 精简语言，交互组件

## 系统

A. 数据集的导入

B. 主视图(布局)

C. 网络的属性

D. 节点的信息

E. 控住按钮(缩放，迭代控制)

F. 边的条件推荐

G. 边的类型展示(有哪些边条件组成以及交互)

H. 数据导出

## 使用场景

### 生成网络

选中两个节点进行边创建，左下方面板提示可以成边的条件。

选择不同的条件，去生成边。边的条件可以进行筛选增减。

应用到全局。

可以添加第二种边的类型。

### 基于已有网络

原有网络的力引导图布局，蓝色为原有的边。

创建原有网络并没有相连的节点对，然后选择成边的条件。

全图生成边，灰色的是新加的边，红色的是原有的和新加相重合的边。

## 其他特性

-   易于探索节点的一度邻域，用户可以选择指定的节点进行基于新建边的拓展
-   条件过滤等小组件

## 讨论

1. 基于范式的交互
    - 可应用的范围广，多数据，多领域，多应用。
2. 边的条件，高度定制化
    - 相似度算法
    - 条件的排名算法
3. 人机探索
    - 用户的选取方式和机器的推荐
