---
title: "Visual Progression Analysis of Event Sequence Data"
tags: ["论文评述", "报告"]
date: 2019-06-21
author: 孟林昊
mathjax: true
---

论文：Visual Progression Analysis of Event Sequence Data

作者：Shunan Guo, Zhuochen Jin, David Gotz, Fan Du, Hongyuan Zha, and Nan Cao

发表：IEEE VAST 2018

## 背景介绍

Event data是指带有离散的时间信息的事件数据，这些事件数据由特定属性聚集排列成事件序列（event sequence）。以一个人的学术生涯为例，单个实体（entity）的事件序列由本科毕业 -> 做研究 -> 发表论文 -> 博士毕业 -> 成为教授这一系列事件组成。

[![图片 1](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/06/%E5%9B%BE%E7%89%87-12.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/06/图片-12.png)

这些事件序列数据揭示了实体在不同阶段的演变过程，对事件序列数据的模式分析可以帮助发现不同人群疾病的发展过程，或是疾病的发展规律，对于不同人群使用不同的诊疗方案可能会有不同的结果，也需要进行比较。由于不同的individual sequence，其序列长度不同，发展速率不同，这就给使用基于时间或是顺序的大规模事件序列数据的总结摘要来进行模式分析带来了挑战。

本文将事件序列数据划分为不同阶段（stage），从而揭示不同群体的行为模式。

[![stage](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/06/stage.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/06/stage.png)

本文贡献在于以下三个方面。

1. 提出了一种针对事件序列数据的无监督阶段分析算法。其将事件序列数据进行对齐和划分。提取出不同持续时间的阶段来更好地反映发展模式。

2. 设计了对以上阶段分析算法结果的可视化系统ET2

3. 利用三种评估手段（case study, interview, performance evaluation）验证了系统的有效性。

## 系统流程

[![2](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/06/2.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/06/2.png)

本文提出的阶段分析算法有以下三个步骤组成。

[![process](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/06/process.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/06/process.png)

### 事件表征

使用了类似于word embedding的方法，将每个event sequence看成sentence,每个event看成word,利用skip-gram model进行训练来得到embedding结果。但不同于自然语言处理方法中训练样本通过滑动窗口生成，几个连续的单词形成上下文语境，对于事件序列，不光要考虑事件排列顺序，还要考虑事件发生的时间间隔。因此，对event embedding训练的损失函数中利用权重wij来调节周围事件出现在中心事件附近概率的权重，时间间隔越小，权重wij越大，损失函数表示如下：

[![loss](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/06/loss.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/06/loss.png)

### 事件对齐

使用了一种叫做动态时间规整(Dynamic Time Warping)的算法。它是一种衡量两个时间序列之间的相似度的方法，主要应用在语音识别领域来识别两段语音是否表示同一个单词。如图所示，上下两条实线代表两个时间序列，时间序列之间的虚线代表两个时间序列之间的相似的点。DTW使用所有这些相似点之间的距离的和，称之为归整路径距离(Warp Path Distance)，用来衡量两个时间序列之间的相似性。动态时间规整算法就是要找到这些对应的时间线上的点来最小化两个序列的相似性。

[![dtw](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/06/dtw.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/06/dtw.png)

事件序列对齐算法中，先利用最长事件序列初始化一个中间序列，再使用DTW算法找到要比较的事件序列和中间序列的对应关系，事件之间的距离用事件向量的欧式距离进行度量，每次迭代都会对中间序列的向量进行平均化更新，直到所有事件序列都和中间序列找到对应关系，对于一个序列中一个事件对应中间序列多个事件的情况，我们只选取和该事件最相似的中间序列事件。

[![align](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/06/align.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/06/align.png)

### 事件分割

成阶段使用了一种叫做Content Vector Segmentation(CVS)的方法，它是一种将文档划分成为一些连贯的段落的方法。将中间序列类比为文档，中间序列每个向量看成单词，我们认为相同阶段的事件有着相似的语义，分割算法的目标在于最大化每个segment的coherence(内部语义的相干性)。

[![coherence](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/06/coherence.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/06/coherence.png)

我们进一步利用中间序列的分割结果就可以得到每个序列的分段结果，并进一步将序列分段结果导入可视化模块进行可视分析。

## 界面概览

下图是整个用户界面概览。

[![interface](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/06/interface.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/06/interface.png)

 

Sequence view使用滚动列表的形式展示了每个individual sequence的分段结果；Cluster view将每个阶段的分段聚集成簇，并展示了不同阶段间簇的发展模式；Stage transition view将同一阶段的簇聚集在一起，展示了不同阶段的事件分布和演变模式。

## Case Study

本文的Case study共有两个，一个是使用公开的重症监护数据集MIMIC来分析临床进展，邀请来一位心脏病学家和他的一名博士进行分析；一个是利用包含39位大学教授23年间的学术生涯里程碑事件的数据集分析学术发展路径，邀请一名高年级博士利用系统进行分析。

[![case](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/06/case.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/06/case.png)

专家访谈总结了case中三位专家对ET2给出的反馈。包括一下三个方面：

1. 自动阶段分析：方便有效

2. 可视化设计：cluster view highly effective

3. 系统：简单易用，查询机制十分关键，建议应用到特定领域（特定疾病或是特定领域的学术路径）；视图太多，图太多字太少，event overview建议去掉

## 讨论

1. 过程分析算法适用于任何事件序列数据，算法本身和可视方法对序列长度、种类以及事件间隔都没有任何限制。

2. 阶段过程分析缺乏ground truth来度量算法准确性，本文通过用户反馈来验证，未来作者计划收集带有已知ground truth的基准数据集得到更为定量的准确率度量。