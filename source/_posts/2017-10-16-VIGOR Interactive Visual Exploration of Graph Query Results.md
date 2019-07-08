---
title: "VIGOR: Interactive Visual Exploration of Graph Query Results"
tags: ["论文评述", "报告"]
date: 2017-10-16
author: 陈文龙
---

论文：VIGOR: Interactive Visual Exploration of Graph Query Results

作者：Robert Pienta, Fred Hohman, Alex Endert, Acar Tamersoy, Kevin Roundy, Chris Gates, Shamkant Navathe, Duen Horng Chau

## **动机**

图查询或子图匹配是许多领域的重要工具，但目前大量的工作的都是围绕图算法和图查询等技术，很少有工作可以帮助用户理解图结构和查询得到的子图结果。因此，本文提出了一种新颖的交互式的可视分析系统，用于探索和理解图的查询结果。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/%E5%9B%BE%E7%89%87-1.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/%E5%9B%BE%E7%89%87-1.png)



## **系统介绍**

作者通过一个具体的使用场景来介绍系统的主要功能。该场景下使用的数据为无向的，未加权的图数据，包含数据挖掘和信息可视化社区的59,655个作者，48,677篇论文，7,236次会议，417次会议和1,634,742个关系（边）。之后使用该系统进行查询：

**查询：寻找合作撰写了两篇论文的两个作者，并且要求其中一篇发表在VAST上。**

在示例视图中构建出相应的图结构，如下图所示：

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/%E5%9B%BE%E7%89%87-2.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/%E5%9B%BE%E7%89%87-2.png)

 

**查询结果：**

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/%E5%9B%BE%E7%89%87-3.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/%E5%9B%BE%E7%89%87-3.png)

查询出的子图通过降维投影和聚类进行放置，每一个灰色方块代表一个查询出的子图， 用户可以调整聚类的参数。可以发现，A、B中的结果表示的是两篇论文一篇来自VAST， 一篇来自KDD。

**群集比较：**

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/%E5%9B%BE%E7%89%87-4.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/%E5%9B%BE%E7%89%87-4.png)

右键单击选择A,B两个群集，然后在特征探索视图中进行比较，可以发现，灰色集群（集群B）可能包含更多的高级研究人员，因为它们具有较高的论文数量，更多的合作作者。

**筛选过滤：**

此时，我们想知道是什么类型的文章桥接VAST和KDD两个研究社区，可以回到示例视图中进行过滤：

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/%E5%9B%BE%E7%89%87-5.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/%E5%9B%BE%E7%89%87-5.png)

**筛选结果：**

经过筛选，得到了如下图所示的融合图，融合图是将所有的匹配出的子图连接在一起形成的（节点会在多个结果中共享，每个节点只显示一次）。可以发现每篇论文都与理解文本数据有关，对刘世霞未来的研究具有潜在的价值。她的灵感来自于数据挖掘的速度，自动化与视觉，交互设计和可视化相结合。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/%E5%9B%BE%E7%89%87-6.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/%E5%9B%BE%E7%89%87-6.png)

 

**降纬和聚类：**

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/%E5%9B%BE%E7%89%87-7.jpg)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/%E5%9B%BE%E7%89%87-7.jpg)

 

##  User Study

作者请了12位被试分别使用vigor和Neo4j执行四个任务，结果如图所示：

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/%E5%9B%BE%E7%89%87-8.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/%E5%9B%BE%E7%89%87-8.png)

 

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/%E5%9B%BE%E7%89%87-9.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/%E5%9B%BE%E7%89%87-9.png)

可以看出VIGOR无论是在花费的时间还是在错误率方面都要优于Neo4j,而且也要比Neo4j更加易用，更受用户欢迎。

## 总结

本文提供了一个用于探索和理解图查询结果的新颖的可视化分析系统，多视图之间联动性很好，并且通过实例展示了系统的可用性和易用性。但是查询示例是通过Neo4j的查询语句建立的，对于不熟悉Neo4j的用户很不友好。