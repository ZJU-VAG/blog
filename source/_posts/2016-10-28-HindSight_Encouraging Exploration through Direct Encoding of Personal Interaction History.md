---
title: "HindSight: Encouraging Exploration through Direct Encoding of Personal Interaction History"
tags: ["论文评述", "报告"]
date: 2016-10-28
author: 劳天溢
mathjax: true
---

论文: HindSight: Encouraging Exploration through Direct Encoding of Personal Interaction History

作者: Mi Feng, Cheng Deng, Evan M. Peck, Lane Harrison

发表期刊: TVCG 2016



## 1. 背景

人的记忆力是有限的，并且会随着时间衰减。在数据探索过程中，人们需要花费精力记住自己的探索记录。因此，一项可以支持记录交互历史的可视化技术在数据探索研究领域将会有很大影响。

## 2. 简介

HindSight是指描述直接在原有可视化系统上展现交互历史的设计原则的涵盖性术语。文章提出了一个假想：在探索性分析中，直接编码的个人历史可以对用户行为产生积极的影响。为了验证这个假想，他们进行了实验：把HindSight用于3个已有的可视化系统中，来检验HindSight原则的价值。

HindSight原则的核心想法是（在数据编码的基础上）将用户的 **交互** 也编码到可视化设计中。

## 3. 实验过程

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/10/%E5%9B%BE%E7%89%8721.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/10/图片21.png)

实验使用了3个交互性的可视化系统（MetaFilter，255Charts，Storytelling），分别设置了实验组和对照组。实验参与者为AMT（“机械的土耳其人”网站）的雇员。



[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/10/%E5%9B%BE%E7%89%8711.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/10/图片11.png)

他们的测试过程分为3个阶段

Training：给参与者一个指导页面，描述了他们的任务和系统中的交互

Exploration：参与者和可视化系统交互，不限时长

Insight：可视化系统被隐藏，参与者被要求描述3-5个他们的发现，也可以在Comments里面写下他们的自由的见解

### 3.1 评估

对于实验结果，他们评估2个方面的因素：探索行为，以及交互之后产生的见解。

他们的测量指标有2种：

定量：

Visited：有多少个图用户直接交互过

Revisited ：有多少个图是用户重复查看过的

Exploration time：用户和图表交互花费的时间

定性：

Mentions：在发表见解阶段中一个图表被提及的次数

### 3.2 先导试验

他们在MetaFilter系统中做了先导实验，并且根据先导试验中的效应量和统计分析得出每个实验需要的人数规模。具体参与每个实验的人数如下：

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/10/%E5%9B%BE%E7%89%8731.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/10/图片31.png)

**用到的统计学方法：**

为了排除显著性检验(注①)的局限性，他们用到了统计学里的方法：置信区间（用bootstrap method计算），效应量（Cohen’s d）(注②)。

## 4. 实验结果

### 4.1 MetaFilter系统：

“The Rise and Decline of Ask MetaFilter”：描述了一个社区网络博客中主题种类的发布趋势。一共20个area-chart。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/10/%E5%9B%BE%E7%89%8722.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/10/图片22.png)[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/10/%E5%9B%BE%E7%89%8732.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/10/图片32.png)

HindSight设计：

- 交互历史用透明度的微小改变来编码。

- 如果一个图表被访问了0.5s以上，那么它会增加一些透明度，使它在视觉上明显一些。

统计结果：

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/10/1.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/10/1.png)

左侧用颜色映射了实验的统计数据：两个缩略图分别表示了对照组和实验组的访问频率：橙色（实验组），紫色（对照组）。较大的图表示了对照组和实验组的访问频率的差值：对照组只关注上面、左边，实验组关注的范围更广并且访问频率明显增多。

右侧直接列出了统计数值：在 Visited数据中，实验组 M = 9.4 95% CI [7.5, 11.3]，对照组 M = 5.4 [4.4; 6.5]，效应量 d = 0.75。说明在实验组中，用户的访问次数显著地增加；在Exploration Time数据中，实验组 M = 43.4 seconds [32.6, 65.6] 对照组 M = 36.1 [25.7, 51.6]，效应量 d = 0.15，在实验组中，用户停留的时间和对照组相比，增加得不是很显著。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/10/31.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/10/31.png)

在产生的见解方面：在实验组里更多地引用了底部区域，对照组里则引用的位置比较均匀。

### 4.2 255 CHARTS：

“How the Recession Shaped the Economy, in 255 Charts”：每一条线代表了一个行业在2004-2014年的增长或者下降。相比MetaFilter系统，数据更大，更复杂。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/10/%E5%9B%BE%E7%89%8741.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/10/图片41.png)   [![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/10/%E5%9B%BE%E7%89%876.jpg)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/10/图片6.jpg)

HindSight设计：如果一个图表被访问了0.5s以上，那么它会增加一些透明度，并且变宽一些。
统计结果：

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/10/2.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/10/2.png)

访问次数、重复访问次数、探索时间都显著增加，用户访问区域更偏重于中间部分。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/10/4.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/10/4.png)

产生的见解方面：见解引用的趋势和行为模式十分类似，实验组更多引用中间的部分。

### 4.3 StoryTelling:
“CO2 Pollution Explorer”：可以选择国家、年份查看CO2排放情况

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/10/%E5%9B%BE%E7%89%8771.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/10/图片71.png)  [![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/10/%E5%9B%BE%E7%89%8781.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/10/图片81.png)



HindSight设计：如果国家被访问了0.5s以上，那么它会增加一些透明度；如果年份被访问了0.5s以上，那么它会从灰色变成红色
统计结果：

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/10/5.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/10/5.png)

发现实验组和对照组的访问次数和时间差不多。不过他们发现，对照组和实验组访问的年份和国家非常相似。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/10/6.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/10/6.png)

产生的见解方面：发现没有显著的pattern，但是他们采用了Boy et al. 的评估方法，发现HindSight还是有一些improvement。

## 5. 结论

1. 大体上，HindSight设计可以鼓励人们去发现更多数据，并且在交互之后产生更多见解

2. 影响力取决于所用的系统种类：简单系统中，直观效果更大，在这类简单系统中，数据量越大，影响越明显

3. 具有较低的技术壁垒

4. 和间接历史记录编码不同，直接编码不需要用户在不同空间区块间来回处理，来获取历史信息和数据的联系

5. 正在开发类似系统的机构可以考虑用HindSight这个设计原则来帮助用户更快地感知数据

### 缺点：

1. HindSight太概念化，没有具体的标准化的操作方法，3个实验中使用的HindSight方法也比较随意，没有系统性

2. 不同系统的效果不一样

3. 参与调研的用户行为不一定具有代表性

4. 初次使用的交互行为和正常使用的交互行为也不同

### 优点：

实验比较完备，用数据说话，可以借鉴到UserStudy中。
注①：显著性检验：事先对总体做出一个假设，然后利用样本信息来判断这个假设（原假设）是否合理
注②：效应量（实用价值）是衡量效果的指标，不受样本容量的影响。一种计算方法是：均值的差 / 合并标准差