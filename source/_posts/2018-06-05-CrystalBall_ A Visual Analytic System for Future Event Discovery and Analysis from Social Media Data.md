---
title: " CrystalBall: A Visual Analytic System for Future Event Discovery and Analysis from Social Media Data"
tags: ["论文评述", "报告"]
date: 2018-06-05
author: 胡元哲
mail: cadhyz@zju.edu.cn
mathjax: true
---

论文：CrystalBall: A Visual Analytic System for Future Event Discovery and Analysis from Social Media Data

作者：Yunhai Wang, Xiaowei Chu, Chen Bao, Lifeng Zhu, Oliver Deussen, Baoquan Chen and Michael Sedlmair

发表: IEEE infoVis 2017

# 1. 介绍

现有大多系统从社交媒体分析过去和正在发生的事件，很少关注一些即将发生的事情；现有预测未来事件的系统都指向了专一的事件类型，比如疾病，死亡，骚乱的预测 。今天的论文**使用 tweet 数据来探测未来事件**的可视化系统。

本系统的主要需求可以概括为下面三点：

1. 群众想知道本市最近的音乐会，体育比赛。
2. 零售商想知道人们未来一段时间的购买需求。
3. 政府想知道潜在的大型集体活动，游行。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/06/Screen-Shot-2018-05-16-at-11.12.51-AM.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/06/Screen-Shot-2018-05-16-at-11.12.51-AM.png)

CrystalBall 系统分析 tweet 数据，预测未来几周可能发生事件。CrystalBall 集成了多个组件，Twitter Streaming API ，未来事件提取，事件标识和排名以及交互式可视化界面。所有的数据收集和分析都是在线进行的。每天刷新以显示未来几天或几周内可能发生的事件。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/06/Screen-Shot-2018-05-16-at-11.13.00-AM.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/06/Screen-Shot-2018-05-16-at-11.13.00-AM.png)

我们可以把本文的贡献概括为以下三条：

1. 基于一种新的未来事件定义，提出了一种通用的方法来根据流式 Twitter 消息发现未来事件的系统 。
2. 设计多个度量标准，对已识别的未来事件进行特征化和排名 。
3. 一个新的交互视觉界面，将交互界面与计算方法和指标紧密结合，以支持未来事件的探索和感知 。

# 2. 处理与提取未来事件数据

作者看来，未来事件的定义是与**将来的位置和时间**相关联的事件。**位置和时间**是定义未来事件的主要属性。

首先从所有推文中筛选出日期迟于现在或者有明显将来时态的未来事件。

对于这些筛选出的推文，我们使用 7 种指标进行衡量

**NPMI**：位置和时间之间的相关性，相比 PMI，将其正则化到 1 和-1 之间。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/06/Screen-Shot-2018-05-17-at-8.58.53-AM.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/06/Screen-Shot-2018-05-17-at-8.58.53-AM.png)

**链接比例**：包含链接的推文与所有未来推文的比例

**主题标签比例**：包含标签的推文与所有未来推文的比例

**用户可信**度：论文选择一个简单的度量，即 Twitter 追随者朋友（TFF）比率来表示用户的可信度。TFF 是追随者与朋友的比率。1.0 到 2.0 之间的比率表示用户具有平衡的跟随/跟随者关系

**用户多样性**：如果关于一个潜在的未来事件的所有推文都来自一个账户，那么这些推文很可能来自被编程为定期发送某些推文的机器人。

**中心性**：推特间通过转发，@连接，高度连接的推特网络将具有接近 1 的程度中心性，而分散的推特网络产生接近于 0 的中心性。

**推特相似性**：但是并不是所有推文都有@和转发相关联。该指标计算了每篇推文的相似性

现在已经提出了未来事件的 7 个指标。下一步是结合这些措施来评估已确定的未来事件的质量。论文希望对事件进行排名，以便 CrystalBall 首先直观地表示高质量的事件。

**RankSVM 进行排序**。为了训练 RankSVM，论文开发了一个标签数据集，其中包含三天内提取的未来事件（约 1000 个事件）。作者将事件分为了 5 个类别。标注决定表明更加重视地缘政治和基层性质的事件。使用标记的数据集来训练 RankSVM，训练出一个可应用于无标签事件排序的模型。

# 3. 可视化界面

## 按时间轴检索

我们从整个时间轴进行查看。下图每行是一个日期，表示当天所可能发生的事件，实线连接的是有相同的地点的事件。虚线连接的是具有同样的关键词的事件。每个事件都有自己的颜色，颜色代表整个事件的感情属性，而颜色的深浅表达了置信度。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/06/Screen-Shot-2018-05-17-at-11.51.21-PM.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/06/Screen-Shot-2018-05-17-at-11.51.21-PM.png)

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/06/Screen-Shot-2018-05-18-at-4.30.20-PM.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/06/Screen-Shot-2018-05-18-at-4.30.20-PM.png)

除此之外我们可以点击某个日期，进入当日的事件界面，如下图所示：

1. A 图，花瓣的红色占比代表了未来事件 7 个指标的大小，中间的数字是该日共有几个未来事件。
2. B 图中，1 表是每个时刻的事件数，2 表是近 30 天内将会发生的相似事件数，3 表是按照感情属性分类的结果。
3. C 图中，未来事件中的关键词，D 按钮可以用来收藏

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/06/Screen-Shot-2018-05-18-at-4.47.53-PM.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/06/Screen-Shot-2018-05-18-at-4.47.53-PM.png)

## 按地点检索

A 图中可以放缩不同尺寸的地点，中间的数字表示的是事件数，不同深浅表达了在不同时间点内的事件。

B 图中当我们点击华盛顿城市，会跳出关系该城市的事件映像。

除此之外还有词云界面，关系网界面，这里不再赘述，有兴趣的读者可以自行去论文查看

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/06/Screen-Shot-2018-05-18-at-5.59.02-PM.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/06/Screen-Shot-2018-05-18-at-5.59.02-PM.png)

# 4. 样例验证

论文中举出 4 个例子，这里只介绍其中一个。下面介绍了一件北卡罗来纳州夏洛特市 2016 年 9 月抗议活动有关的一周活动。图 8 中连接的实线代表了三个有同样的地点的事物，分析这个时间线，可以发现这个时间线中有很多关于抗议的关键词。关注 9.24 一天，可以发现很多人的情绪都转变为恐慌，愤怒。与此同时从关系网也可以发现，大家的视线都转向了一篇关于抗议的推文。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/06/Screen-Shot-2018-05-18-at-7.44.08-PM.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/06/Screen-Shot-2018-05-18-at-7.44.08-PM.png)

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/06/Screen-Shot-2018-05-18-at-7.44.04-PM.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/06/Screen-Shot-2018-05-18-at-7.44.04-PM.png)

# 5. 缺陷与未来工作

-   论文使用 时间-地点 组合进行编码，比较局限。
-   存在识别未来事件错误，关于过去事件的新闻头条的推文可能会被错误地视为未来事件，而且很多转发是在很多天之后才收到转发。
-   时间位置的提取算法还是不准确
-   未来会尝试处理多个数据源的流量(fb, ins, wiki, google)
-   未来会考虑更换更好的 nlp 算法
