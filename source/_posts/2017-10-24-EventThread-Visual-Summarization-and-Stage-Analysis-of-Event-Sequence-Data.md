---
title: "EventThread: Visual Summarization and Stage Analysis of Event Sequence Data"
tags: ["论文评述", "报告"]
date: 2017-10-24
author: 赵喆
mathjax: true
---

论文：EventThread: Visual Summarization and Stage Analysis of Event Sequence Data

作者：Shunan Guo, Ke Xu, Rongwen ZhaoDavid Gotz, Hongyuan Zha, and Nan Cao

发表：VAST 2017

## 简介

本文提出了一种对事件序列数据进行可视化概括和阶段分析的技术，并实现了一种全面而集成展示和分析数据的新型可视化系统。

## 动机

事件序列数据是的是在一段时间内发生的一系列事件，分析事件序列集合可以得出语义上重要的顺序模式。目前已经有许多分析和可视化技术来研究这种数据形式，但仍存在一些问题：

1. 使用统计分析方法来提取明确匹配的事件模式，无法获取相似但不相同的事件序列的潜在集群。
2. 难以将大规模异构事件序列数据转换为统一数据模型。
3. 对提取的结构没有做详尽的语义解释。
4. 对用户调整参数验证实验的支持度不够高。

因此，我们引入了EventThread，用于视觉总结大规模和高维事件序列数据。

## 系统设计

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/%E5%9B%BE%E7%89%871.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/图片1.png)

主要分为预处理模块，分析模块和可视化模块。

1. 数据转换和分析过程

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/%E5%9B%BE%E7%89%872.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/图片2.png)

数据过滤：真实事件序列数据包含大量事件类型，分布稀疏且频率有限。实现中使用n-gram（n = 1,2）统计模型将TF-IDF得分低的事件视为噪声去除。

2. 序列比对：移动事件序列，使其沿着共同的起始时间轴对齐。

3. 阶段折叠：将对齐的事件分成多个阶段。

4. 数据建模：事件序列数据可以由三路张量$\mathscr{X} \in R_{+}^{M \times T \times N}$表示。其中M，T，N分别表示事件，阶段和实体的数量。$\mathscr{X}_{i j k}$表示在第k个实体的j阶段发生的第i个事件。

5. 汇总算法：上步中我们得到了表示事件序列数据集的三路张量χ，利用张量分解得到潜在的序列模式，即线程。转化成如下的优化问题：

$$
\min \|\mathscr{X}-[\lambda ; \mathbf{A}, \mathbf{B}, \mathbf{C}]\|^{2}
$$

$$
\mathbf{B}^{T} \mathbf{B}=\mathbf{I}, \mathbf{A}, \mathbf{B}, \mathbf{C} \in R_{+}^{[N, T, M\} \times K}
$$

表示张量CP分解算法，产生N*K，T*K和M*K的因子矩阵A，B和C，K是表示潜在线程数的输入参数。使χ与这些分量的乘积之间的误差最小化，A，B和C分别表示线程在事件，阶段和实体上的分布。

正如文本分析从文档集合中导出主题一样，我们需要从事件组成的序列集合中导出潜在的线程。不同与主题建模的是三路张量允许对潜在线程进行阶段、事件和实体三个方面的解释。

## 可视化设计

### 用户界面

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/%E5%9B%BE%E7%89%878.png)

### 线程视图

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/%E5%9B%BE%E7%89%879.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/图片9.png)

同一阶段的不同线程内的段可以进一步集成到潜在阶段类别中，提出一种布局算法来放置线程。

布局算法：首先通过均衡显示屏的宽度来确定阶段的x坐标。再基于每个阶段的事件相似性组合线程，同时最小化相邻阶段相同线程的垂直距离以减少线程交叉。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/%E5%9B%BE%E7%89%8710.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/图片10.png)

在给定阶段的垂直距离小于等于阈值的相邻线程将在相应的阶段内聚集在一起。

## 案例分析

1. COPD患者医疗事件分析

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/%E5%9B%BE%E7%89%8711.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/图片11.png)

2008年至2014年捕获的7年纵向医疗数据，包括5,804名慢性阻塞性肺疾病患者队列。数据集包括代表诊断，程序和遭遇（即入院和出院事件）的时间戳事件。每个线程代表某个队列的典型临床路径。

2. 车辆维护分析

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/%E5%9B%BE%E7%89%8712.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/图片12.png)

该数据集包含来自1,112辆汽车的近5000个维护记录。每个记录包括汽车的身份证件，维护类型，特定的维护项目和项目的描述。数据处理后，生成了七个潜在线程，代表各种车主的维护习惯，每个阶段代表汽车上的又一轮维护。

可以看出所有线程在后期都趋于更多的修理和零件更换。

3. 学术行为分析

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/%E5%9B%BE%E7%89%8713.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/图片13.png)

数据集包含23年以来的40个人的记录，并手动将事件分为3个高级类型，包括培训，发表和晋升。

发现教授更有可能发布会议论文。从线程1在最后阶段与线程2合并可以看出，副教授获得资历后，其与教授行为之间的相似性日益增加。

## 局限性

1. 创建的阶段长度是固定相同的。

2. 潜在序列模式的数目是手动定义的。