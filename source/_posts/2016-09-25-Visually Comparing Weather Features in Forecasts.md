---
title: "Visually Comparing Weather Features in Forecasts"
tags: ["论文评述", "报告"]
date: 2016-09-25
author: 林立文
mathjax: true
---

论文：Visually Comparing Weather Features in Forecasts

作者：P. Samuel Quinan, Miriah Meyer

发表：TVCG 2016

## 介绍

气象学家通过可视化结果来考察天气特征中的信息，对天气预报提供帮助。文章作者与气象学者合作，指出天气可视化中遇到的两个主要挑战：1)各种可视化方案之间不一致；2)对于一组预报结果中特征的关联缺少直接的可视化支持。在这项工作中，作者考察了若干个气象数据，对于不同的问题类型，提出了一组有效的可视化方案，在一个开源工具WeaVER中体现了这些可视化方法；并思考在使用气象数据中遇到的挑战。

## **多维气象数据可视化方案**

作者从不同来源搜集了具有代表性的一系列气象数据可视化结果。考察这些图像之后，肯定了其中一些符合可视化原则的有效方法、并对其它一些情况给出了改进的方案，以提高气象研究者的效率。

1)对于相互独立的场（即解读其中一个场的信息不需要对另一个场的知识），建议在底层颜色图、一组轮廓线、一组纹理或符号这三种视觉编码中组合，以对应于2个标量场以及1个标量或向量场。下图是其中一个例子：

![](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/09/1.png)

2)对于通过一组数据推导得出的均值与变化值（如标准差），建议以底层颜色图显示变化值的矩阵、并使用轮廓线显示均值。下图是一个例子：

![](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/09/2.png)

3)对于某条件的概率值，建议在重点关注的数值区间用颜色图表示，对于其他数值区间则使用轮廓线表示。下图是一个例子：

![](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/09/3.png)

4)对于底层的视觉编码，作者也给出了一些建议。如一些常用的变量的颜色表，如下图所示：

![](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/09/4.png)

（上图各组颜色表对应的变量分别为：温度、风速、降水量、相对湿度、标准差、概率、Haines指数）

在这个颜色表中，体现了一些原则。除最右端的Haines指数以外，其余各项都尽可能使得亮度均匀变化；设计颜色表时，不涵盖全部亮度范围，为轮廓线与符号等留下空间；颜色表大多数所映射的数值范围都是跨度较大固定值，以便统一观察多组可视化结果（标准差除外，因为标准差的数值含义会随具体情况变化）。

5)对于同时显示一组数据(组内每个数据来源也含有若干特征)的情况，作者将spaghetti plots与contour boxplots改进为interactive(交互式) spaghetti plots与interactive(交互式) contour boxplots，用于同时呈现若干个来源的数据，并支持用户高亮显示所选的组成员。下图分别为两种可视化方法的例子：

![](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/09/5.png)

![](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/09/6.png)

（其中后者是为了避免组的成员过多造成视觉上的不便）

## **系统实现**

作者将这些可视化方法加入到WeaVER中，对此提供了五个视图，下图为系统运行的一个截图：

![](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/09/8.png)

同时，对这个系统，作者协同一些研究者进行了实例的验证。如对于Diego山火事件的预测，首先使用 deterministic与stat视图了解大气整体情况、然后使用direct ensemble视图进行多个模型的比较、最后使用probability视图判断各个地点发生山火的可能性。下图为最后一个视图的情况：

![](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/09/7.png)

（其中概率条件被设置为了：表面温度大于60°F、表面风速大于20mph、Haines指数大于等于5）

## **总结与展望**

作者对与天气预报中的一些问题与数据进行考察，提出了一个可视化方案并加入到系统中，并得到了气象研究者的肯定。

对于新加入的两个改进视图(interactive spaghetti plots, interactive contour boxplots)，仍然需要正式的评估。对于非轮廓线的情况，目前还没有直接进行一组数据的可视化或者比较。这些都是未来可以关注的方向。