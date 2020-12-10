---
title: "Formalizing Visualization Design Knowledge as Constraints: Actionable and Extensible Models in Draco"
tags: ["论文评述", "报告"]
date: 2019-01-26
author: 胡元哲
mail: cadhyz@zju.edu.cn
mathjax: true
---

论文：Formalizing Visualization Design Knowledge as Constraints: Actionable and Extensible Models in Draco

作者：[Moritz D](https://www.ncbi.nlm.nih.gov/pubmed/?term=Moritz D[Author]&cauthor=true&cauthor_uid=30137004), [Wang C](https://www.ncbi.nlm.nih.gov/pubmed/?term=Wang C[Author]&cauthor=true&cauthor_uid=30137004), [Nelson GL](https://www.ncbi.nlm.nih.gov/pubmed/?term=Nelson GL[Author]&cauthor=true&cauthor_uid=30137004), [Lin H](https://www.ncbi.nlm.nih.gov/pubmed/?term=Lin H[Author]&cauthor=true&cauthor_uid=30137004), [Smith AM](https://www.ncbi.nlm.nih.gov/pubmed/?term=Smith AM[Author]&cauthor=true&cauthor_uid=30137004), [Howe B](https://www.ncbi.nlm.nih.gov/pubmed/?term=Howe B[Author]&cauthor=true&cauthor_uid=30137004), [Heer J](https://www.ncbi.nlm.nih.gov/pubmed/?term=Heer J[Author]&cauthor=true&cauthor_uid=30137004).

发表：IEEE TVCG 2018

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/01/Screen-Shot-2019-01-26-at-9.27.20-PM-2.png)

## Introduction

程序员编写的可视化图表与专家眼中的设计标准总存在差距。我们无法每次都向可视化专家咨询设计上的意见，所以我们需求将设计标准，研究成果应用于自动化设计工具的正式框架，这些工具有助于对于推荐数据的合理编码和正确的视觉探索方式。我们建议将可视化设计标准建模为约束的集合，并结合从实验数据中学习到的软约束的权重，使用求解器把理论设计知识具体的，可扩展和可测试的表达出来的系统。我们使用 Draco 实现了我们的想法，Draco 是一个基于答案集编程（ASP）的基于约束的系统。本文的贡献可以概括为以下三点：

-   本文提出了一种自动化可视设计的规范框架 ，使用一些设计规范来帮助用户制作好的可视化设计
-   本文将可视化设计建模为约束条件进行最优化求解，有些约束条件是硬性条件(必须满足)，有些是软性条件(带有惩罚)
-   本文基于 Clingo，这是一种基于答案集编程(ASP)的求解器，还有 Vega-Lite, 这是一种 json 化的可视化图表语法
    ![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/01/Screen-Shot-2019-01-26-at-9.08.18-PM.png)

## Related Work

### Visual Encoding Principles

可视化设计标准定义了在可视化图表当中最基本的概念，mark 是可视化中的基本图形元素，channel 是表达数据的方式和频道。比方说一张折线图，它的 mark 是线段，channel 是位置(高低)。
![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/01/Screen-Shot-2019-01-26-at-7.58.11-PM.png)

除此之外，可视化还将数据类型 data 定义为：continuous(数值型，10 英尺，23 岁)，ordered(离散型，有大小之分，如星期几)，categorical(离散型，无大小之分，如苹果，梨子)三类。将处理数据 Aggregate 分为，sum, mean，count，median。

### Vega-lite

Vega-Lite 吸收了前任对于视觉编码的研究成果，并参考了 d3，visQL(tableau 前身)等可视化语言。 Vega-Lite 结合了传统的图形语法，提供了可视化编码规则和分层和多视图显示。用户通过组合选择来指定交互式语义。在 Vega-Lite 中，选择是一种抽象，它定义输入事件处理，兴趣点和包含测试的谓词函数。选择通过用作输入数据，定义比例范围或通过驱动条件逻辑来参数化可视编码。 Vega-Lite 编译器自动合成必需的数据流和事件处理逻辑，用户可以覆盖这些逻辑以进行进一步的自定义。

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/01/Screen-Shot-2019-01-26-at-8.41.09-PM.png)

