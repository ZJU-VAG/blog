---
title: "Bridging From Goals to Tasks with Design Study Analysis Reports"
tags: ["论文评述", "报告"]
date: 2017-12-20
author: 梅鸿辉
mathjax: true
---

论文：Bridging From Goals to Tasks with Design Study Analysis Reports

作者：Heidi Lam, Melanie Tory and Tamara Munzner

发表：InfoVis 2017

本文作者之一Tamara之前已经发表过很多与可视化任务和可视化设计相关的分类文章，包括：

- 可视化任务的多层分类

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/12/%E5%9B%BE%E7%89%871.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/12/图片1.png)

- 可视设计和验证的嵌套模型
  [![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/12/%E5%9B%BE%E7%89%872.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/12/图片2.png)

这些文章能为可视化系统的设计提供指引。但本文作者对现有的任务分类仍不满意，主要原因在于现有的分类不能很好的指出高层分析目标和低层分析任务间的关系。

举例来说，分析员发现航班交易失败记录猛增，他希望了解为什么会发生这样的情况。于是尝试检查失败记录的属性(时间、航空公司等)分布，并发现某个航空公司可能是罪魁祸首。
这个例子中高层分析目标可能是“寻找错误原因（Identify Main Cause）”，而对应的低层分析目标则是“查找某个属性的outlier（Discover Outliers）”。

而分析员是通过自身的经验和尝试完成了这样的一个转换，如果能有一个分类直接将其对应起来，则可以大幅减少所需时间，提高分析效率。

为了完成这个分类，作者选取了Vis2009-2015共287篇论文并进行筛选。筛选标准包括

1. 解决现实世界问题
2. 使用真实数据
3. 设计或评估时涉及至少一个目标用户
4. 包含实际分析报告

最后，从筛选出的20篇文章提取出其中的分析报告加以分析。原始的分析资料可以在http://tinyurl.com/gt27fau找到。

从中，作者总结出9种分析目标，和其对应的输入输出需求：
[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/12/%E5%9B%BE%E7%89%873.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/12/图片3.png)
其中，I=input，O=Output，Obs=Observation, Pop=Population, Pop Defn=Population Definition/Pop Contrasts。

- observation：数据中的发现（outliers, trends, …)
- record：分析的最小单元
- population：一系列record
- population definition：描述population的一系列属性和数值
- hypothesis：基于分析者信念和有限线索的猜想

这些分类可以又如下的使用方式：

- 与现有分类对照学习
- 用于学习采访脚本
- 用于学习分析记录
- 用于可视设计