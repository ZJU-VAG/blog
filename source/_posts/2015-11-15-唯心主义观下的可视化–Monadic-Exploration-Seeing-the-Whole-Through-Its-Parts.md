---
title: "唯心主义观下的可视化–Monadic Exploration: Seeing the Whole Through Its Parts"
tags: ["论文评述"]
date: 2015-11-15
author: 汪飞
mathjax: true
---

人类置身于大量数据之中，这些数据包括社交数据中的照片集、每年读过的图书、写过的博客或微博等。对于这些数据，人们不仅希望能看到自己感兴趣数据的详细内容，而且还希望能了解这部分数据所在数据集合的上下文结构。比如说，在看某人的个人信息的同时，还想知道这个人都有哪些朋友，这样可以更全面地了解这个人的情况。从在线社区当中调查发现，从用户已知的知识出发探索数据其实比我们熟知的原则—overview first–更有效。面对大尺度的数据，绘制数据的整体视图往往非常困难，另外，用户也不需要了解全局数据。
受社会学家 Bruno Latour 的启发，论文从可视化的角度重新解释 monad 概念。论文提出了一种在复杂关系数据中探索数据的新思想和可视化方法。在此基础上，论文设计了一种探索关系数据空间的交互工具，此工具不仅包含个体视图而且包含总体结构视图。

## Monad 概念和原则

Monad 是从事物自身出发，描绘其看到的世界。这看起来有些抽象，其实 Monad 类似于通常所说的唯心主义。任何一组视图，都包含一个对象以及这个对象所能看到的周围其他对象。
On Having, Not Being
元素和它们之间的关系是构成世界的基本元素。元素之间的关系定义为属性。关联的元素之间符合牛顿第三定律：作用力和反作用力，即两者之间的关系是相辅相成的。另外，实体具有一些属性，实体和属性之间的关系为 having 关系而不是 being 关系。Having 关系意味着元素之间的关系可以相互切换。
Difference
有时候两个 monad 视图中存在部分元素相同。如何才能区分两个 monad 呢？monad 中关联元素的变化确定了两个 monad 的不同。另外，差异化是理解单子世界的基本条件，是单子唯一性的基本保证。
Movement
运动主要用于展示重叠的单子视图的变化，在可视化中用动画为信息探索提供帮助。

## 可视化设计

在论文的实验网站中有三个界面，分别展示文章视图、monad 视图和网络视图。从文章视图和网络视图的比较来看，前者更关注细节，而后者则关注整体结构。Monad 视图则综合了两者的长处，避免其不足，以单个实体为中心，将关联的实体径向布局在周围。点击中心实体可以看到细节内容，同时也能看到实体的上下文环境。

[![monad-1](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/11/monad-1.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/11/monad-1.png)
Monadic 视图以径向布局，中心是关注的实体，周围的元素依照集合排序和相关性排列，离中心越远则相关性越低。当中心点发生变化时，周围的其他元素也随之变化。除此之外，monadic 视图还支持搜索和关键字导航。

[![monad-2](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/11/monad-2.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/11/monad-2.png)

## 用户调查分析

作者将 monadic 视图应用到“Beautiful Trouble”这本书上，通过该视图展示书中的引用关系。视图发布到网站上，包含三个界面：文本视图、monadic 视图、网络视图。从读者和编辑反馈的情况来看，大多数人都认为 monadic 是非常好的设计，界面简洁而且理解书中的内容非常快。而网络视图看起来比较糟糕，交叉的线条容易产生混乱。

[![monad-3](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/11/monad-3.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/11/monad-3.png)
