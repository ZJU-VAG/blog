---
title: "Graph Structure of Neural Networks"
tags: ["论文评述", "报告"]
date: 2020-10-09
author: 潘如晟
mathjax: true
---
### 作者介绍

![作者介绍](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/10/9/b181f9b36d5d71a06f670005f360a7f9b8427b62.png)

### 背景

对于一个神经网络，我们往往能够很直观的把它和一张图联系起来。它可以是最简洁的示意图，tensorboard风格的计算图，甚至是精确到每个神经元之间的连接。我们希望能够找到一个综合以上特点的图表示，能够回答以下这些问题：

- 图的结构和网络性能之间是否存在**关联**？

- 如果是，性能好的网络对应的图结构上有哪些**特征**？

- 这些特征是否可以**推广**到一般的任务和数据集？

![背景1](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/10/9/58c2f27de277fa7ac47013d137e2ebc61b9790e7.png)
	
此外，人脑也可以抽象成一个图结构数据，通过拓扑结构等分析方法与已有的图数据进行一些类比，如下图所示。

![大脑网络](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/10/9/e4de035c57e4a236218c5856dc3e4eb7fea2c027.png)

### 相关工作
现有的现有的神经网络图的表示主要是基于计算图形式，近年来主要有二部图，有向无环图和邻接矩阵几种常见形式。

![相关工作](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/10/9/3a163993746f3fb25f087c6ace1c2c19872fc680.png)

计算图这一特定形式由于人为设定了约束，存在以下几点局限性：

- 缺乏灵活性
	- 有向无环图：人为设置的约束限制了设计空间和应用范围
- 难以与神经科学关联
	- 大脑网络的结构灵活而复杂
	- 双向的信息传输

### 贡献
基于上述这些背景，本文有以下几点贡献：

- 提出了一种新的神经网络的表示方式：关系图

![](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/10/9/daeb05c63837878559f39275bb2dbf05145e8a4a.png)

- 基于不同的前提条件，同一关系图能够代表多种网络结构

![](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/10/9/1234ef795fff68bd641909526cd9ed4f2d0688ef.png)

- 将网络科学的分析方法有效应用于图结构和神经网络性能的关系的分析

![](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/10/9/861b2ce7b4a7fcbf48f9c9f5dbcf807e27ed84b4.png)

### 关系图
#### 定义
- 节点：神经元

- 无向边：代表神经元之间的连接

- 计算：通过节点和邻居节点之间的消息交换来表示

![](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/10/9/24a83c692f5fdb5d7b4864f2b9cc4aa8d4698ade.png)

#### 优点
- 灵活性
	- 不受图结构的限制（无向图）
- 容易与神经科学联系
	- 能够表示双向信息传输

#### 信息交换

![](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/10/9/33520558ff4447ba7ebc3650e668316cbccb0450.png)

![](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/10/9/990c92fd4ac755b013c8ac7080aa0347e4f1a0e1.png)

### 关系图生成网络

![](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/10/9/18659fbfb459a983ba5fbb074c4f4281d9ac00c1.png)

![](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/10/9/3edc254708005f315cc2b3f7cac4055759ebe98f.png)

![](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/10/9/123cb17c79cf1cbd63f377b573dd7bb77f951d7e.png)

![](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/10/9/36ebe4b30fa2e8f680d7d033b81004dbec0d6911.png)

### 图结构与网络性能

- 图结构的度量
	- 全局特征：平均路径长度
	- 局部特征：聚类系数（clustering coefficient）

- 图生成方法
	
- WS-flex：有更好的覆盖范围
	
	  ![](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/10/9/88e70735a1a125f4f17572b8b5914401b2195509.png)
	
	  
	
- 控制计算开销一致

![](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/10/9/770d4fe2a4733830968f0937b89b804ec5444578.png)

### 结论

1. 不同结构的神经网络存在一致的最佳位置：具有特定结构的图所对应的神经网络往往性能都很好

![](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/10/9/997c27f346dcf54c5557eab309868279ce2ad2b8.png)2. 最好的人工神经网络和生物神经网络结构相似：最好的5层感知机和猿猴的大脑全皮层神经网络非常相似。

![](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/10/9/ee5b8c3b710e5bd3c759042cc7a2b0e8d48814b3.png)

### 总结

- 关系图基于FC，通用性有待提高

- 将网络科学和深度学习架构进一步结合

- 在图神经网络中的应用
