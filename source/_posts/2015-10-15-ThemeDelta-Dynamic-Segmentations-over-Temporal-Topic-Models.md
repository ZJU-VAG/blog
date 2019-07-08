---
title: "ThemeDelta: Dynamic Segmentations over Temporal Topic Models"
tags: ["论文评述"]
date: 2015-10-15
author: 谢潇
mathjax: true
---

## 简介
许多可视化分析系统都需要对动态变化的趋势进行分析。通常情况下，趋势可以使用具体的关键词或者概念来表示，主题可以用主题内出现的关键字来表示。不同时刻趋势所从属的主题的变化就体现了趋势的动态变化。为了体现出趋势的收敛与分散，作者设计出了ThemeDelta这个系统，使用了一种时间分割的算法来提取趋势变化的特征并在前端将其可视化。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/10/%E5%9B%BE%E7%89%871.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/10/图片1.png)



## 后端

后端使用了一种时间分割算法对文档集合进行时间上的分割，使得在分割处前后文档集合的主题发生显著变化。作者按时间顺序遍历数据并通过评估两个相邻窗口的的主题相似性来对数据进行分割。[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/10/%E5%9B%BE%E7%89%8711.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/10/图片11.png)

计算相似性时，作者定义了一个相似矩阵和两种分布。相似性矩阵如上图，数值代表了两个主题中关键词相同的个数。两种分布分别是行分布p(R)和列分布p(C)。对于两窗口间主题的相似性，作者定义为两窗口间所有的行分布和列分布与均匀分布的相对熵的平均（见下图）。

可以看出，F最小值为零，F越小，两窗口间的主题相似性越小，主题变化就越显著。当F值达到局部最小时，就将两窗口取出，在剩余的数据中继续分割。
[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/10/%E5%9B%BE%E7%89%872.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/10/图片2.png)[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/10/%E5%9B%BE%E7%89%873.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/10/图片3.png)

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/10/%E5%9B%BE%E7%89%874.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/10/图片4.png)

## 前端

作者使用了如下的可视化编码：

- 使用线条的粗细来表达关键词的权重。
- 使用颜色来表达关键词的类别。
- 使用渐变线的端点代表趋势的开始或结束。
- 连接垂直距离上最接近的趋势实例（关键词）。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/10/%E5%9B%BE%E7%89%875.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/10/图片5.png)

## 实例

下图使用的数据源是美国总统大选中罗姆尼的演讲稿。红色部分代表只有罗姆尼提到过的关键词，绿色部分代表罗姆尼和奥巴马都提到的关键词。可以看到在Apr 18 2012 – May 02 2012前后主题有巨大的变化。在具体查看演讲稿后作者发现在这一时间前罗姆尼进行的是共和党党内选举，而在之后是进行总统大选。
[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/10/%E5%9B%BE%E7%89%876.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/10/图片6.png)