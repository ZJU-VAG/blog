---
title: "IBM Watson Analysis——用Watson做可视分析"
tags: ["其他"]
date: 2014-12-08
author: 夏菁
mathjax: true
---

关注可视化的同学们大概还记得红极一时的 IBM 在线可视化工具[Many Eyes](http://www-969.ibm.com/software/analytics/manyeyes/)，用户可以上传自己的数据，套用里面的可视化组件生成数据可视化。

“嗯，这样很好，把数据漂亮地展示出来了。但是我只关心我的数据业务，我还想在数据上做点分析，能再智能一点么？”相信 IBM 已经听到了客户们的意见，所以就有了现在的[IBM Watson Analysis](http://www.cad.zju.edu.cn/home/vagblog/www.ibm.com/software/products/en/watson-content-analytics)。

IBM 把 Watson Analysis 的功能概括为非结构化信息的组织、聚合、分析以及可视化，最终目的是让用户发现数据价值。

用户使用 IBM Watson Analysis 对市场数据进行分析，最终制定出优惠券方案。用户首先导入表格数据，系统自动评估数据质量（也就是对数据的有效性、数据缺失等进行评估）生成数据质量报表。进一步分析之前，系统在属性预览中根据数据类型可视化每个属性的大致分布。基于对各个属性的基本认知，用户以其中一个属性为目标(target)继续分析，结果通过几个可视化分别列出该属性的最佳关联属性、其它关联属性以及其它可能属性，通过调整关联属性的个数用户还能看到多个属性作用下目标属性的变化，以及这些属性是如何对目标属性进行变化。

从案例中可以看出 IBM Watson Analysis 的实现，其可视化基于 Many Eyes，分析过程包括数据质量分析以及数据维度关联分析两个方面。

IBM 称他们将在不久的将来把 Watson Analysis 服务开放给个人和企业级用户使用，喜大普奔~~
