---
title: "The Spinel Explorer-尖晶石族矿的可视化交互分析"
tags: ["论文评述","报告"]
date: 2015-05-19
author: 林明
mathjax: true
---

论文：The Spinel Explorer- Interactive Visual Analysis of Spinel Group Minerals

作者：M. Luján Ganuza, Gabriela R. Ferracutti, M.Florencia Gargiulo, Silvia M. Castro, Ernesto A. Bjerg, Eduard Gröller, Kresimir Matkovic
发表：TVCG2014

## 简介

论文主要描述了The Spinel Explorer这个系统在尖晶石族矿分析方面所提供的方便，三角图、三棱柱图，两种可视化视图的实现，以及领域专家在使用上的积极反馈。

尖晶石最为一种小众的矿石，在形成之后，性质稳定，故而可以通过分析尖晶石的化学组成，分析其形成时期的地质环境，进而分析相应的地质变化，或应用于矿床的经济价值的开发。所以简化尖晶石的研究流程，有着很大的价值和意义。

在过去的工作流程中，地质专家在拿到样本的分析数据集后，需要通过特定的软件，将其画成特定的散点图或是三角图，经验分析其中特征后，统计筛选其中的部分数据，继续画图验证分析，如此往复。一般这样的一次分析工作，在原来要历时几天才能完成，而该系统中继承常用视图、三角图、三棱柱图的绘制，数据的统计和展示，图表的联动筛选和分析，使得原来繁复的工作在数小时内就能完成，意义重大。

### 三角图

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/%E4%B8%89%E8%A7%92%E5%9B%BE.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/三角图.png)

图1 三角图

图1中，显示为Fe、Cr、Al的成分比例图。其中保证Fe+Cr+Al的总和为1（100%），等值线离端点远近，说明相应的成分含量越高。上图中，

A：100%Fe

B：70%Fe+30%Cr

C：70%Fe+30%Al

D：70%Cr+30%Al

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/%E4%B8%89%E8%A7%92%E5%88%B7%E9%80%891.png)[
![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/%E4%B8%89%E8%A7%92%E5%88%B7%E9%80%89%E6%9B%B4%E6%AD%A3.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/三角刷选更正.png)

图2 三角图三角刷选

图2展示的是三角图中的三角刷选，及其代表的值域。上图为论文中的示意图，但略显不合理，下图为笔者在原图基础上的修正示意。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/%E4%B8%89%E8%A7%92%E5%9B%BE%E5%8C%BA%E5%9F%9F%E9%80%89%E6%8B%A9.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/三角图区域选择.png)

图3 三家图区间选择

上图为关于Cr的区间选择，不过操作提示却显示在Cr、Fe的边上，略显费解。==一个简介明了，且无歧义的选择操作，会更提高用户的体验。

### 三棱柱图

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/%E4%B8%89%E6%A3%B1%E6%9F%B1%E5%9B%BE.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/三棱柱图.png)

图4 三棱柱图

三棱柱图是三角图的维度拓展，在The Spinel Explorer系统中，这个新拓展出来的维度，可以显示出另外两个独立成分的分布。如在上图中，三角面投影显示的是铁酸根离子、铬酸根离子、铝酸根离子的分布，棱柱方向投影显示的是亚铁离子和镁离子的分布，而各个端点便是正负离子结合的端元（End-menbers）。
三棱柱图中的数据点只在地面、近底面、近侧面上投影，如图4所示。

## 系统预览

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/%E7%B3%BB%E7%BB%9F%E9%A2%84%E8%A7%88.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/系统预览.png)

图5 系统预览

该系统中，数据联动，下侧实时显示选中数据，左侧为各种成分范围区间，主视图中包含散点图、三角图、三棱柱图及其展开图、平行坐标图、盒式图，方便地质专家分析。

## 用户反馈与总结

### 用户反馈

论文中，作者用来自the Frontal Cordillera in Central Andes和Patagonia的样本，分别进行了尖晶石形成是地质环境的分析与地质变化的分析。
从用户（地质专家）的用户反馈来看

- 系统集成了用户分析所需的各个部件，省去了各个软件切换是用的大量时间耗费
- 系统中实时的数据统计和数据刷选，更是为用户提供了便捷
- 平行坐标图、三棱柱图等作为地质领域的新视图，为分析带来了便捷

从而，使得原本几天的分析工作，简化到数个小时便可完成，效果显著。

### 总结

#### 贡献

- 大大简化地质分析工作流程
- 两种新视图的应用

#### 未来工作

- 经验图表的比对工作（论文作者）
- 三角视图的刷选提高（笔者）