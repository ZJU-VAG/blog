---
title: "#FluxFLow: Visual Analysis of Anomalous Information Spreading on Social Media"
tags: ["论文评述", "报告"]
date: 2015-05-14
author: admin
mathjax: true
---

FluxFLow: Visual Analysis of Anomalous Information Spreading on Social Media

Jian Zhao,NanCao,ZhenWen,YaleSong,Yu-RuLin,andChristopherCollins

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/%E5%9B%BE%E7%89%871.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/图片1.png)

FluxFlow 是一款可视分析系统，用于可视化和分析社交媒体中的异常信息扩散。本文的数据来源于分析对象是 Twitter 的跟贴信息。

对社交媒体的研究有两个主要问题，“哪些消息流值得观察？”和“被选出的消息有何不同？”。针对这两个问题，本文分别设计了基于 OCCRF（One-Class Conditional Random Fields Model，单类条件随机场）的数据挖掘算法和用于查看数据挖掘结果和其内在隐含信息的可视化设计。系统基本构架如图

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/%E5%9B%BE%E7%89%872.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/图片2.png)

OCCRF 的特点是有着时序依赖、单类以及无需标注好的训练集，其结果是一个作为异常度度量的“异常分数”。本文主要用了以下几类特征作为 OCCRF：

C1 用户简要特征，C2 用户网络特征，C3 时序特征，C4 内容特征

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/%E5%9B%BE%E7%89%877.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/图片7.png)

可视设计方面，用一个圆形的设计表达一个跟帖（及其后的所有回复），圆的半径是跟帖内回复的用户数，内圆颜色编码了情绪指标（从上面 C4 类的两个特征中提取），外圆颜色编码了“异常分数”，颜色越偏向紫色则越异常。还用扇形的开始和结束位置编码了跟帖的时间跨度。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/%E5%9B%BE%E7%89%873.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/图片3.png)

这个圆形设计被用在了很多地方，如可视化的主要视图

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/%E5%9B%BE%E7%89%874.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/图片4.png)

MDS 投影和层次聚类视图

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/%E5%9B%BE%E7%89%875.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/图片5.png)

图中除了上述圆形视图外，还有一些简化了的小圆，即没有被选中的数据，其编码是通过颜色表达一些（上面特征表中的）用户信息。

除此之外还能表达一些关系信息，如同一个人的多次回复，好友关系（下图）等

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/%E5%9B%BE%E7%89%876.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/图片6.png)

除此之外，还有一些详细视图如 OCCRF 中隐含变量的时序分布（下图 d）、MDS 分布（下图 e）、具体回复内容（下图 f）等。

本文还用多个案例介绍了系统的使用方法、OCCRF 内在隐含变量与结果的关系等。
