---
title: "Surprise！Bayesian Weighting for De-Biasing Thematic Maps"
tags: ["论文评述", "报告"]
date: 2016-12-07
author: zjuvis417
mathjax: true
---

论文: Surprise！Bayesian Weighting for De-Biasing Thematic Maps

作者: Michael Correll and Jeffrey Heer

发表会议: InfoVis 2016

主题地图经常被用来可视化事件热度在地理空间上的分布。然而，传统的主题地图可视化方法受困于已知基准率、采样失真以及归一化等问题，给用户认知带来了困难与偏差。本文利用贝叶斯统计思想，提出了一种全新的主题地图可视化技术。它通过突出异常事件，弱化常规事件来提高主题地图的可读性。

![](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/12/p1.png)

上图描述了加拿大各省份的犯罪情况分布。图(a)描述了犯罪数在各省份的分布情形，图(b)描述了犯罪率在各省份的分布情形，颜色越深，表示相应的犯罪数(率)越高。可以发现，图(a)和图(b)存在矛盾的结果。这是因为传统的主题地图可视化方法存在着两个方面的问题：当直接可视化事件数量分布时，容易受到人口分布因素的干扰（图(a)）；当可视化事件所占比率的分布时，容易受数据不确定性因素的影响（图(b)）。因此，本文提出了基于贝叶斯算法的Surprise Map可视化方法（图(c)）。

Surprise Map采用两种对立颜色编码数据的重要程度。本文认为，当观察得到的数据分布D与预期分布不相符时，相应数据项存在较大的分析价值，即为重要数据。当观察得到的数据分布与预期分布基本相吻合时，相应数据项不存在较大分析价值，即为不重要的数据。

本文方法的关键在于如何根据预期与实际数据计算Surprise的数值。Surprise的计算方法引用自2005年Wainer等人的工作。首先，本文根据简单、可解释的原则提出五个常用的预期模型M并给出条件概率的计算公式P(D|M) = 1-|D-M|。然后，选择若干模型构建模型空间，并定义先验分布P(M)。Surprise Map的工作亮点在于结合了贝叶斯方法，根据先验分布P(M)和实际数据D计算后验分布P(M|D)。计算方法如下：P(M|D) ~ P(D|M)P(M)。最后，文章利用相对熵来计算Surprise：
$$
K L(P(\mathscr{M} | D) \| P(\mathscr{M}))=\sum_{i=1}^{|\mathscr{M}|} P\left(M_{i} | D\right) \log \frac{P\left(M_{i} | D\right)}{P\left(M_{i}\right)}
$$
下面利用一个鸟类死亡率的案例来验证该方法的有效性。

![](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/12/p3.png)

上面各图的横轴从左到右表示1月到12月，纵轴从上往下表示鸟的不同种类。图(a)受困于几种鸟类的绝对数量过大，相应的死亡数量也较大，导致其它鸟类的死亡规律并不明显。图(b)受困于数据的不确定性，几个颜色最深的色块是数量较少的鸟类。图(c)采用Surprise的计算方法，突出了几个值得关注的死亡特征，有助于分析人员开展进一步的研究。

