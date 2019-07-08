---
title: "Towards Better Analysis of Deep Convolutional Neural Networks"
tags: ["论文评述", "报告"]
date: 2017-05-05
author: 李宗壮
---

## 简介

首先介绍一下CNN（卷积神经网络）。CNN是一种特殊的神经网络，一个标准的CNN由一系列的层组成，包括卷积层，pooling层，全连接层等。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/05/12.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/05/12.png)

深度卷积神经网络已经在很多领域都有了突破性的表现。然而高质量深度模型的开发伴随着大量的尝试和错误，也并不能清楚的理解深度模型工作的原理。因为它难以理解的函数和并不清晰的工作机制，深度卷积神经网络一直被视作是黑盒模型。

因此，本文提出用可视化的方法帮助研究者更好的理解、判断和调整深度卷积神经网络。



而目前有两个主要的难题阻碍着研究者去理解和分析深度CNN

1. 一个CNN可能包含十几乃至100多层（深度），每层又会有成千上万的神经元（广度）

2. CNN包含许多组件，它们的值和作用难以很好的理解



## 相关工作：

已有的方法可以分为两个大类，code inversion和activation maximization

Code inversion 是从一个特定层的激活向量合成出一张照片

Activation maximization 旨在找出是的给定的神经元最大激活的图像。



总体来说，需要设计一个工具来满足以下三个需求

- Understanding： 学习网络结构的影响
- Diagnosis：诊断一个未能收敛的训练过程
- Refinement：发现提升模型的潜在方向



## 系统概览

根据上面的需求，促使开发一个可视化系统系统包含如下几块

- 一个DAG的结构，把一个卷积神经网络转换为有向无环图以及把神经元和层进行聚类来进行概览
- 一个神经元聚合可视化模块用来揭示每个神经元的多个方面
- 一个双向聚合边绑定技术来减少连接数量众多引起的杂乱
- 一个交互模块提供一系列的交互，例如交互式聚合结果修改和显示调试信息的需求



先来看一下系统的总览

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/05/2.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/05/2.png)

接下来是几个模块：

**DAG模块**

为了更有效的展示一个大的CNN，首先把相邻的层聚合起来

接下来把内层作用相似的点聚合起来。假定有相似激活的点有相似的作用。

两种聚类方法：K-Means和MeanShift

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/05/3.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/05/3.png)



对神经元聚类的可视化效果如下。其中应用了自定义的一种矩阵包装算法和矩阵列重排序算法。神经元之间的联系经过双向边聚类变成了类之间带有权重的边，并进行了绑定。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/05/41.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/05/41.png)



## 案例分析

选取了两个经典案例。

### **案例一**

经过对一系列深度广度各不相同的卷积神经网络的可视化，对卷积神经网络的结构的影响进行了研究。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/05/5.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/05/5.png)

 

### 案例二

对一个失败的收敛过程进行了分析。从可视化系统中发现问题，层层排查最终确定问题，修改网络，实现收敛，得到了不错的结果。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/05/6.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/05/6.png)

 

## 总结

作者的两个心得：在专家们使用到原型之前，有时他们也并不清楚他们具体想要的是什么效果；使用专家感兴趣的数据对于深入研究是至关重要的。

局限性：首先，CNNVis并不能可视化那些不能转换为有向无环图形式的深度模型；其次，激活矩阵的可扩展性有限；第三，这个系统有一个学习曲线，需要专家花一到两小时来彻底熟悉它的可视化编码和交互

本文的创新性在于以可视化方法帮助理解分析深度模型，对于专业人员是很好的辅助工具，有很好的参考价值。