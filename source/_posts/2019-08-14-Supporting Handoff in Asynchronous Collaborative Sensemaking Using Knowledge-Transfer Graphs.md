---
title: "Supporting Handoff in Asynchronous Collaborative Sensemaking Using Knowledge-Transfer Graphs"
tags: ["论文评述", "报告"]
date: 2019-08-14
author: 徐卫霞
mathjax: true
---

-   论文：Supporting Handoff in Asynchronous Collaborative Sensemaking Using Knowledge-Transfer Graphs
-   作者：Jian Zhao, Michael Glueck,Petra Isenberg, Fanny Chevalier, Azam Khan
-   发表：TVCG 2017( Best Paper Honorable Mention )

## 背景介绍

协同意义构建(Collaborative Sensemaking ) : 通过多人的沟通交流，弥补个人理解上的不足，得到对事件等更加全面的理解。

因为时间、地点、隐私等原因，在日常的协作中会出现异步协作意义构建的情况。可以通过可视化的方法对协作人员的工作过程可视化展示并进行管理、综合等，使得后来的协作者可以很好地对之前协作者的工作过程进行分析，交互式的系统可以使得协同工作更加的方便。

<img src='http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/8/14/09857d7f7e2c0421cb8e7186ddf8ee21c42ef225.png' style='zoom:50%'/>

由于无法直接沟通，协作者无法将自己的分析过程完全的传递给后面的协作者，使得异步协同意义构建时协作者间存在知识传递问题。本文解决的问题是在异步协作意义构建的场景下对知识的传递问题。

## 相关工作

涉及到的外部化(Externalization)方法包括：基于图的可视化、时间轴、注释空间（commentspace）。

可视化平台：CLIP 系统与本文系统相似，适用于协同意义构建的场景，但未解决在异地协同中存在的知识传递问题。

<img src='http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/8/14/24a7b2645f030e5ce4aa76f4b94e27cc486cc620.png'/>

CLIP 系统的论文如下：N. Mahyar and M. Tory. Supporting communication and coordination in collaborative sensemaking. IEEE Transactions on Visualization and Computer Graphics, 20(12):1633–1642, Dec. 2014. doi: 10.1109/TVCG.2014.2346573。

## 本文工作

提出了**KTGraph**--- 一种在异步协作意义建构中支持知识传递的可视化方法

贡献：

1. 一种支持调查者间知识传递的新型协同可视化工具 KTGraph
2. 基于对协同研究和意义构建的研究，为支持知识传递提供了设计要素。
3. 两阶段的用户研究，以多方面评估我们的技术在文档分析场景中的应用情况

## 应用示例

FBI 怀疑小镇 Alderwood 可能存在政治阴谋，需要从大量的新闻文章和其他信息中分析得到小镇中存在的异常情况(VAST 2006 challenge 的题目，对数据集有部分缩减)。其中本文中用到的数据集为新闻文档和图片等，具体格式如下图。需要通过异步协同的方式对小镇中存在的异常情况进行分析，保证调查者间充分的知识传递。![](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/8/14/fe19bb5c186e27e8308b5d35766eabb15ff4eebb.png)

## 设计要素

基于之前对异步协作意义构建的研究，提出了以下四点设计要素：

G1：支持交互式外化(externalization)

G2：编码分析依据(Encode analytic provenance), 将得出的结论与对应的依据进行映射

G3：促进共同理解(facilitate common understanding), 通过标签等组件显式的表达调查的进展和过程

G4：提供交互和分析依据(Provide interaction and analytic provenance), 提供之前调查者的调查过程和进度

## 系统

##### 主要技术

1. 通过引用、注释、标签等进行可视化，使得早前的意义构建更加的详细
2. 对所有元素都可以通过标签进行标记，表达调查者的一些原始猜测，显式的表达调查结果。
3. 通过添加时间轴等对整个调查过程进行可视化，并提供对调查历史的回放使得之后的调查人员可以了解之前的调查者如何对调查过程进行编码和可视化，是一种隐式的沟通。

##### 系统概览

![1565763517427](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/8/14/fa4040d2050ed0c00dda079642e37aa321add291.png)

