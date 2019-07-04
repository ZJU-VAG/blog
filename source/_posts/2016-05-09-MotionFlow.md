---
title: "MotionFlow: Visual Abstraction and Aggregation of Sequential Patterns in Human Motion Tracking Data"
tags: ["论文评述", "报告"]
date: 2016-05-09
author: 胡万祺
mathjax: true
---

论文：MotionFlow: Visual Abstraction and Aggregation of Sequential Patterns in Human Motion Tracking Data

作者：Sujin Jang ; Niklas Elmqvist ; Karthik Ramani

发表：TVCG 2016

## 介绍

人体动作追踪数据（human motion tracking data）由体感装置Kinect捕获得到，包含多帧记录人体各个关节3D坐标的数据。这种数据的可视分析一直以来都是个难点，因为这种数据几乎是分布在无限的时间和空间范围上，而且包含的帧数较多，数据量大且数据结构异常复杂。这篇文章为了解决这个难题，提出了可视分析系统——MotionFlow（图1）。它将动作数据抽象成不同动作状态之间的转移序列，并用几个联动视图进行展现，方便用户发现和探索出一些有趣的动作模式。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/05/11.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/05/11.png)

<center>图1：系统界面</center>

系统的工作流程如图2所示。系统会先自动对每一帧的动作数据进行聚类，定义出一定数量的动作状态，并将原始的动作数据表达成这些动作状态之间的转移序列，然后用图和树的表达形式对这些序列进行可视化。用户在交互和探索的过程可调整聚类的参数，从而更新所有的可视化视图，也可以将发现的一些有用的动作模式抽取出来并做标注。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/05/21.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/05/21.png)

<center>图2：系统工作流程</center>

## 可视化设计

下面详细介绍下系统的可视化设计。首先作者设计了一种图符poselet来表示每种动作状态，如图3所示。图符中间用火柴人的方式表现该动作状态的平均动作，其余的动作以稍微浅一点的灰色绘制。每个火柴人是基于3D绘制的，可以用鼠标拖拽进行旋转，以从不同的角度查看火柴人的动作。图符周围的颜色编码该动作状态的方差，由绿到红分别表示方差越来越大。另外图符的左上角会标上该动作状态的序号。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/05/32.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/05/32.png)

<center>图3：动作状态图符</center>

作者采用了两种视图对动作序列进行可视化：Pose states graph（图4）和Pose Tree（图5）。Pose states graph采用力引导图的布局展示不同动作之间的状态转移，有向链接的粗细编码转移量的多少。然而在这个视图里并不能看出每个动作在时序上在不同动作状态的转移情况，所以作者提出了另一种视图Pose Tree，参照了字典树的表达方式，Pose Tree将动作序列以树的形式展开，并将每一个叶子节点所在的分支定义成一个动作模式。

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/05/41.png)

<center>图4：Pose states graph</center>

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/05/51.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/05/51.png)

<center>图5：Pose Tree</center>

图1（c）是Pose Tree的Treemap表达形式，每个矩形表示一个动作模式；图1（f）是一个动画窗口，用户选择某个动作状态图元的时候可以点击播放来查看整个动作的动画。

系统支持的交互包括：动态调整动作状态的聚类数量；动作状态的合并、拆分和锁定（图6），其中锁定的意思是强制保留某个动作状态，重新聚类时锁定的动作状态不会发生改变；抽取Pose Tree的子树，并新建标签页以标注的形式保存。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/05/6.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/05/6.png)

<center>图6：合并、拆分和锁定</center>



## Expert Review

文章最后用一个Expert Review验证了MotionFlow系统的可用性。他们邀请了六个博士生来参与访谈，其中三个研究手势交互设计、三个专门做动作轨迹数据的分析。首先作者给他们介绍了系统，并让他们自由试用系统；然后给他们提出了4个open-ended的任务让他们去完成：1、调整聚类参数，生成一系列动作状态；2、找出最常见的动作模式；找出最特殊的动作模式；3、找出觉得有意思的动作模式并用标签页保存。在每个任务完成之后都需要回答相对应的几个问题，最后再对使用系统的整体感受进行总结。整个Expert Review下来，MotionFlow得到了参与者的很多正面的评价（图7）。

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/05/7.png)

<center>图7</center>