---
title: "SkyLens:Visual Analysis of Skyline on Multi-dimensional Data"
tags: ["论文评述", "报告"]
date: 2017-10-28
author: 朱闽峰
mail: minfeng_zhu@zju.edu.cn
mathjax: true
---

论文：SkyLens: Visual Analysis of Skyline on Multi-dimensional Data

作者：Xun Zhao, Yanhong Wu, Weiwei Cui, Xinnan Du, Yuan Chen, Yong Wang, Dik Lun Lee, and Huamin Qu

发表：IEEE VAST 2017

## 介绍

日常生活中，我们总是要在一个多维数据集中比较多个候选者，然后最终做出决定选择一个。例如，旅游的时候我们想要选择一个目的地，我们往往会考虑花费、气候、安全性等。当数据量比较大时，做选择就要进行多次对比，非常耗时。因此，一般会采用![img](http://www.cad.zju.edu.cn/home/vagblog/wp-includes/js/tinymce/plugins/wordpress/img/trans.gif)skyline 查询，自动的抽取出一系列优质的 skyline point 作为候选，这些候选不会影响最终结果。然而，Skyline 查询减少了需要考虑的数据，但是 1）用户还得在 skyline points 中查找自身喜好的数据，2）skyline points 数量可能仍然比较多。因此，我们需要一个比较 skyline 的工具。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/Picture1.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/Picture1.png)

## 挑战

比较 skyline 主要分两方面：首先是解释 skyline 查询的结果，一个 skyline point 的构成原因不一定是他在某个维度是最好的，也有可能多个维度的综合评判。然后是要比较多个 skyline point，我们需要从不同的维度，skyline point 的不同属性分析比较 skyline points 之间的优劣。

## 分析任务

分析任务包括以下 7 个方面：

1. 编码多维属性及其统计信息
2. 编码每个 skyline point 的支配子空间
3. 高亮多个 skyline point 的区别
4. 检测 skyline point 的聚类和离群点
5. 分析 skyline point 之间的支配关系
6. 帮助优化 skyline 查询
7. 支持过滤查询结果

## 可视化设计

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/Picture2.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/Picture2.png)

### Projection View

布局：基于距离的相似度矩阵，采用 t-SNE 降维方法进行布局。

可视化设计编码：

-   内圆颜色编码支配分数
-   外圆扇形编码属性值大小
-   扇形颜色编码与选定 skyline point 的属性差值

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/Picture3.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/Picture3.png)

### Tabular View

布局：列表示各个属性，行表示每一个 skyline point

可视化编码：

-   所有数据点按照某属性进行排列，灰色线代表 skyline point
-   所有 skyline point 按照某属性进行排列，蓝色条高度代表其他 skyline point 与此数据属性的平均差值
-   其他 skyline point 与此数据在各个属性上的差值
-   决定子空间的数量
-   显示当前 skyline point 排序和属性值

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/Picture41.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/Picture41.png)

### Comparison View

布局：环形布局，比较所有组合

(a)Radar chart 可视化编码:

雷达图展示 skyline point 各个属性值

每个轴上是属性分布

轴上的圆代表相对排序

蓝色虚线圆代表支配分数

(c)Domination glyph 可视化编码:

内部饼图代表支配分数的分布

饼图大小代表支配分数总量

外圆弧代表被唯一支配的数据点的数量

(d)中，显示 skyline point 和被支配的点的属性分布

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/Picture51.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/Picture51.png)

## 案例分析

Lorraine 想要选择一个适宜的地方享受一个月的假期。这个案例介绍了如何使用 SkyLens 找到一个适宜旅游的城市。案例中使用的数据库是 Numbeo quality-of-life （https://www.numbeo.com/quality-of-life/），数据库包括了176个城市和8个属性。整个操作流程分为以下几步：

1. 优化 skyline 查询结果。由于 Lorraine 只是想去度假，所以去除购买力和房屋支付能力两个属性在 skyline 查询中的影响。

2. 过滤 skyline 查询结果。Lorraine 想要体验亚洲以外的文化，通过洲属性过滤亚洲。

3. 重新计算 skyline query 得到 62 个候选城市。Lorraine 在 skyline 查询的结果中中发现了去年夏天去的维多利亚，想要了解成为维多利亚 skyline 的原因。

4. 在 Tabular View 中观察维多利亚气候排序。Lorraine 发现维多利亚的气候排名只是在众多 skyline 结果的中间位置，所以气候不是维多利亚成为 skyline 的原因。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/Picture6.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/Picture6.png)

5. 在 Tabular View 中观察维多利亚的其他排序。维多利亚在交通和环境方面排序较高，Lorraine 猜测是交通和环境使得维多利亚成为 skyline point。但是 Lorraine 看到维多利亚的决定子空间只有花费和环境，这说明在交通上面维多利亚不是最优的。

6. 查找优于维多利亚的城市。Lorraine 在系统中看到，在环境方面和交通有两个城市（惠灵顿和雷克雅维克）优于维多利亚，而维多利亚在花费上面优于两个城市。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/Picture71.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/Picture71.png)

在分析过程中，坚定了对交通和环境两个属性的需求，然而找不到花费优于维多利亚并且交通和环境不差于维多利亚的城市。

7. 高亮在（花费、交通、环境）子空间内的 skyline。于是 Lorraine 决定只关注于（花费、交通、环境）这三个因素比较优异的城市。

​ 于是 Lorraine 决定只关注于（花费、交通、环境）这三个因素比较优异的城市。

8. 在 Projection View 中找到各个属性都不差的格丹斯克 Gdansk 和克卢日-纳波卡。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/Picture8.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/10/Picture8.png)

9. 经过对比，格丹斯克在气候、交通和环境方面都优于克卢日-纳波卡，最终选择格丹斯克。

## 总结

文章提出了一个探索和比较 skyline 的可视分析系统，SkyLens。SkyLens 可以进一步抽象为对于多维数据的比较，比如优化算法中的最优点，可以简单得拓展到其他算法中。
