---
title: "Dendrogramix: a Hybrid Tree-Matrix Visualization Technique to Support Interactive Exploration of Dendrograms"
tags: ["论文评述", "报告"]
date: 2015-05-04
author: 吴斐然
mathjax: true
---

**Dendrogramix: a Hybrid Tree-Matrix Visualization Technique to Support Interactive Exploration of Dendrograms**

Renaud Blanch, Rémy Dautriche, Gilles Bisson
PacificVis 2015

层次聚类是一种常用的算法，其将原始数据组织成树状结构，以刻画数据点之间的相似程度。经典的层次聚类可视化方式为系统树图（Dendrogram），本文则介绍了一种新的层次聚类树的可视化方法 Dendrogramix，其混合了树和矩阵可视化方法，在聚类层次上叠加了个体关系的表达，丰富了表达的内容。

Dendrogramix 的形成过程非常简单直观。如图一所示，将一个简单的包含有 5 个二维点的数据集（图一（a））层次聚类，其结果的系统树图如图一（b）所示。而 Dendrogramix 首先用矩阵编码了这五个点之间两两相似性（图二（a）），运用自动优化方法重排序按相似度显现出对角线上的聚类性质（图二（b）），将这些聚类加以编码（图二（c）），最后对折以节省显示空间（图二（d））。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/tu1.jpg)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/tu1.jpg)

图一 原始数据点和对其进行层次聚类以后的结果

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/tu2.jpg)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/tu2.jpg)

图二 Dendrogramix 的形成过程

Dendrogramix 的主要交互分为浏览、对象比较、聚类聚合、树重排序、聚类二元操作几项。首先就**浏览**来说，Dendrogramix 支持数据对象以及层次的选择，这和传统的系统树图并无二致，图三（a）显示了当用户选择一个对象之后的高亮情况，标签上方的方块编码了选择到的对象和其他对象之间的相似度。**对象比较**着重于选择到两个数据对象并且高亮，从而能够观察到这两个对象之间的相似度（图三（b））。对于**聚类聚合**来说，Dendrogramix 支持对于层次聚类中某一个树进行收缩聚合操作，类似系统树图的子节点收缩伸展操作，用户还可以在聚合起来的聚类上做标注加标签。**树的重排序**支持用户在不破坏数据相似度关系的情况下将某一个节点或者某一部分节点拖动到需要的位置。需要注意的是，重排序本质上是对层次聚类二叉树各个节点的左右两个字节点位置进行交换，所以对一个节点进行拖动操作会对整个结构产生影响。**聚类二元操作**是一种建立在一连串树的重排序之上的操作，其可以将两个聚类相交的部分按用户要求挪动到相应的位置。如图四所示，用户观察到图四（b）红色聚类和绿色聚类相交部分体现出这两个聚类的相似度较大，但是采用自动的排序优化算法并没有把这两个聚类排到邻近的位置，于是用户可以采用如图四（c）的拖动操作，最终将其拖到图四（d）的位置，从而实现对自动重排序结果再优化的效果。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/tu3.jpg)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/tu3.jpg)

图三 选中单个对象和多个对象之后的界面显示

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/tu4.jpg)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/tu4.jpg)

图四 聚类二元操作的各个步骤，用户目的为将（b）中的划选部分拖动到（d）中的位置，从而引发一系列聚类重排序的操作。

文章的最后作者精心设计了一个 case 来论文该方法的可靠性。总而言之，这是一篇论述可视化方法的偏 infovis 风格的论文，方法上的确比较简洁易懂，而且和传统的层次聚类可视化方法比较来说，增加了新的信息并有机整合进了可视化的编码之中，一方面继承了以前方法的特性，又让用户容易上手，确实是一种比较有意义的改进。但是个人感觉本文的工作并没有做完，目前的文章容量和编排放到 VIS 这样的会议可能就不太够了。此外该工作的改进潜力不小，作者在未来工作中也介绍了一些改进点，比如帮助比较不同的层次聚类方法等等，个人认为这个方向可能和 bi-cluster 这种多域的 matrix 可视化可以结合，此外在方法对大规模数据的适应方面也有一些改进空间。
