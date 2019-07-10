---
title: "[论文快速浏览]SCIVIS 2014: Video and High Dimensional Data"
tags: ["论文评述"]
date: 2014-11-13
author: 丁治宇
mathjax: false
---

文章列表（本 section 有 5 篇文章，4, 5 两篇暂时没有 full paper release 出来）：

1. 《A Structure-Based Distance Metric for High-Dimensional Space Exploration with Multi-Dimensional Scaling》
2. 《The Impact of Interactivity on Comprehending 2D and 3D Visualizations of Movement Data》
3. 《GazeVis: Interactive 3D Gaze Visualization for Contiguous Cross-sectional Medical Images》
4. 《An Approach to Supporting Incremental Visual Data Classification》
5. 《Glyph-Based Video Visualization for Semen Analysis》

## 《A Structure-Based Distance Metric for High-Dimensional Space Exploration with Multi-Dimensional Scaling》

本文主要针对传统 MDS 方法结果和平行坐标结果不 match 的问题，基于 Structural Similarity Index （SSIM）方法，设计一种新的 metric，用于优化 MDS 结果。

使得 MDS 结果和平行坐标结果更加一致。

图 1 是第一个应用实例，eMDS 是传统 MDS 投影结果，sMDS 是本文方法。

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/11/case-study-1.bmp)

<center>图一</center>

作者首先将 9 维的高维数据分成两个类投影到低维空间，颜色映射为淡蓝和洋红色。e 是 a 和 b 对应的平行坐标结果。从 e 可以看出，两类数据在第 4 维属性上有了较大差异，因而，作者从第 4 维的属性出发，使用他提出的 metric 优化了 MDS 结果，使得 MDS 结果，从 a 变成了 b。其次，单独观察淡蓝色的类，其平行坐标结果如 f，将该类细分成两个类，颜色分别着色为黄色和淡蓝色。原始 MDS 结果如 c，两类数据 overlap 较多。然后坐着观察 g，发现在第 5 维度上两类数据差异较大，于是从该维度属性出发，将 MDS 结果优化为 d，淡蓝色和黄色数据类明显分离开。h 是将平行坐标 polyline 变化成均值条带进行表达的结果。更有利于观察不同数据的异同。

图 2 是另一个 case study，图 a，b，c 的分析和展示过程如图 1 中例子，可见相对 a，b 和 c 的结果更加 match。

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/11/case-study-3.bmp)

<center>图2</center>

d 和 h 中，都是先选择一个中心点，然后以一定半径扩展为一个圆，如是选定 3 个数据区域，着色为三种颜色。e 和 g 都是对各自对应的另一种 mds 方法中着色圆形区域的数据点的直观展示，以显示两者之间（g&e,g&h）没有一一对应关系。

f 是对 d 的平行坐标结果，i 是对应 h 的平行坐标结果。可知，i 和 h 的组合更加 match，f 对 d 则不是很 match，例如，淡蓝色部分区域在 f 中几不可见，三个区域数据混合严重，但是实际上由 d 可知，三个区域是相互分离的。而在 i 中，情形和 h 展示的较一致。

---

## 《The Impact of Interactivity on Comprehending 2D and 3D Visualizations of Movement Data》

在 2D（x，y）空间中展示 spatio-temporal 数据（如 GPS）容易导致 overplotting，从而丢失信息。将时间信息当成第三维度，在 3D 空间中展示，容易去除空间轨迹的 overlapping。然而，已有的实验无法很好地证明后者比前者更有优势。 本文的主要贡献在于：本文设计了很好的对比实验和任务，分析两者的优缺点。尤其是，发掘了交互在两种方法上对于可视化的结果的影响，有助于后人更好地理解和应用这两种方法。

本文是一个 task design 和 user study 类型的文章，因此，我们不做详细叙述，感兴趣读者可以细读该论文以参考 task 和 user study 的设计。

---

## 《GazeVis: Interactive 3D Gaze Visualization for Contiguous Cross-sectional Medical Images》

本文针对从以下问题，即：连续的多张医学切片图像中捕获医生的眼动数据，抽取眼动模式，并对其进行有效的可视化，此类研究很少。针对上述数据，本文提出并实现了一个交互的 3D gaze 数据可视化系统 GazeVis。提出了 gaze data 的一种新的表达形式： gaze field。

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/11/QQ%E6%88%AA%E5%9B%BE201411121825022.jpg)

<center>图3</center>

图 3 是 gazeVis 的系统界面，左边四个 view 是 2D 和 3D 的可视化展示窗口，右边是传输函数等控制界面。

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/11/QQ%E6%88%AA%E5%9B%BE20141112185504.bmp)

<center>图4</center>

图 4 展示的本文的核心技术点，将 gaze data 通过高斯核卷积转化为一个连续的 gaze field。

最后将这个 field 和作为上下文的 volume data 一起进行可视化（体绘制）

结果如图 5 和 6 所示

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/11/QQ%E6%88%AA%E5%9B%BE20141112191958.bmp)

<center>图5</center>

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/11/QQ%E6%88%AA%E5%9B%BE20141112192007.bmp)

<center>图6</center>

图 5 左图和右图分别是调整了 opacity 映射的结果，图 6 则分别为改变高斯卷积参数的结果。

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/11/QQ%E6%88%AA%E5%9B%BE20141112192307.bmp)

<center>图7</center>

图 7 是 12 个不同级别的医生的 user study 的结果，从左到右是专家级，一般，入门级医生的 gaze 数据可视化结果。可以看出，入门级的医生在观察这类数据时，没有经验，因此眼动是接近噪音分布，没有规律可循的。而专家级的就很有规律，并且无效数据很少。一般的医生介于两者之间。
