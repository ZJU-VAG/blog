---
title: "MobilityGraphs: Visual Analysis of Mass Mobility Dynamics via Spatio-Temporal Graphs and Clustering"
tags: ["论文评述"]
date: 2015-11-29
author: 张天野
mail: zhangtianye1026@zju.edu.cn
mathjax: true
---

论文：MobilityGraphs: Visual Analysis of Mass Mobility Dynamics via Spatio-Temporal Graphs and Clustering

作者：Tatiana von Landesberger, Felix Brodkorb, Philipp Roskosch, Natalia Andrienko, Gennady Andrienko, and Andreas Kerren

发表会议：TVCG2015

了解人类移动的规律对于政策制定和城市规划有着至关重要的作用。移动数据集纪录了人们在不同时刻出现的位置以及人们在不同地点之间的移动流。分析移动数据的困难点在于比较不同时刻的空间位置（spatial situations）以及了解空间位置随时间的变化。传统的流可视化方法会造成大量的杂乱现象，同时现代的方法不支持长时间段下的分析复杂的移动数据。因此，作者提出了一种结合基于时间和空间的简化和可视分析的方法解决了以上问题。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/11/Picture1.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/11/Picture1.png)

首先，作者对于轨迹数据中出现的所有地点进行聚类，根据聚类的中心对当前轨迹范围（以伦敦为例）进行空间剖分[1]。从轨迹数据中抽取出基于有向图的时变流（time-varying flow）数据，其中节点是空间剖分得到的结果，边是节点之间流的统计。伦敦 twitter 数据在经过处理后得到 7d\*24h 个时间步下的有向图，包含 606 个节点，21727 条边。

正是因为过多的节点和边，造成流视觉上的混乱，过多的时间步导致无法进行比较长时间的比较。作者提出了基于时间和空间的简化方法，进一步抽取更为简单的图结构。通过空间聚类，减少布局上的杂乱现象；通过时间聚类，将具有相似空间位置的时间步聚成一类，进而比较时间步的长度。

如果先进行时间聚类，抽取某个时刻的时变流（有向图）特征向量将会达到 2 万维，对于聚类稳定性和时间是一个巨大考验，所以先有必要先进行空间聚类。空间聚类是把超图（supergraph，所有时间步的平均） ⟨P,L,T, W(P,T),M(L,T)⟩中的空间小区域聚类成大区域。空间聚类算法基于 DBScan，将相距较近并且相互间具有较强人流量的区域聚成一个类。

时间聚类是把刚才简化后的时变流抽取出特征向量。此时的时变流结构已经只有 42 个区域，394 条边，相对于 2 万维下降到原来的 1.8%，可以提高 kmeans 的聚类速度。

整个系统如下图所示，（a）日历视图，每一行表示一天的各个小时 颜色和下面的聚类对应（b）参数设置（c）kmeans 聚类中心的流图。节点大小编码区域集合内人数的平均或总和；边宽度编码区域集合间的平均流量；从暗到亮，处于右边（顺时针）的边表示从节点中出去。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/11/Picture2.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/11/Picture2.png)

同时用户可以对两个图进行比较。如下图所示，T3（左）和 T7（右）进行比较。其中节点大小由左边的网络决定，颜色是相对于左边的相对流量比，由蓝到白到红，分别是降低、不变和增加。从时刻表可以发现 T3（黄色）的时间是在凌晨，T7（淡绿色）是在工作时间，可以明显看出，几乎所有的节点和边都是偏红色的，说明工作时间的人流量比凌晨有所增加，这也符合人的正常规律。

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/11/Picture3.png)

与伦敦不同的是，阿比让城是一个多中心的城市，这主要是因为城市被水域所分割。简化后的流图类似于一只蝴蝶，中间一个较大的节点和西边和东边的节点有着强烈的连接。

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/11/Screen-Shot-2015-11-29-at-10.28.37-PM.png)

这个工作提出流一种概览轨迹数据的方法，同时考虑了时间和空间简化，所以我们可以实时调节参数。但也正是因为如此，丢失了个人的轨迹数据，只能从宏观上看出整个城市的移动图，不能从微观层面进行观察。

[1] Natalia Adrienko and Gennady Adrienko. Spatial generalization and aggregation of massive movement data. Visualization and Computer Graphics, IEEE Transactions on, 17(2):205–219, 2011.

[2] Tatiana von Landesberger, Felix Brodkorb, and Philipp Roskosch. Mobilitygraphs: Visual analysis of mass mobility dynamics via spatia-temporal graphs and clustering. 2016.
