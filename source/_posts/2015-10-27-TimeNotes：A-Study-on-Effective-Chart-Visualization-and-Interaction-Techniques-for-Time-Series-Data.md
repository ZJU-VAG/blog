---
title: "TimeNotes：A Study on Effective Chart Visualization and Interaction Techniques for Time-Series Data"
tags: ["论文评述"]
date: 2015-10-27
author: 蔡西文
mathjax: true
---

## 简介

在过去的十年中人们对于时间序列数据的兴趣出现了激增。在分析时间序列数据时，我们遇到了的挑战之一是相比于大容量的数据存储，屏幕分辨率太小。本文的作者评价了现存的一些方法，在此之上提出了TimeNotes的技术，并通过用户研究比较了他们的有效性。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/10/%E5%9B%BE%E7%89%8721.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/10/图片21.png)



[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/10/%E5%9B%BE%E7%89%8712.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/10/图片12.png)

本文对于过去时间序列数据可视化的相关研究做了一个详尽的调查，提出的TimeNotes主要是基于Stack Zoom的方法。在Stack Zoom中，整体视图以树型结构表示，下层子元素是对父元素中一个时间片段的放大，每一层元素共享整个视图宽度，且各个元素占有的宽度相同，而其对应的父元素中的片段宽度不等，因此上下层之间是不等比例的缩放。TimeNotes对于Stack Zoom进行了改进，使得相同父元素的子元素共享其元素的宽度，这些子元素占有的宽度与其对应的父元素中的片段宽度成比例，因此在具有继承关系的上下层之间是等比例缩放；此外TimeNoes还加入了重叠（图中右下角）和提升的功能，能有助于用户进行更好的比较。

## 用户研究

本文的关注点主要用于测试具有清晰的node-link关系的层次结构的有效性。作者选择将TimeNotes与StackZoom进行了比较，以评估它的有效性。通过咨询生物学家，作者将一些典型的分析行为分成了两个类别，并设计了五个task：



- A.Hierarchy Navigation（Leaf Counting）
- B.Comparison（Amplitude）
- C.Comparison（Frequency）
- D.Hierarchy Navigation (Zoom/Pan and Labeling)
- E.Hierarchy Navigation (Label Analysis)

用户研究的结果证实了TimeNotes的技术要比StackZoom更好。

此外作者还展开项现场研究研究，通过观察生物学家使用软件，回答他们的问题以及与他们讨论，获得了一些反馈，并总结如下：



- 缩放和平移可以提供概览和效率
- 层次的布局有助于在不同尺度上的平列的比较和思考
- 重叠有助于比较
- 在展示中的分解有助于交流