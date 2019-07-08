---
title: "Authoring Narrative Visualizations with Ellipsis"
tags: ["论文评述", "学术会议", "报告"]
date: 2014-06-25
author: 侯雨濛
mathjax: true
---

论文：Authoring Narrative Visualizations with Ellipsis

作者：Arvind Satyanarayan,  Jeffrey Heer

发表会议：Euro VIS 2014

 

在现行的叙事性数据新闻的制作过程中，由于新闻从业人员往往具备较少的编程基础，而现有的可视化集成工具在storyline的组织和交互上又有所局限，因而新闻从业人员往往不能按照自己的新闻思维与设计思路去制作一个具有良好表达性的数据新闻成果。该篇文章的工作就是基于这一需求，建立了一个基于状态机的场景模型，形成一个结合了多种可视化组件、标注、时间线和交互等元素的原型工具——Ellipsis，来方便新闻从业人员自由地创造叙事性的数据新闻。

1. 模型结构

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/06/QQ%E6%88%AA%E5%9B%BE20140625151146.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/06/QQ截图20140625151146.png)

图1：Ellipsis建立的模型结构

 

[
](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/06/图片13.png)



2. 工作流程

Ellipsis制作基于storyline的叙事性数据新闻的工作流程如下：

首先，导入完整的静态可视化代码。

之后，通过基于GUI的鼠标操作，对可视化的呈现内容进行场景切分，做storyline的编排。

进而，对每一个场景进行编辑：添加图元、标注和交互的触发器。

然后，将不同场景按照线性时间编排或者非线性的方式组合起来，形成一个完整的叙事性的数据新闻。

最后，导出WEB端可以直接使用的代码，以方便用于进一步的发布。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/06/QQ%E6%88%AA%E5%9B%BE20140625150244.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/06/QQ截图20140625150244.png)

图2：用Ellipsis制作叙事性数据新闻的流程示意

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/06/QQ%E6%88%AA%E5%9B%BE20140625150359.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/06/QQ截图20140625150359.png)

图3：用Ellipsis制作叙事性数据新闻结果

3. 用户界面

Ellipsis为用户提供了基于拖拽的友好的操作界面，可以轻松实现标注、绑定、设置等操作，还为用户提供了场景管理和预览与输出的功能。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/06/%E5%9B%BE%E7%89%8713.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/06/图片13.png)

图1：Ellipsis用户界面

4. 用户研究

本文作者邀请参与者使用Ellipsis来完成简单的叙事性数据新闻的制作任务，参与者均在无需过多指导的情况下顺利完成任务。且评价该系统为“a promising collaborative design tool”（有潜力成为一个出色的集成的设计工具），“give reporters more of a sense of ownership over the ﬁnal visualization”（能够让记者们获得更多的对最终可视化作品的把握感和拥有感）。

此外，参与者们还提出了，关于Ellipsis还可以更多地去关注复杂的storyline设计，以及交互界面还可改进等意见。

综上，Ellipsis在叙事性的数据新闻制作上是一个成功的工具。它为数据新闻界的用户带来了在storyline编排、交互设计和叙事组织方面上的较大自由度，使得新闻从业人员能够对产出的数据新闻具有更多的自主性和创造性。