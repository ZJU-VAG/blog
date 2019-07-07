---
title: "SketchPad_N-D: 一种基于手势的所见即所得的高维数据编辑方法"
tags: ["论文评述"]
date: 2013-12-30
author: 朱标
mathjax: true
---



论文: SketchPad_N-D:WYDIWYG Sculpting and Editing in HighDimensional Space
作者: Bing Wang, Puripant Ruchikachorn, and Klaus Mueller
发表会议: Vast 2013



为了测试高维数据可视化软件，或者为了证明这些软件的有效性，人们往往需要具有特定已知特征的数据，而这些数据在实际中往往不容易得到。本文基于平行坐标和 N-D ploygon ，提出了一种基于 sketch 的、所画即所得 （WYDIWYG） 的高维数据生成、修改/清洗方法，可以有效地创建、修改出一些具有所需特征的高维数据。



## 本文方法由两部分组成

1. 第一部分是一个平行坐标的视图，作者在平行坐标轴上定义了两个操作

    1. 通过在平行坐标轴上画一条代表概率密度函数的曲线来指定对应轴上数据分布情况，如下图所示。

       

       ![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2013/12/%E5%9B%BE%E7%89%871.png)

       

    2. 通过画一个四边形或者蝴蝶结形，分别指定相邻两个维度之间的正相关和反相关特征，如下图所示（这两个形状通过 4 个顶点进行指定，图中的数字表示 4 个点指定的先后顺序），相关程度可以通过滚动条进行调节。

       

       ![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2013/12/%E6%97%A0%E6%A0%87%E9%A2%98.png)

       

2. 第二部分是一个散点图的表示，分为轴向对齐、非轴向对其两种交互策略

    1. 轴向对齐的交互: 实际上就是一个大家所熟悉的散点矩阵，横纵维度就是 N 维数据的 N 个正交基（这里以 N=4 为例），如下图所示。在任意投影平面上，用户通过指定一个分布的范围（下左黑线框部分）以及该分部的中心（下左红线部分）来生成数据点，这些数据点满足:

       	1. 在该投影平面上的投影符合用户的指定
        	2. 在其他维度上均匀分部。

       然后用户可以通过本文提供的笔刷根据自己的需求在每个投影平面上擦除/添加上一些数据点，以得到一个满意的结果。这里需要指出的一点是，当用户在某个投影平面上擦去一些点的时候，其他投影平面上的点可能会相应减少，本文提供了自动、手动两种方式对受影响的数据进行修补，修补的前提是在用户进行过擦除操作的投影平面上，用户擦除过的区域上不会出现新的点。

       ![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2013/12/%E6%97%A0%E6%A0%87%E9%A2%982.png)

   	2. 非轴向对齐的交互

       和1类似，只不过投影平面可以由用户通过本文提供的 N-D touchpad polygon 进行任意指定，然后在相应的投影平面上进行相应的操作。

       

       ![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2013/12/%E6%97%A0%E6%A0%87%E9%A2%983.png)



## case study 1

用户通过非轴向对齐的交互生成了如下图所示数据，在最后的两个投影平面上，数据分别呈现了不同方式排列的 “ND” 字母。



![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2013/12/%E6%97%A0%E6%A0%87%E9%A2%985.png)



## case study 2

用户轴向对齐的交互指定了在 4 维空间中明显可以分为两类的一个数据，来验证 K-means 方法， (c) (d) (e) 三个图里面的红、黑分别表示 k-means 方法分出来的两个类，通过 (e) 可以清楚地看到， k-means 方法只在第 4 个维度上把两个数据分开了，而其余维度上都混在一起，没有很好分开。



![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2013/12/%E6%97%A0%E6%A0%87%E9%A2%984.png)



## case study 3

用户通过非轴向对齐的交互，任意指定投影平面对数据进行观察，然后手动移除 outliers



![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2013/12/%E6%97%A0%E6%A0%87%E9%A2%986.png)



## user study

最后，本文请了 8 个从未使用过该系统的用户进行测试，让他们在平行坐标中交互出特定的 feature ，用户普遍对该系统给出了肯定的反馈，且都在较短的时间内做出了相应的 feature 。



![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2013/12/%E6%97%A0%E6%A0%87%E9%A2%987.png)



## 未来工作

1. 为 sketch 加 curve-drawing 、 line-drawing 组件。
2. 对类别型数据的支持。



## 评述

本文中使用的可视化技术都是现成的，但是 sketch + visualization 结合得很好，用户交互起来非常直观，学习成本低，这个从 user study 里面就可以看出来。但是对于散点图部分的交互，尤其是非轴向对齐的部分，各个投影平面之间会出现 overlap ，在同时制作多个投影方向特征的时候，用户很难交互出一个自己想要的结果，也有可能用户想要的结果根本不存在（但是本文的方法不能给用户以足够的提示、引导，用户很难意识到这个问题）。