###Automated Visualization Design

过去的自动化设计系统使用预先设计的规则对用户的需求进行判定，通过聚类和穷举(dfs)，最后得到一个有限集合，通过 rankSVM 等排序算法，得到最后的偏好。这种方案的缺陷在于，穷举的搜索策略是深度优先搜索，复杂度过大，还有很多回溯，这对于大型设计空间来说效率低。 Draco 使用现代约束求解器和标准化的表示语言，并且还提出了软约束的概念，增加了灵活性。最近的一篇自动可视设计系统是来自 idl 实验室的 Voyager 2。
![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/01/Screen-Shot-2019-01-26-at-8.52.31-PM.png)

## Modeling Visualization Design In Draco

-   硬性可视化约束规范
-   如前文所述，Draco 当中的规则分为硬规则和软规则。硬规则包括一些可视化图表内部的逻辑(比方说折线图无法表示种类等等)，还有许多用户自己定义的偏好。这些规则必须被满足。

        - Mark ∈ {bar, line, area, point}
        - Channel ∈ {x, y, color, text, shape}
        - Field ∈ {site, year, age}
        - Type ∈ {categorical, continuous}
        - Aggregate ∈ {sum, mean, count, median}
        - Zero ∈ {yes, no}

    我们还可以写多条件 硬规则，如下所示

-   :- X
    X 这种情况不会发生

-   :- channel(\_,shape), not mark(point)
    表明对于形状编码必须是是“点” ，其他标记类型（如区域，线，条或文本）不能对形状进行编码。

-   :- mark(bar), channel(E, y), continuous(E), not zero(E)
    表明必须使用零作为基线的垂直条形图。

软性可视化约束规范

-   :~ X [w]
    倾向于 X 这种情况不会发生，如果违反那么会有 w 的惩罚

-   :~ continuous(E), not zero(E) [5]
    表示模型更喜欢连续字段的坐标从零开始，并且违反规则会使这个模型的 cost 增加 5

通过以下的语句定义数据的信道偏好设置

-   :~ channel(E,y), type(E,nominal). [0]
-   :~ channel(E,x), type(E,nominal). [1]
-   :~ channel(E,column), type(E,nominal). [2]
-   :~ channel(E,color), type(E,nominal). [3]

假设我们有 m 个软性约束，pi 为第 i 个约束，每个约束的惩罚为 wi

令 S = {(p1, w1)… (pi, wi)} npi(v)是 v 这种视图违反软约束 pi 的次数，那么 Cost 可以定义为：

这样我们通过求解器可以通过这些权值得到不同可视化图表的偏好。

## User Study

### 比较试验

本文将 Draco 与 voyager2 中使用的 CompassQL 求解算法做比较，将 CompassQL 中的规定转成 Draco 中的 -: X(硬规则)，将 CompassQL 中的偏化转成 Draco 中的 ~:X(软规则)。实验结果可以发现，CompassQL 中复杂的规则语句在 Draco 只需要短短几句。

### 使用 rankSVM 训练软约束参数

本文使用 lY. Kim and J. Heer. Assessing effects of task and data distribution on the effectiveness of visual encodings,和 lB. Saket, A. Endert, and C. Demiralp. Task-based effectiveness of basic visualizations. 所用到的实验数据，训练软约束参数，获得了比原先自定义不同的可视化结果。

## Conclusion

作为今年 infovis 的 best paper，本篇文章确实可圈可点，本论文的文档，在线演示可以看https://uwdata.github.io/draco/

### 总结

-   本文提出了目前最完整的自动化可视设计框架
-   这个框架具有高度灵活性和可训练性
-   未来它将支持推荐更复杂的图表或者仪表盘
-   这个系统为 理解可视化语法，创新可视化设计，理解不同编码的感知 都- 有不可或缺的作用
