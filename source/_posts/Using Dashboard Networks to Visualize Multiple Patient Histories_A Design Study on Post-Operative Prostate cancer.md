---
title: "Using Dashboard Networks to Visualize Multiple Patient Histories: A Design Study on Post-Operative Prostate cancer"
tags: ["论文评述", "报告"]
date: 2019-06-13
author: 王杰
mathjax: true
---

论文：Using Dashboard Networks to Visualize Multiple Patient Histories: A Design Study on Post-Operative Prostate cance

作者：Jurgen Bernard, David Sessler, Jorn Kohlhammer

发表：IEEE TVCG 2018

简介：这篇paper是一篇关于医疗健康的可视化设计研究。作者以术后前列腺癌的病史为例，使用仪表盘网络来进行可视化设计研究。

[![图片12](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/%E5%9B%BE%E7%89%87124.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/图片124.png)

## 相关工作

将电子病史进行可视化有助于医疗研究、临床治疗、专家病患间的沟通。然而病史中蕴含大量病人的信息特征，需要对比展示，难以有效的表达，是一项具有挑战性的任务。

现有工作中，最早开展的是直接对单个病人的各种信息进行展示（Visualization of Single Patient Histories ）。

比如2004年的这篇paper，使用交通信号灯的视觉编码表达病情（红色表示病情严重，黄色是警告期，绿色表示康复）。主要视图是沿病史的时间展示各种属性，其他视图用作医疗辅助。作者本人之前也做过类似的研究。不过这种方式1次也只能展示1个病人的情况，实际上没法展示、探索大量病例。

[![图片2](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/%E5%9B%BE%E7%89%8723.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/图片23.png)

*图1，Connecting time-oriented data and information to a coherent interactive visualization,2004.*

为了能够同时展示多个病例的某些特征，需要将病例中的一些特征抽象为特定的视觉符号，通过统计进行展示（Visualization of Event Sequences of Patients）。

比如2015的CoCo系统，在这张视图中，其三角形代表病例中的一个事件：病人每天睡在什么床上，右侧统计了对应事件组合的死亡率。但是，这种方式一次也只能展示一种或几种用于比较的特征，而且会损失每个病例一些独有的特殊信息。

[![图片3](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/%E5%9B%BE%E7%89%8733.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/图片33.png)

*图2，Cohort Comparison of Event Sequences with Balanced Integration of Visual Analytics and Statistics,2015.*

总结的说，现有病史可视化的相关工作有两种，分别能表达：**multiple attributes for few patient histories**；**few attributes for many patient histories**，

挑战是 **multiple attributes for many patient histories**， 而且这些属性有多种数据类型（numerical, ordinal, categorical, and binary），使用平行坐标、散点图矩阵等常规方法并不适合。

于是作者转而去参考glyph设计思想在相关领域的运用，采用glyph design来可视化多变量属性集合（Visualization of Multivariate Attribute Sets）。这篇2012年的paper采用glyph来表现生物实验的工作流，可以在一张视图上同时显示大量信息。

[![图片4](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/%E5%9B%BE%E7%89%8742.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/图片42.png)

*图3，Taxonomy-based glyph design—with a case study on visualizing workflows of biological experiments,2012.*

## 本文方法

首先，作者与4名医学专家确定了15个描述前列腺癌手术的主要属性，根据属性的不同类别赋予不同的视觉编码。

[![图片6](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/%E5%9B%BE%E7%89%8762.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/图片62.png)

*图4，前列腺癌手术的15个主要属性*

数据集包含欧洲2000余份前列腺癌手术的病史，处理病史分为分段和聚合两个步骤：

**分段segmentation：**把复杂的时态数据划分为有意义的小段落，使用事件的发生顺序取代事件发生的实际时间 。有两种分段的标准： 1. 某些指标发生显著变化（新的治疗手段/结果） 2. 到达给定的分段最大长度（本文为6个月）。为2000余份病史创造了10485个分段， 平均每个病例有3~7个分段。

举例如下：一个病人在经历前列腺癌手术后，前4个月的癌症情况为良好，而5-10月复发了，则为其分段。段落是之后可视化、统计所用的最小单位。

[![图片7](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/%E5%9B%BE%E7%89%8773.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/图片73.png)

**聚合aggregation：**把分段组合以展示在dashboard中。有两种聚合的方法： 1. 把10485个分段聚合在一起，提供所有患者的overview 2. 根据某种属性进行分组统计，纵向比较（longitudinal changes）。

举例（1）如下：这是10485个分段的overview，作者称之为static dashboard 静态仪表盘。不同类型变量使用了不同图表和合适的视觉编码。在总览中，可以看到，pt2c,pt3a,pt3b最为常见；格里森中3+4,4+3最为常见；大约3/4的患者一次手术后仍有复发现象；所有患者都做了手术，最主要的还是放射治疗。

[![图片8](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/%E5%9B%BE%E7%89%8784.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/图片84.png)

*图5，case 1，静态仪表盘*

举例（2）如下：刚才介绍了第一种使用场景，这种全体的概览明显地没有利用到各个分段的特征信息；接下来是第二种使用场景。

首先选择了只含有pt4状态的患者，然后依照治疗手段的不同组合，从左向右排布。从这种纵向比较中，可以观察发现PSA值逐渐提高，患者的治疗结果也逐渐恶化。比如接受放射治疗的患者，11个案例全部都为复发。比如左边的只有op，到了最右边用上最终手段cht，病人的死亡率仍然很高，其癌症非常严重。

作者称之为仪表盘网络，实际上就是按照某一属性的组合排列，纵向排布用作比较。

[![图片9](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/%E5%9B%BE%E7%89%8793.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/图片93.png)

*图6，case 2，仪表盘网络*

举例（3）如下：第三种使用场景，在dashboard network的基础上，再比较某一属性的区别。只出现pt2c情况的患者，相比pt4的患者，最显著的是没有出现化疗的仪表盘；每个阶段对比下，其PSA值比较低；其治疗结果也更好，只有少量的meta、dod；N1值接近0，N0占据了主导地位。

总结的来说，医疗专家能从中总结规律，患者也能轻松的找到自己所在阶段的整体情况，便于治疗沟通。

[![图片10](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/%E5%9B%BE%E7%89%87104.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/图片104.png)

*图7，case 3，仪表盘网络之间的比较*

## 用户评估

本文的可视化面向三类用户：医疗专家，可视化专家，非专家（公众–患者）。

- 实验参与的者情况：14名参与者（2女12男）；参与者至少拥有硕士学位，5名拥有博士学位；包含5名可视化专家，4名前列腺癌症临床医生，5名非专家。

- 实验流程：介绍前列腺癌和属性编码（10分钟）；熟悉本文的可视设计（10分钟）；执行评估患者情况的任务（20分钟）。

- 实验结果：统计每个参与者对数据属性作出观察的数量；所有参与者都能作出有效的观察；医疗专家能够做出更多的观察，并保持一致性。

[![图片11](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/%E5%9B%BE%E7%89%87115.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/图片115.png)

*图8，对于每个属性作出观察的数量统计*

## 总结

本文的思路和方法很简单，针对医疗数据做了一个可视化设计，能够一次性呈现多种属性，使得用户能够快速作出观察。

- 优点：不同领域的参与者都能理解可视设计，作出大量观察；参与者能够同时分析大量属性，并直观地指出患者队列之间的差异。

- 局限性：在现实环境中，患者熟悉可视设计仍需要时间成本；存在不同治疗顺序的患者被统计到一起（OP-RTX-HT对比OP-HT-RTX），丢失了这部分信息；可扩展性较差，dashboard的复杂性增加时可能会破坏现有可视化设计的协调性。

- 未来工作：研究处理丢失、噪音数据的能力；研究可扩展性；研究应用到其他领域的可行性。