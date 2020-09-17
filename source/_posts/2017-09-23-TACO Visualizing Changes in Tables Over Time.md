---
title: "TACO: Visualizing Changes in Tables Over Time"
tags: ["论文评述", "报告"]
date: 2017-09-23
author: 朱闽峰
mail: minfeng_zhu@zju.edu.cn
---

论文：TACO: Visualizing Changes in Tables Over Time

作者：Christina Niederer, Holger Stitz, Reem Hourieh, Florian Grassinger, Wolfgang Aigner, and Marc Streit

发表会议：IEEE InfoVis 2017

## **介绍**

很多领域下，表格数据是一种非常常见的数据。当表格有多个版本的时候，理解表格数据就需要比较不同版本的表格。然而当前的可视比较工具的可视结果难以解释，并且不适用于大规模数据。作者设计了一个新的可视化工具 TACO (TAble COmparison)，用于比较表格版本的随时间变化情况。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/09/Picture1.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/09/Picture1.png)

## **数据**

文章中使用的数据包括两个：一、自 1986 年到 2012 年的夏季奥运会比赛数据；二、大规模肿瘤基因组学数据（病人及其对应的 microRNA 集合）。

### **表格数据变化类型**

作者首先对于表格数据的变化类型进行了归纳，包括四个方面：

1. 结构变化，主要体现在表格行列的增加或者删除，比如在奥运会数据表中，参赛国和比赛项目的变化。
2. 内容变化，主要体现在表格数据单元格的值的变化。
3. 排序变化，主要体现在表格的行列位置发生变化，比如在奥运会数据中，国家按照总金牌数来排名。
4. 合并/分离变化，主要体现在多行（列）合并为一行（列），比如多次实验结果取平均值。

### **表格数据变化计算**

对于表格数据的变化，文章通过以下方式进行计算。首先基于对比的两个表格进行并操作，两个表格分别与并的结果进行比较，得到发生变化的单元格。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/09/Picture2.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/09/Picture2.png)

## **变化信息多层次聚合**

为了支持大规模表格变化的可视化，我们需要对表格的变化做一些聚合。对于表格的变化，绿色代表单元格增加，粉色代表删除，蓝色代表单元格值发生变化。文章对表格变化做了不同层次的聚合，首先总变化比例（b）展示了整个单元格整体变化的比例，行列变化图（e，f）统计了每行每列变化的比例，2 维变化比例（g）图展示了行列上的总变化比例。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/09/Picture3.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/09/Picture3.png)

## **可视化设计**

文章采用 overview+detail 的可视化设计，从概览到细节逐层进行比较：

### 1.基于时间线的总览

stacked bar 展示表格数据两个连续版本的总体变化比例，其中，矩形总高度编码表格大小，颜色高度编码各个变化类型的数量。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/09/Picture4.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/09/Picture4.png)

### 2.表格基本信息和变化预览

进一步，分析者可以选择两个感兴趣的表格进行对比，从一些聚合的变化信息上了解大概。信息窗展示两个表格的基本信息，二维化比例图展示了行列上的变化比例。颜色和之前的编码一样，绿色代表增加，粉色代表删除，蓝色代表单元格变化。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/09/Picture5.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/09/Picture5.png)

### 3.基于每个单元格变化的细节比较

进一步，分析者可以查看基于单元格的变化情况，分析表格变化的原因。用热力图的方式展示两个表格各自的单元格值。对于表格变化的可视化，文章对于不同变化类型设计了不同的可视化方法：

结构变化（行列的增删）——绿色或者粉色的直线

内容变化——渐变的颜色编码归一化的值变化

合并分离——Y 连接符

排序变化——紫色的线连接原始位置和最新位置

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/09/Picture6.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/09/Picture6.png)

## **案例分析**

对于夏季奥运会数据，我们从时间轴中可以看到，随着时间增加，矩形的高度不断增加，这说明参加奥运会的国家和比赛项目增加。同时我们也发现了在 1934 年和 1948 年之间的时间轴上没有信息。这是因为由于第二次世界大战，1940 年和 1944 年没有举办奥运会。因此我们聚焦于世界大战前后奥运会的变化，即比较 1934 年和 1938 年的奥运会数据。在图(c)中，列上面有少量的绿色，这说明有少量的比赛项目增加了。同时在表格数据行上的变化非常大，意味着有大量的国家新参加了，同时也有许多国家缺席了。在(d)中可以进一步分析原始的表格数据，我们可发现：

-   德国参加了 1936 年，缺席 1948 年
-   法国、比利时、意大利于 1948 年参加
-   比赛项目增加女子 200 米和女子 500 米单人皮艇
-   芬兰于 1936 年赢得男子 10000 米三枚奖牌，但 1948 年颗粒无收，所以排名从 1936 年第六 掉到 1948 年最后

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/09/Picture7.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/09/Picture7.png)