A: Graph panel , 调查人员通过引用、注释等组件对调查过程进行可视化(G1)，通过自定义标签对调查过程中发现的一些知识进行标记(G3)。

B: Comments panel , 对 graph panel 中的一些节点或边添加注释，注释内容较为自由，包括解释原因、提出假设等(G3)。

C: Dataset panel , 对数据集进行可视化，包括关键词检索(G1)、为 graph panel 中的假设与文档建立映射(G2)等。

D: Timeline panel , 对调查过程进行可视化，提供对调查过程的回放等进行知识传递(G4)。

## **User Study**

实验主要分为知识传递的性能、外部化的多样性和偏好两个阶段。创建 baseline 系统对 KTGraph 的实际性能进行对比测试，baseline 包括 graph、comment、dataset Panel 和用户交互。被试为具有计算机科学或工学背景、英语熟练、对上述案例陌生的大学毕业生和专业研究人员，每个被试只参与其中一个阶段的实验。

### 知识传递的性能

##### 目的

测评 KTGraph 在异步协作意义构建中进行知识传递的性能

##### 实验

被试随机分到 KTGraph 和 baseline，由工作人员预先生成初始的知识传输图，被试通过初始图获取知识并结合原始数据集继续自己的调查。

##### 测评指标

1. handoff score ：对初始图研究后了解到的正确知识得数目

2. debriefing score：被试完成调查后得到的正确假设和观点的数目

3. key documents score ：对包含正确证据文档的正确引用的数目

##### 实验结果

实验显示 KTGraph 的各个测评指标分数都比 baseline 更优秀，证明 KTGraph 在知识传递方面有更好的性能。

![1565764581176](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/8/14/4e4433c5264d851119e7536317ae492f36813a6a.png)

### 外部化的多样性和偏好

##### 目的

在调查的不同阶段去研究多样化的知识传输图和策略

##### 实验

将被试每三人一组进行异步协作，随机分配到 baseline 和 KTGraph 进行调查，调查结束后完成对界面组件可用性的调查问卷和一个针对调查过程的访谈

-   在对纽约市的出租车的场景分析中，节点表示了一个区域，而节点的信号则对应这个区域的出租车接客数量，网络中的边则是两个区域之间的乘客上下，边权重则是接送的乘客数量。
-   而在另一个场景分析中，作者将人转换成节点，节点信号则是一段时间内这个人的人际交往数量，也就是该节点的度数。

##### 实验结果

被试普遍认为 KTGraph 的时间轴对于知识传递更有效，调查的各个阶段形成的知识传输图多样化明显。

### 知识传递策略的分析

##### 目的

基于前两个实验的调查结果，对被试采取的策略与得分之间的影响情况进行分析。

##### 知识传递策略

1. Starting over：忽略已存在的图，根据初始线索构建自己的图，后续将自己的图与已存在的图做合并，关注点在自己的图
2. Random access：随机查看看起来有趣的元素，并尝试理解整个图。
3. Naive browsing：自然的顺序对图进行查看,之后综合并排序决定研究的方向。
4. Hubs and bridges：将复杂的模块连接形成更大的图
5. Tracing from the origin：需要找到之前调查的开始点并通过图结构对之前分析人员的调查过程进行研究

##### 实验结果

结合之前实验中被试采取的策略以及他们的得分情况进行分析。结果显示，tracing from the origin 策略较为优秀，而且 KTGraph 很好地支持了包括 tracing from the origin 在内的较为优秀的策略。

### 总结与未来工作

##### 总结

1. KTGraph 在 user study 中优秀的表现证明通过 KTGraph 可以很好的获取之前调查者的知识并利用它们更好的输出结果

2. 定义了在知识传递中使用的一些策略并验证了 KTGraph 可以很好的支持其中较为优秀的策略。
3. 局限：被试的数目限制了结论的有效性；被试间协作是按顺序进行的，无法并行工作，策略可能不全面

##### 未来工作

1. 扩展 KTGraph 的分析能力

2. 更多的用户研究去深入评价 KTGraph 在知识传递中的效果

3. 提升工具的可扩展性和工作空间管理
