---
title: "Vol2velle Printable Interactive Volume Visualization 可打印的交互式体可视化"
tags: ["论文评述", "报告"]
date: 2016-12-27
author: 潘嘉铖
mail: panjiacheng@zju.edu.cn
mathjax: true
---

论文：Vol2velle: Printable Interactive Volume Visualization 可打印的交互式体可视化

作者：Sergij Stoppel and Stefan Bruckner，university of Bergen

发表：TVCG 2017

## 1. 简介

因为纸质媒体便宜、可回收、易使用等特点，在很多场景中，我们会经常将体可视化打印到纸质媒体上，但是在可视化结果硬拷贝（如打印）时，【交互性】受到一定的损失，而我们知道，在数据可视化中，特别是体数据可视化中，交互特性非常重要，于是作者提出一种打印数据可视化的方法，并且保留了一定的交互性。

作者参考了传统的 Volvelle，提出了一种 Volumetric Volvelle（Vol2velle）。Volvelle 是一种可旋转的轮盘，早在公元前 1000 年，就已经开始使用，一直被设计用来做一些科学可视化，如行星轨迹观察等。人能够直接和 Volvelle 进行交互，这也有助于加深理解和记忆，而根据 IKEA 认识偏见效应，人会对自己参与制作的工具有更高的评价这种认识偏见，使得 Volvelle 的意义更加突出。

但是传统的 Volvelle 生产过程中，非常费时费力，往往从设计到制造要花几周时间。于是作者提出了一个用于设计和渲染 Volvelle 的系统。

## 2. 贡献

首次实现了自动化生成可交互的纸质媒介上的可视化：

主要工作如下：

1. 分析了纸质媒介的设计空间和约束条件
2. 提出了参数化和编码体可视化的策略
3. 生产了一个半自动生成 Vol2velle 的系统

## 3. 相关工作

### 图示可视化方面

1. **Ghosted Views**: Importance-driven feature enhancement in volume visualization（2005 TVCG 170）

    去除或抑制场景中不重要的部分，从而使得更重要的信息呈现出来

2. **Cutaways**: Illustrative context-preserving exploration of volume data(2006 TVCG 117)

    针对前一篇文章的改进，关于高透明度图像如何去除重叠又能减少上下文信息丢失的工作

3. **Exploded Views** for Volume Data（2006 TVCG 121）

    体可视化中，关于如何分解视图，解决遮挡问题

交互和参数定义方面

1. **Design Galleries**: A general approach to setting parameters for computer graphics and animation（1997 ACM 584）

    定义了一个计算机图形应用中的接口库，通过调整参数来达到设计目标

2. Mastering Transfer Function Specification by using VolumePro Technology

    半自动传递函数操作的用户界面范例，用来给用户提供意见和预览

3. High-Level User Interfaces for Transfer Function Design with Semantics（2006 TVCG 117）

    为高级用户提供用户界面，集成了予以模型，为专门的可视化问题提供语义信息，以此来设计传递函数

4. Image graphs—a novel approach to visual data exploration（IEEE Visualization 105）

    一个显示 交互中，参数变化如何影响结果的可视化系统

### 非传统的可视化界面

1. **PaperWindows**: Interaction Techniques for Digital Paper （2005 ACM 222）

    对物理纸张进行投影，通过运动不准系统来跟踪纸张的运动和形状从而产生交互

2. **PaperLens**: advanced magic lens interaction above the tabletop（2009 ACM 110）

    类似于光学透镜的一种交互方式

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/12/image9.gif)

### 无电子设备的物理可视化

1. **Activity Sculptures**: Exploring the Impact of Physical Visualizations on Running Activity（2014 TVCG 27）

    数据雕塑，将数据赋予物理形式

    ![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/12/image10.png)

2. An interaction model for visualizations beyond the desktop（2013 TVCG 43）

    提出了一个桌面之外的可视化交互模型，原始数据被处理成可视化，然后渲染到物理世界，用户直接操作就可以更改数据

    ![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/12/image11.png)

### 纸质物理可视化的生成

1. **Popup**: automatic paper architectures from 3D models.（2010 ACM 60）

    3D 纸质建筑，利用自动算法，生成用户指定的模型的纸张结构

