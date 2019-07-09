---
title: 是什么特质让Hamlet如此Hamlet？
tags: ["论文评述"]
date: 2013-10-16
author: 马晓红
mathjax: true
---

论文：Explainers: Expert Explorations With Crafted Projections

作者：Michael Gleicher

会议：IEEE VAST 2013 Honorable Mention

本文介绍了方便用户添加标注，并且可以解释的投影函数的构造方法。

这是本文方法对不同城市的各种指标构造的线性一位投影结果的可视化。

[![1](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2013/10/1.jpg)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2013/10/1.jpg)

140 个城市从左到右，从上到下依次排布，代表其投影的序列。紫色代表用户标记的美国城市，绿色代表其他城市。作者仅仅用了三个城市指标：Healthcare indicators，sports event 以及 public healthcare。每个维度在线性投影的函数中的权重也为-1，0 或 1。这样的投影函数满足多个优良的属性：

- 准确性：分类结果要准确
- 简单性：分类结果要容易解释
- 多样性：提供多种分类函数供选择
- 统计属性：代表性等等其他属性

本文方法用莎士比亚戏剧的案例案例：

下图展示了作者对莎士比亚戏剧的分类：

[![2](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2013/10/21.jpg)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2013/10/21.jpg)

每行代表一部作品，每行的五格代表一部戏的五幕场景。

绿色代表风格很接近 Hamlet，紫色代表风格与 Hamlet 不同。前三个是本文方法的分类效果，都是用了三个特征做分类；后两个是普通 SVM 的效果。

可以看到作者的分类效果并不理想连 Hamlet 本身（12 行）的五幕都没被分为一类。而最好的第五个 SVM 使用了 26 个维度才将勉强将 Hamlet 分类出来。

于是作者的结论是：Hamlet 没有显著特征！

乍看似乎很可笑，代表了莎士比亚戏剧创作的最高成就怎么可能没有独特之处呢。

再看看文学评论家的说法，就发现 Hamlet 是一部充满矛盾，不连续以及不确定性的作品。我们可能很难用简单的维度来描述其特征。Hamlet 的其魅力所在就在于此。
