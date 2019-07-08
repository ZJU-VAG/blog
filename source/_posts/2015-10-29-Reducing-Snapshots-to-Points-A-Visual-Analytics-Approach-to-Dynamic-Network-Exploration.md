---
title: "Reducing Snapshots to Points: A Visual Analytics Approach to Dynamic Network Exploration"
tags: ["论文评述"]
date: 2015-10-29
author: 朱标
mathjax: true
---

论文：Reducing Snapshots to Points: A Visual Analytics Approach to Dynamic Network Exploration
作者：Stef van den Elzen, Danny Holten, Jorik Blaas, Jarke J. van Wijk
发表：VAST 2015

## 简介

动态网络的可视化方法可以分为Animation (time-to-time) 和 Small-multiple (time-to-space) 两类。对于前者，用户每一时刻只能看到一帧，前后内容需要用户去记忆、理解，往往需要来回观看很多遍才能粗略理解动态网络的变化过程，给用户带来了很大的认知负担；对于后者，将不同时刻的网络进行并排罗列，由于屏幕空间有限，很多时候并不能将所有时刻的网络同时进行展示，且难以进行网络动态变化模式的发现。本文提出了一种对动态网络进行二维投影的方法，可以将每个动态网络表示成一张静态的node-link图，每个node代表某个时刻的网络，link连接了相邻时刻的node，可以有效地帮助用户发现稳定状态(stable state)、重现状态(recurring state)、异常拓扑(outlier topologies)及分析网络状态间的转移过程。

## 本文方法

下图是本文方法的工作流程：

1. 离散化：原始数据由一系列时序的事件组成，每个事件均发生在某两个个体之间。方法的第一步是将原始数据进行离散化，生成一些离散的snapshots。具体做法是生成一些连续的时间窗（为了最后投影结果的连续性，时间窗口可以有部分重合），将每个时间窗内的所有事件转换成一个等价的网络，网络里的节点和边分别是这个时间窗内出现过的节点和边，并将每条边在这个时间窗内出现的次数当做该边的权重。

2. 向量化：为了进行投影，需要进行向量化将每个snapshot转换成一个高维的向量。具体做法是先将snapshot表示成邻接矩阵，然后将邻接矩阵转化成一个高维向量，当然这里还可以往该向量里加入一些额外的属性，比如该网络中节点平均的度（degree）等。

3. 投影：经过前面两个步骤，我们已经得到了一些列时序的高维向量，只需要对其进行二维投影即可。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/10/rstp_workflow.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/10/rstp_workflow.png)



本文方法本身比较简单，都是一些已有的方法的组合，但本文针对方法的每个步骤，都进行了全面、细致的讨论，讨论涉及的内容有：

1. 离散化：讨论了时间间隔、窗口大小的选择对最终投影结果的影响

2. 向量化：讨论了多种归一化方法（binarization，Min-max和Z-normalization）对投影结果的影响

3. 投影：讨论了不同的投影方法（PCA，MDS和t-SNE），不同的距离度量（DDQC，KS）。并讨论了在PCA投影时，将其中一个轴替换成时间轴，可以更清晰地展示网络随时间的变化。

4. 可视化：讨论了多种节点颜色编码方案，snapshots间的动画切换效果等



## Case

Case 1：

这是一个作者生成的动态网络数据，从左图中，我们可以看到有四个稳定态，颜色由浅到深编码了时间的推移，其中左下方的是反复出现的稳定态，可以看到它包含了多种不同颜色的节点。(a)是将时间作为横轴的PCA投影，可以明显看到4个不同的稳定态，并且最下方的稳定态重复出现了三次。(b)是将左图中PCA投影方法替换成非线性投影的效果，可以看到不同的稳定态被很好地区分，但是稳定态之间的转移过程消失了。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/10/rstp_case11.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/10/rstp_case11.png)





Case 2：

这是一个真实的数据集，记录了一个学校里180名学生在7个工作日内面对面接触的数据，一共有45,047条记录。最终生成的动态网络里面有180个节点、10,104条边，作者取的时间窗是60分钟，前后时间窗的重叠部分达到了54分钟，最终生成了2015个snapshots。



下图左边是PCA投影的结果，其中左边没有进行向量的归一化，而右边进行了 Z-normalization 的归一化。从左图中，我们可以看到作者标出的对应每一个工作日的折线。中心有一个稠密的投影区，也就是文中说的稳定态，作者通过进一步查看发现那对应了夜晚的时段，即学生们放学后相互之间见面就很少了，网络结构也就变得稀疏、相似了。从右图中我们看到一些离群点变得更明显了，离中心区域近的点的网络结构都比较稀疏，比较接近夜晚时段的状态。而离中心远的离群点则网络结构相对稠密，对应学生间碰面较多的时段。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/10/rstp_case2_1.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/10/rstp_case2_1.png)

下图是使用非线性投影方法投影的结果，相比于PCA投影的结果，每个工作日的投影结构更为明显。左图和右图的区别在于颜色编码不同，左图编码的是从19日到27日，右图编码的是每天的早6点到晚6点，可以更清楚地分析每天的活动规律。可以看到每个工作日基本上是连续的一条轨迹，其中每一天的轨迹都会在几个基本固定的时刻断开，作者分析是由于上课、午休等导致的。另外，在右图中可以看到，周二和周三下午有异常，点的分布和当天的轨迹不连续，作者发现这是由于周二下午只有一节课，而周三下午有一场考试导致的。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/10/rstp_case2_2.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/10/rstp_case2_2.png)



下图左边是将横轴替换成时间轴的PCA投影，可以看到规律的七个工作日的网络变化，早上开始逐渐变活跃，中午的活跃状态会降低，下午又会重新变活跃，直到晚上恢复完全的平静。而双休日由于没有数据，都处于平静的状态。右图是z-normalization归一化后进行非线性投影的结果，可以看到白天的活动都被分成了基本等长的一些小段，作者表示这是由于学校每次课都持续一个小时左右。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/10/rstp_case2_3.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/10/rstp_case2_3.png)

## 总结

这篇文章是VAST 2015的Best Paper，而文章的idea及文中用的方法并不复杂，我认为它获得这一荣誉的原因有：

1. 选题好，动态网络的分析是当前较为热门的问题，本文方法虽然简单，但是确实较为有效地解决了状态发现、状态转移分析等问题。

2. 虽然方法简单，但方法所涉及到的方方面面均进行了细致的讨论，整个工作做得相当完整。

3. 虚拟数据和实际数据相结合。虚拟数据的结果更为漂亮，比较能吸引人，也更容易让人理解方法本身。真实数据的分析进一步证明了方法的实用性。