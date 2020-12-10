---
title: "HOLA: Human-like Orthogonal Network Layout"
tags: ["论文评述"]
date: 2015-12-07
author: 张天野
mail: zhangtianye1026@zju.edu.cn
mathjax: true
---

论文：HOLA: Human-like Orthogonal Network Layout

作者：Steve Kieffer, Tim Dwyer, Kim Marriott, and Michael Wybrow

发表会议：TVCG 2015

这篇文章设计了一种计算正交网络布局的自动化算法。重点在于，使用这种算法得到的布局能与用户手工绘制得到的结果在结构、布局上保持相似，使其更贴近用户的审美、认知观念。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/12/%E5%9B%BE%E7%89%8711.jpg)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/12/图片11.jpg)

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-includes/js/tinymce/plugins/wordpress/img/trans.gif)

文章主要按算法设计过程的先后顺序分为三个部分介绍：

1. 用户调查

此步骤为算法设计的构成性步骤。在此阶段，需要被试手工改进若干幅正交网络图的布局。通过这些结果，总结出贴近用户的 9 条设计原则，并将这 9 条原则运用到下一步的算法设计当中。

2. 算法设计

根据上一步的到的 9 条设计原则对算法进行设计。整个算法共分为四步：

    	- 图拓扑结构的分解：将图结构分解为外围的多个树结构与中间的唯一核心结构
    	- 核心结构布局：将中间的核心结构进行正交化布局
    	- 外围的树结构布局：将所有分解下来的树结构进行正交化布局，并将其重新插入核心中
    	- 最终调整：对图中不合理的位置进行最终优化

3. 最终评估

此步骤为算法设计的总结性步骤。此步骤将 HOLA 算法得出的结果与人工绘制结果、另一个 yFiles 自动化布局算法结果进行对比，让被试做一系列评估测试。最终得到结论，HOLA 算法得到的结果无论在美观、实用性上都明显优于 yFiles 算法结果，并且其布局质量能与手工结果的质量不相上下。

与此同时，可以看到，作者采用的整个算法设计方法也是前所未有的创新。在进行算法设计前后分别进行一次用户调查：一次为构成性的用户调查，为算法设计过程提供输入；一次为总结性的用户调查，对算法最终得到的结果进行评估。可以说，整个设计方法是以用户为中心的，充分体现了用户在这个过程中的重要性。

综上，本文的主要贡献主要可以分为三点：

1. 提出了 9 条贴近用户审美、认知的正交网络布局原则

2. 设计了一个显著有效的正交网络布局自动化算法

3. 运用了以用户为中心的设计方法进行算法设计
