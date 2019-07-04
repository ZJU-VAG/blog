---
title: "ColorMapND: A Data-Driven Approach and Tool for Mapping Multivariate Data to Color"
tags: ["论文评述", "报告"]
date: 2019-05-10
author: 顾宇辉
mathjax: true
---

论文：ColorMapND: A Data-Driven Approach and Tool for Mapping Multivariate Data to Color

作者：Shenghui Cheng, Wei Xu, Klaus Mueller

发表：IEEE TVCG 2018

## 动机

目前为止几乎没有支持将多元数据到颜色的研究，已有的一些方法能够将低维数据映射到颜色，但只支持2~3个变量。

## 系统界面

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/gu3.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/gu3.png)

系统由四个视图构成，Color Legend（本文方法生成的调色板）， Pseudo Colored Plot（着色图），Local Enhancement（对选择区域进行对比度增强）和Channel View（对单个属性分布着色）。

## 基础框架

### 基本任务

1. 数据样本间的相异性可以通过颜色来感知。
2. 属性间的相异性可以通过颜色来感知。
3. 将数据样本与属性之间的关联表示为可感知的颜色标记

### 色彩映射

本文的多元数据映射到颜色的方法 简单说就是 将数据点嵌入到Radviz空间，在根据嵌入点的坐标 计算得到相应的色彩值。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/gu4.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/gu4.png)

### 解决方法

1. 任务一和任务三可以通过RadViz来解决，由于Radviz的特性，数据样本 越相似，布局位置肯定越接近；数据样本某个属性的值相对越高，它与边缘上的属性点位置也会越近。任务二通过一种新的基于相似性的属性排序和间距来解决，通过哈密尔顿回路 对属性进行排序  ，根据属性相关性 确定 间距。

   

   将优化后的RadViz显示器 与 等形状的彩色地图融合，形成ICD（circular interactive multivariate color mapping display）。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/%E5%9B%BE%E7%89%875.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/图片5.png)



2. 三大基本任务中相异性都需要通过颜色来感知， 这一过程的基础是需要一个精确的色彩空间。这个色彩空间需要符合以下3点要求：

   a. 感知均匀；

   b. 圆盘形状；

   c. 颜色空间的色调饱和度切片应该是等亮度的。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/gu5.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/gu5.png)

CIE HCL (Hue Chroma Luminance)符合了以上要求，但在显示器所用的sRGB色彩空间环境下只能显示部分色彩，因此需要在可见部分中找到最大直径的CIE HCL切片来作为ICD中使用的色彩空间。

## 其他功能

### 多元着色插值

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/gu7.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/gu7.png)

Adaptive kernel density estimation（AKDE）是核回归（kernel regression）方法的一种，是使用核函数对数据进行非参数估计（nonparametric estimation）的回归模型。本文对着色图根据数据样本进行AKDE插值讨论了三种策略：

1. 先着色，后插值（效果不好，颜色偏差）
2. 先插值，后着色（布局过程需要不断迭代，初始位置丢失，代价昂贵）
3. 先插值，根据插值计算权值来着色（Nadaraya-Watson回归）

### 处理大规模数据

当数据样本过多时，会造成ICD过于密集遮挡调色板的问题。本文使用了hashmap采样来解决这个问题，既解决了遮挡色板的问题，又能保持整体分布。下图分别为原始、降采样和hashmap采样三种效果。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/gu8.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/gu8.png)

 

## 案例分析

### America’s Mood Map

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/gu1.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/gu1.png)[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/gu2.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/gu2.png)

从华盛顿和俄勒冈州来看，这两个州的人性格非常相似，但与相邻的加州却有很大的不同，主要的区别是外向。另一方面，蒙大拿州是一个相对“正常”和“和平”的州——它在所有属性上几乎是平等的，值也很低。

## 总结

- 通过ICD，可以得到多元数据的着色方案。
- 颜色能在一定程度上表现数据样本的组成和相关性。
- 颜色对数据相关性的表达未定量地评估。
- HCL空间和sRGB空间不能完美覆盖。