2. **Interactive Gigapixel Prints**: Large Paper Interfaces for Visual Context, Mobility, and Collaboration

    大尺寸的纸质品可以拥有大尺寸和高分辨率，并且同时有较强的移动性和协作性，文中工作介绍了交互式的打印十亿像素

## 4. Volvelle 结构介绍

### 基本结构

Volvelle 最基本的构成是由三个层次，固定的表面层，可旋转的轮盘，固定的基座组成。

在基础结构上，可以增加多个可旋转的轮盘，但是增加多个轮盘，能展示图像的空间也会越来越小，而且使用者学习认知和操作的复杂度也会增加。虽然利用透明媒介来展示图片可以缓解空间缩小的问题，但是却无法解决复杂度增加的问题。

### 基本模型

根据材料的不同，Volvelle 的模型又可以分成两种：纸质模型和透明模型。

纸质模型就是普通的，用纸片打印并制作而成的；透明模型的轮盘，则使用透明的胶片制作而成。目的是为了叠加多张图像。透明视图的一个问题是：所呈现的图像必须要遵循正确的遮挡顺序来进行叠加，作者采用了利用每个层次离观察者最近的距离来进行排序。

### 编码方式

作者提出了信息（主要是 图片）在轮盘上的两种基本的布局方法以及它们的混合使用：

左图是沿半径的同轴编码，中间是沿着圆周的镜像编码，右图是两者的混合使用。

沿着圆周，可以编码一个有序的循环变量；而沿着半径，我们可以编码一个顺序变量。

### 窗口布局

针对不一样的编码方式，我们也需要采用不一样的窗口布局，比如对于验证圆周的镜像编码方式，我们就需要采用下面左图的方式，而针对混合编码或者同轴编码，我们需要用下面右图的方式。

### 其他交互方式

文章还提到了两种增加的交互方法，一个是利用 slide chart 的方式来多编码一个标量参数，slide chart 是一种可以抽插的纸条，可以多展示一个参数：

另外一种方法是利用，changing picture option 的方法，可以编码一个布尔变量，用来切换两种不同的视图。做法是通过将两张裁剪好的轮盘叠在一起，当底下的轮盘旋转的时候，会插入到上面的轮盘：

### 采样过程

生成过程的关键之一，就是如何进行采样。一般有以下三种采样方法，第一种方法是均匀采样，这种采样方法，刚好能编码完整的二维数据，但是存在空间浪费（因为外圈空间被浪费）；第二种方法是密集采样方法，这种方法能有效利用空间；第三种方法是锥形采样，往往用在有一个偏移量存在的状况（比如有一个公共的大窗口）

上面提到的是，圆周方向的采样策略，而半径方向的采样，也同样存在问题，比如，在均匀采样的方法下，我们往往会采样到很多相似的图片，因为沿着半径方向的参数并不一定是线性的。所以我们需要用一种非线性的方法来进行采样：以下就是三种不同的采样方法，第一行采用了均匀采样，就造成了结果高度一致的情况。

## 5. 应用举例

利用半径方向和圆周方向两种不同的编码方式混合编码的一个例子（手部 CT 扫描数据的可视化）：

![1561970398314](https://jackie-image.oss-cn-hangzhou.aliyuncs.com/19-07-01/1561970398314.png)

利用 changing picture option 来切换千足虫外表面视图和切片视图的一个例子：

![1561970329405](https://jackie-image.oss-cn-hangzhou.aliyuncs.com/19-07-01/1561970329405.png)

人体头部 CT 扫面数据利用透明模型来进行可视化的一个例子：

![1561970367667](https://jackie-image.oss-cn-hangzhou.aliyuncs.com/19-07-01/1561970367667.png)

## 6. 相关讨论

目前这个系统仍然存在以下问题：

1. 图片大小和采样数量之间权衡，根据经验只能放 5-25 图
2. 多个轮盘叠加能编码更多信息，但是却会增加复杂度
3. 打印机基本都没办法打印白色
4. 最终成品的质量和打印机有关系
5. 透明介质上，只有黑色才能完全不透明，所以导致了渲染和实际打印的结果不一样
6. 当前的透明模型的排序方法不是最优的
