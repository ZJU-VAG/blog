---
title: "基于语义的大规模出租车轨迹交互分析方法(SemanticTraj)"
tags: ["论文评述", "报告"]
date: 2016-11-24
author: 黄兆嵩
mail: zhaosong_huang@zju.edu.cn
mathjax: true
---

论文: SemanticTraj: A New Approach to Interacting with Massive Taxi Trajectories

作者: Al-Dohuki S, Kamw F, Zhao Y, et al.

发表期刊: TVCG2016

## 简介

在城市规划、城市运输及城市交通管理等领域，对于车辆轨迹的信息挖掘和知识提取越来越重要。大规模的城市出租车轨迹数据，能够帮助各个领域的专家分析城市交通和城市人群的移动规律。现有的工作大都围绕对地理位置的框选或刷选来完成数据的过滤。

本文介绍了一种基于语义信息对大规模出租车轨迹数据进行交互式的检索、分析的可视化方法。领域专家或者使用者可以通过输入带有语义的查询条件对轨迹数据进行查询检索，并通过系统的可视化界面对轨迹数据进行探索，从而得到有用的信息。系统通过在轨迹数据上建立了两种文本语义索引文件来加速语义查询速率，并设计了多视图的可视化界面来帮助用户分析轨迹数据。最后通过用户的实验验证了系统的可行性。

## 问题导向

大规模的出租车数据对城市交通城市规划等领域提供了很多有用的信息。为了挖掘出这些信息，现有的大量工作研究了轨迹信息的可视分析，轨迹信息的存储和轨迹语义的标注。然而这些工作大都是基于对地理位置的刷选来完成对数据的过滤。对于特定的任务，例如一家商场的管理者，希望知道在城市的什么地点放置摆渡车辆，能够帮助人们来商场购物? 交通警察希望知道哪些路段是经常堵车的路段，那些路段交通状况很好? 如果使用原有的系统来回答类似上述的问题，操作就会十分繁琐。而如果可以直接通过语义来查询满足条件的出租车轨迹信息，那么分析的时间就会大大下降了。

## 界面设计

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/1.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/1.png)

系统的主界面如上图所示：

1. 查询输入框，允许用户进行文本的输入条件，同时也可以打开查询条件的选择器（如下图）。查询支持布尔查询，模糊查询，渐变查询和范围查询。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/2.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/2.png)

2. 绘制选项，系统提供了绘制选项使得用户可以自定义轨迹绘制的透明度，颜色宽度等属性，完成自定义的可视化效果。

    3.4.5. 轨迹的各种分析视图，包括反应道路交通流向关系的桑基图，轨迹数据各个维度的平行坐标图，数据的详细列表，和反应轨迹数据速度的环形热力图。并用文本的方式总结了轨迹的基本特点，包括轨迹的速度，车辆数目，上下客的最多的 5 条道路等信息。帮助用户完成轨迹的多角度分析任务。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/3.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/3.png)

6. 地图面板，用于在地图上直观的绘制轨迹，并添加文本的标签帮助用户理解轨迹的语义信息。

## 数据处理方法

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/4.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/4.png)

出租车的轨迹数据如上图所示，记录了某城市一个月的 8120 辆出租车的轨迹信息。基本的数据处理流程如下图。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/5.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/5.png)

系统通过文本语义的转换工具，把原始的出租车轨迹数据转换成两种不同类型的数据索引文件，包括出租车轨迹索引文件和行程索引文件。前者记录某出租车的轨迹语义索引，后者通过上下客信息记录某一段乘客的行程语义信息。并通过行驶距离计算出行驶的花费。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/11.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/11.png)

转换过程中，每一条数据的街道名称通过距离数据经纬度最近的街道来获取，而速度信息也通过赋予速度数值语义的方式转化为用户更能理解的数据格式，方便用户进行语义查询。

## 分析及案例

系统通过了交通专家，犯罪学家及 15 名计算机学生的实验，通过该实验，结果表明轨迹数据的语义信息有利于更快速有效的理解数据。系统展示的各种统计图表和查询效率非常有利于交通问题的分析。系统中总结的文本信息有利于对数据信息的挖掘。证明了系统的有效性。

查询速率方面，作者提出了三个问题：

-   Q1：查询经过上塘路的所有出租车轨迹

-   Q1：查询经过上塘路和中河高架的所有出租车轨迹

-   Q1：查询经过上塘路或中河高架的所有出租车轨迹

验证系统的查询速率。结果表明所有的查询都能控制在交互级别的时间。证明了语义索引文件的有效性。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/8.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/8.png)

最后通过案例分析，验证了系统在解决实际问题方面的有效性（举 1 例）：
浙江博物馆的管理人员想要选择接送游客的班车地点。他们通过输入浙江博物馆作为上下客地点为条件，过滤出的出租车图例如下。绿色(红色) 点表示出租车的上客(下客)地点。用户通过总结的文本信息和绿色点的位置分布，很容易的找到来博物馆的人最多的街道名称和地点，从而能够建立游客接送点。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/9.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/9.png)

然后管理人员通过平行坐标图，发现，下午 3 点到 5 点的车辆明显比其他白天的车辆少很多，从而能够得出在下午 3 点和 5 点可以适当的减少车辆来节约成本的结论。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/10.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/10.png)

## 总结

语义信息和地理信息的结合将愈演愈热，就像计算机与人，缺一不可。
