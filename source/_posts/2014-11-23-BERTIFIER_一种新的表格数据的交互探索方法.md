---
title: "BERTIFIER: 一种新的表格数据的交互探索方法"
tags: ["论文评述"]
date: 2014-11-23
author: 尚平平
mathjax: false
---

论文：Revisiting Bertin Matrices: New Interactions for Crafting Tabular Visualizations

作者：Charles Perin, Pierre Dragicevic, and Jean-Daniel Fekete, Member, IEEE

发表会议：InfoVis 2014

表格数据在日常生活中很常见，对表格数据的处理、探索工具也非常多，但作者调查发现已有的系统还是有很大的改进空间，如下为作者对已有系统的调查，行代表系统，列代表特性，其中最后一行为本文系统，可见本文系统在很多特性上都得分很高。

![](http://www.cad.zju.edu.cn/home/vagblog/images/20141123/2014_11_23_BERTIFIER1.png)

本文是基于 Jacques Bertin 提出的操作表格数据的思想：

1. 对 cell 进行编码
2. 重排或聚类行和列，揭示模式。探索表格数据的很多研究也都是基于该思想的。

本文系统流程如下：

1. 原始数值数据
2. 数据编码并可视化
3. 最终结果（矩阵重排，注释等）

![](http://www.cad.zju.edu.cn/home/vagblog/images/20141123/2014_11_23_BERTIFIER2.png)

系统界面如下：

![](http://www.cad.zju.edu.cn/home/vagblog/images/20141123/2014_11_23_BERTIFIER3.png)

如图所示，本文提供了很多交互工具，如 8 种 cell 编码方式、调整行或列的高度或宽度、不同行或列单独编码。此外，本文在矩阵重排时，在一般的重排算法之上提供了一些预处理，如绑定一组行或列、指定某行或列的排序。对于发现的模式，还可进行注释，最后将图片导出，以作他用。

本文提供的八种编码方式如下图所示：

![](http://www.cad.zju.edu.cn/home/vagblog/images/20141123/2014_11_23_BERTIFIER4.png)

本文所用矩阵重排算法：“optimal leaf ordering”— OLO。

​ 算法输入：向量列表和距离度量；

​ 算法输出：已排序向量；

​ 该算法基于的思想为：使得连续的向量之间距离的总和最小。

​ 用户调研：8 位用户参与了调研，除了一位用户表示用本文系统得到的知识用 spreedsheets 也可以获得，其他用户都表示本文系统简单易用，并能得到一些新的知识。

总之，本文提出的系统及交互方法，虽没有特别出奇，但却简单易用，无 Infovis 背景的用户也能方便使用。未来在类别型数据处理、提高扩展性等方面做进一步探索。
