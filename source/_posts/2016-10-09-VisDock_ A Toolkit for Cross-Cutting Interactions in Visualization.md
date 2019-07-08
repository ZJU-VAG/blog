---
title: "VisDock: A Toolkit for Cross-Cutting Interactions in Visualization"
tags: ["论文评述", "报告"]
date: 2016-10-09
author: 梅鸿辉
mathjax: true
---

论文: VisDock: A Toolkit for Cross-Cutting Interactions in Visualization

作者: Jungu Choi, Deok Gun Park, Yuet Ling Wong, Eli Fisher, and Niklas Elmqvist

发表期刊: TVCG 2014



VisDock提供可嵌入D3代码的JS库，为D3创建的可视化添加额外的工具栏（类似于PS/AI），可以简单地添加各种交互如平移、缩放、框选、添加标签等等操作。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/10/fig1.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/10/fig1.png)

VisDock的设计理念源于图形编辑软件如Photoshop、Adobe Illustrator等。与其类似，VisDock提供工具实现多种交互方式：选择、查询管理、导航和标注。
选择包括点选、框选、套索等。在选择的基础上，VisDock还提供类似于PS、AI中的图层管理的查询管理，对多次选择的结果可以分别进行操作，并能对多个选择结果进行交集、并集等集合操作。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/10/fig2.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/10/fig2.png)

VisDock能为可视化程序添加方便的平移、旋转等导航功能，并能添加鸟瞰图（Birdview）增强感受。VisDock提供的标注功能能随着图形的移动、变形自动更新点和区块的位置和形状。
作者对两种用户群体：可视化程序的编写者，以及可视化客户端的终端用户分别进行了调查评估，结果令人满意。
总体来说，VisDock的思路非常新颖，它能为原有的可视化结果额外嵌入交互功能。但实现上仍不完善，仅包含一些简单的通用性交互，并且需要额外插入大量代码；由于仅操作图形而不涉及内在数据，限制了交互种类（例如无法进行筛选、排序等操作）。

