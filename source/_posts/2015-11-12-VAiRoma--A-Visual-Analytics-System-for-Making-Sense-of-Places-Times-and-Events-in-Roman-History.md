---
title: "VAiRoma- A Visual Analytics System for Making Sense of Places Times and Events in Roman History"
tags: ["论文评述"]
date: 2015-11-12
author: 胡万祺
mathjax: true
---

论文：VAiRoma- A Visual Analytics System for Making Sense of Places Times and Events in Roman History
作者：Isaac Cho, Wewnen Dou, Derek Xiaoyu Wang, Eric Sauda and William Ribarsky

发表会议：infovis 2015

本文提出了集文本分析和时空分析的可视分析系统 VAiRoma，帮助人们快速查找古罗马历史文献以学习和了解古罗马的历史。相关工作提到了 sensemaking, 主题趋势可视化、维基百科文本数据可视化、历史可视化等方面的工作。

本文使用的数据来源于维基百科的网页文本数据，提取包含 Roma、Roman、Rome 等与罗马相关的词语的页面，数据量有大约 189000 篇文章。之后，对数据进行预处理，包括提取主题、提取地点、坐标和时间。其中主题提取采用了另外一篇论文《I‐SI: Scalable Architecture for Analyzing Latent Topical‐Level Information From Social Media Data》中的方法，共提取了 40 个主题；地点抽取采用 Stanford NER 方法，并用 GeoNames API 进行精确定位，重名的地点收到纠正；时间抽取则是采用 Stanford NER 和正则表达式匹配的方式实现。最后将数据展现在可视化界面上，图 1 是系统流程图。

[![图片1](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/11/%E5%9B%BE%E7%89%8711.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/11/图片11.png)

图 1

系统界面如图 2 所示，主要分为三块，A 视图（时序视图）是话题在时序上的展示，B 视图（地图）是在地理空间上的展示，C 视图是本文设计的话题浏览视图。时序视图以堆叠图的形式展示了各个主题的热度趋势，支持用户缩放和选择一段时间区间；地图上展示了筛选出的文档中提到的地点，地图上 以热度图的形式提供了热点区域的概览，每个红点表示一个地点，用户可以通过点击源点来查看相关的维基文章；话题浏览视图则让用户将将近 19 万篇文章的探索任务聚焦到 40 个主题中。首先圆心显示了当前时间轴选择的时间区间，或选中主题的关键词。圆周上展示了主题间的层次关系。圆周外围线段连接圆表示了各个主题以及主题所占的权重，视图放大后会看到圆周围按顺时针顺序排列该主题的关键词。

[![图2](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/11/QQ%E6%88%AA%E5%9B%BE20151112125758.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/11/QQ截图20151112125758.png)

图 2

文章后面描述了两个 case study 和一个 user study 来验证系统的可用性和有效性。综上，本文提出的 VAiRoma 可视分析系统，帮助人们快速学习和了解古罗马的历史。
