---
title: "StreetVizor: Visual Exploration of Human-Scale Urban Forms Based on Street Views"
tags: ["论文评述", "报告"]
date: 2017-12-26
author: 朱闽峰
mail: minfeng_zhu@zju.edu.cn
mathjax: true
---

论文：StreetVizor: Visual Exploration of Human-Scale Urban Forms Based on Street Views

作者：Qiaomu Shen, Wei Zeng, Yu Ye, Stefan Müller Arisona, Simon Schubiger, Remo Burkhard, Huamin Qu

发表：IEEE SciVis 2017

## 介绍

城市的形态和人群在城市中的生活息息相关。当我们描述一个城市的时候，可以从宏观和微观两个角度。宏观的城市形态主要包括面积和人口等描述大范围的指标。而微观的城市形态是基于人的感知的，如视觉、触觉、听觉和在城市中的体验。微观的城市形态和人的生活更加密切，因此理解城市形态对于设计搞质量的城市空间非常重要。 经典的城市理论研究只是基于小范围人群的调研，不能提供更加广泛并且深入的指导性意见。而谷歌街景图忠实得记录了道路上多个地理位置的全景视角，这类似于人类的眼睛，提供了从视觉角度研究微观城市形态的方法。我们可以从街景图中查看绿化、天空和建筑等信息在城市不同区域的分布。

## 目标

1. 量化城市形态的多个属性：绿化、天空、车辆

2. 多个层次上探索城市形式：城市、区域、街道

3. 比较不同区域的城市形式

## 分析任务

T1：多尺度的探索

-   城市形态可以组织城市层次、区域层次、街道层次

-   overview 到 detail

T2：定量测定

-   特征：绿化、天空、建筑、道路、车辆

-   城市形态的特征统计、特征分布、特征方差

T3：排序和比较

-   方便浏览和探索，特征需要被排序

-   选择两个区域进行比较特征

## 系统框架

1. 数据采集：Google Street View

文章手机了 170 万张谷歌街景图片，包括新加坡、香港、伦敦和纽约等四个城市。首先从 OpenStreetMap 中获取路网信息，每隔 50 米采集一张谷歌街景图，只去街景采集车辆行进过程中向前向后的照片，因为这边照片包含了道路上的信息。

2. 数据处理：SegNet

基于深度学习方法 SegNet，所有图片的像素点被分为 12 个类，包括绿化、天空等。作者对 12 个类做了聚合，分为绿化、天空、建筑、道路、车辆和其他共 6 个类。每张图片按照 6 个类的像素点比例构成 6 维向量。

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/12/Picture1.png)

3. 可视分析流程

整个可视化分析的流程包括两个步骤，首先在 Ranking Explorer 视图中选取两个要比较的街道或者区域，然后在对应的 AOI Explorer 或者 Street Explorer 比较不同层次的城市形态。

Ranking Explorer：选择两个街道/区域

AOI Explorer：城市、区域层次的比较

Street Explorer：街道层次的比较

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/12/Picture2.png)

## 可视化设计

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/12/Picture12.png)

可视化系统主要包含 3 个视图，分别是 Ranking Explorer（左）、AOI Explorer（中）和 Street Explorer（右）。

### Ranking Explorer

本视图用于总览不同区域或者街道的特征分布，帮助用户选择感兴趣的对象。

布局：每一行代表城市、区域或者街道，每一列代表 6 个特征维度，每个单元格展示了特征的平均值。

### AOI Explorer

此视图包含两个模块，地图模块（b）和统计模块（c）。

地图模块展示了要比较的两个区域的地理位置，其中使用点密度图展示了街景图的位置。点的颜色是街景图中最大值的特征颜色。

统计视图是为了展示不同特征维度间的相关关系。由于街景图太多，绘制效率比较低，所以作者先采用了聚类的方法，将多张街景图做聚合。然后，特征之间的相关关系分一下几个方面来展现：

Feature Correlation（a）：散点图的形式展现两两维度之间的关系。

Feature Histogram（b）：每个维度的数量统计

Feature Diversity（c）：x 轴为类均值，y 轴为标准差

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/12/Picture21.png)

### Street Explorer

街道视图也包含两个模块，分别是地图模块和统计模块。

统计模块中主要是结合了路网的平行坐标轴，它的绘制方法分以下几个步骤：

1. 找到以起始点为边的最小长方形

2. 旋转至起始点到上下绘制边界

3. 主题河流：道路上的每一个采样点都有对应的六个维度的数值，数值作为河流的宽度

4. 平行坐标轴显示属性值的分布

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/12/Picture3.png)

## 案例分析

City-scale Comparison

我们首先对比分析新加坡（左）和伦敦（右）的城市形态。我们可以看到新加坡形成了很多区域，黄色建筑和绿色植物参杂在一起。而在伦敦，市中心黄色建筑比较多，在城市边缘绿色逐渐增多。这是由于伦敦的城市发展过程中是不断扩张的，而新加坡由于岛屿的原因，无法扩张。

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/12/Picture5.png)

Region-scale Exploration

在这里我们比较了新加坡的东陵（红）和伦敦的中央公园（蓝），这两个地方都是公园性质的区域，具有类似的功能。从 A1 中可以看到，这两个区域都有非常高的绿化属性，而中央公园绿化更高一些。A2 中说明新加坡的东陵有更高的建筑比例，这是由于新加坡希望最大化土地利用率。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/12/Picture6.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/12/Picture6.png)

Street-scale Comparison

最后我们对纽约布鲁克林（左）和香港九龙（右）的街道进行比较。首先我们从地图和对应的街景图中就可以看到，纽约布鲁克林拥有更高的绿化程度。平行坐标轴也是验证了这一个发现，布鲁克林的街道主要由绿化、天空、建筑、道路构成，而香港九龙的街景图主要由建筑和道路构成。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/12/Picture7.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/12/Picture7.png)[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/12/Picture8.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/12/Picture8.png)

## 总结

文章提出了一个探索和比较城市形态的可视分析系统，StreetVizor。未来工作将从街景图中抽取更多的语义信息，比如布告板和 POI 信息等，这样可以接入更多种类的数据，从多个角度分析城市形态。
