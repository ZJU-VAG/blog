---
title: "Sequence Synopsis: Optimize Visual Summary of Temporal Event Data"
tags: ["论文评述", "报告"]
date: 2017-10-17
author: 刘良军
---

论文：Sequence Synopsis: Optimize Visual Summary of Temporal Event Data

**优化针对时序事件数据的可视化摘要**

作者：Yuanzhe Chen, Panpan Xu and Liu Ren

发表： TVCG2017

## 1 简介

本文的主要内容是讲如何可视化时序事件数据，提出了一种对这类数据进行可视化的技术，该技术可以较好的提取出高维事件数据中的事件模型。并基于该技术实现 了用于分析高维时序事件数据的可视分析系统 。有两个和领域专家合作进行的case study。

时序事件数据（Temporal Event Data）：每个事件由三个要素组成，即事件类型、发生时间和发生主体，由一系列此类事件组成的数据叫做时序事件数据。例如网站点击事件流以及软件的用户交互日志。



## 2 动机

对时序事件数据的研究早在1996年就开始了，目前已经有许多针对事件数据的可视分析系统，但是这些系统对于这类数据的可视分析来说仍存在一些问题：

1）如果数据维度过高的话，在这些可视分析系统中，数据容易产生混乱，可读性差，不便于用户观察，也不便于用户交互。

2）无法得到一个好的数据摘要，难以让用户对数据形成一个直观全面的的认识。

3）现有的可视分析系统中预处理数据时使用的方法无法有效地处理数据噪声。

因此本文针对现阶段存在的问题提出了Two-part representation。将原始事件数据分解成pattern和corrections两个部分来表示。



## 3 相关工作

LifeLines (1996)

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/ss01.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/ss01.png)

DecisionFlow（2014）

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/ss02.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/ss02.png)



## 4 可视化方法

### **Two-part Representation**

本文不同于传统的可视化事件数据的方法，作者基于MDL原理（最小描述长度原理）原始数据分成两部分（Patterns + Corrections）来表示。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/ss03.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/ss03.png)

，然后通过可视化分解后的两个部分来达到可视化时序事件数据的目的。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/ss04.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/ss04.png)

在这种设计中，即能使得在数据量比较大的时候可视表达不太混乱，提升可读性。也能对原始数据形成一个直观全面的认识。

每一个pattern表示一个事件序列集合，在一个pattern中，每一个矩形表示一个事件，从左到右按时序排列，颜色编码不同的事件。 corrections是用三角形和矩形的高度来编码的，三角形在的地方表示该集合中存在事件序列需要在这个位置插入事件才能对应上该pattern， 三角形的大小表示该pattrrn对应的事件序列集合中这种序列的个数。矩形的高度编码对应集合中包含该事件的序列个数。 通过这两个可视编码我们可以查看信息损失量。

作者在文章详细讲述了如何类比MDL原理，来实现pattern的提取，还提供了一个算法用以加速提取过程。



## 5 可视化设计

### **1.系统界面**

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/ss05.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/ss05.png)

 

### 2.Event Filter

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/ss06.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/ss06.png)

### 3.Summary View

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/ss07.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/ss07.png)

### 4.Sequence View

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/ss08.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/ss08.png)

 

## 6 总结

本文虽然解决了一些使用事件数据传统可视方法会遇到的问题，但是依然存在一定的局限性。

1）难以应用于含有大量独立Pattern的时序事件数据

2）在真实数据中一个事件序列可能含有多个pattern

3）真实数据中的事件重要性可能并不相同