---
title: "SOMFlow: Guided Exploratory Cluster Analysis with Self-Organizing Maps and Analytic Provenance"
tags: ["论文评述", "报告"]
date: 2017-10-18
author: 顾宇辉
---

论文：SOMFlow: Guided Exploratory Cluster Analysis with Self-Organizing Maps and Analytic Provenance

作者：Domink Sacha , Matthias Kraus , Jürgen Bernard

简介：本文提出了一个引导式探索性聚类分析工具SOMFlow，使用SOM算法分析时变数据。

## 动机

聚类方法可用于分析大型未知的时序数据集，但存在一些问题：1.分析的问题不明确；2.有趣的模式往往隐藏在特定子集中；3.难以从一堆聚类结果中发现联系；4.揭示目标结构需要适时调整底层计算。因此聚类分析中需要交互式的数据探索，来形成和提炼假设，调整底层计算。 



## SOM算法

自组织神经网络（Self-Organizing Maps）是一种基于神经网络的聚类算法，它可以对数据进行无监督学习聚类。它的思想很简单，本质上是一种只有输入层–竞争层的神经网络。竞争层中的一个节点代表一个需要聚成的类。训练时采用“竞争学习”的方式，每个输入的样例在竞争层中找到一个和它最匹配的节点，称为它的激活节点。 紧接着用随机梯度下降法更新激活节点的参数。同时，和激活节点临近的点也根据它们距离激活节点的远近而适当地更新参数。竞争层是有拓扑关系的，因此SOM可以把任意维度的输入离散化到一维或者二维的离散空间上。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/som.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/som.png)

SOM算法具有聚类，矢量化，降维以及可用于集群可视化的特性。本文的思想就是利用SOM算法的特性，对数据进行聚类并生成对数据的Overview，并添加一系列可视化技术来支持用户对数据迭代地进行聚类分析。



## 系统介绍

### 界面设计

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/overview.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/overview.png)

## 

### 功能概述

​              [![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/design.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/design.png)





系统支持四种探索任务：1.分析当前SOM结果；2.调整数据拆分模型和参数设置；3.拆分数据生成新的SOM；4.通过流程图反思整个分析过程。

### 分析SOM结果

系统使用了多种可视化技术对SOM算法的以网格为基础的聚类结果进行可视化，为分析者提供多种手段分析聚类结果。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/analyze.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/analyze.png)

### 

### 调整底层计算

1. 对网格单元添加标签，作为附加的元数据;
2. 清洗和预处理数据，使数据标准化;
3. 调整时序特征向量的相似性度量方法（默认是欧式距离），并能调整不同时间区间的权重;
4. 设置SOM算法的参数，包括迭代次数，学习半径等，以及生成网格的尺寸。



### 数据拆分

分析者可以对当前SOM结果中的数据进行拆分，获得需要的数据子集进行进一步的探索。数据拆分操作分为三种形式：1.选择网格单元进行数据拆分；2.选择相似单元（单元集群）进行数据拆分；3.基于元数据对数据拆分。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/partition.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/partition.png)

### 使用流程图进行反思

​    [![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/reflect.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/reflect.png)







1. 每个SOM都作为整个流程图中的一个节点，箭头表示了节点之间的父子关系（过滤，分离等），箭头大小表示对应的数据数量大小。

2. 支持的交互有：

   1.选择某个SOM中的某个单元，所有的SOM中包含了相同数据的单元会高亮，程度与共同的数据数量有关；

   2.将所有SOM单元根据数据内容的相似性进行着色，颜色相似代表数据相似；

   3.选择元数据中特定属性对所有SOM单元对应的数据进行着色。

3. 所有节点都可以进行放缩、注释，调整尺寸等。

 

### 引导方法

除了支持的四种任务，系统还提供了一系列引导方法来辅助用户进行探索分析：

1.在SOM左侧按照当前SOM对元数据属性的兴趣度高低排列各个属性对应的 interestingness缩略图；

2.用户选择某一感兴趣的单元后，将相似性大于设定值的单元用虚线显示；

3.在SOM右侧显示拆分线索，点击触发相应的数据拆分操作。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/guide.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/guide.png)

## 案例分析

研究是否为母语对一门语言的发声影响。[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/case.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/case.png)