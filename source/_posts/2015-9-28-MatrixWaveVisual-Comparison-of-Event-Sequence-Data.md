---
title: "MatrixWave:Visual Comparison of Event Sequence Data"
tags: ["论文评述"]
date: 2015-9-28
author: 朱闽峰
mail: minfeng_zhu@zju.edu.cn
mathjax: true
---

## 文章简介

事件序列是由一系列包含时间属性的事件组成，每一条事件序列包含了按时间排序的多个事件。网站的点击流数据也是一种事件序列数据。当用户访问网站时，他们在多个页面之间跳转的过程，可以作为分析人员分析这个网站浏览情况的一种数据。一直以来，桑基图（Sankey Diagram）是可视化这类数据的常用可视化方法。但是随着变量增多，跳转关系变复杂，桑基图就开始出现视觉遮挡。为了解决这个问题，作者提出了 MatrixWave 的可视化方法，用矩阵来代替节点之间的关系，使之能够可视化更大更密集的事件序列数据。[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/09/mw.jpg)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/09/mw.jpg)

# MatrixWave 结构

网站分析者通常比较关心用户在页面间的跳转关系，所以这篇文章忽略了事件的时间属性，只保留了时间上的先后逻辑关系。图 a 是提炼出来的网站点击流数据，第一行的用户从网页 A 跳转到网页 D 再跳转到网页 B，最后浏览完了网页 B 后关闭了整个网页。整一个流程可以由桑基图 b 展示。矩形结点表示特定网页，两个结点之间的连接表示网页之间的跳转。结点的大小表示该网页的流量，连接的大小表示从一个网页到另一个网页的跳转流量。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/09/matrixwave.jpg)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/09/matrixwave.jpg)

当数据量比较大并且转移关系比较密集的时候，桑基图酒会出现视觉遮挡。为了克服这个问题，MatrixWave 把结点间转移的关系用矩阵来表示，矩阵中的每个单元表示了结点间的转移流量。图 c 展示了 Step1 到 Step2 的跳转。同样，结点的大小表示网页的流量，矩阵中方形的大小表示网页间跳转的流量。为了展示用户关闭网页的动作 （对于分析用户行为有所帮助），增加了一个离开结点，由阴影表示。由此，相邻的步骤之间就可以用矩阵代替，构成了图 d 。为了展示用户浏览整个网站的路径，我们用之字形的走法把矩阵按照先后顺序连接起来，我们就可以在图 e 中观察用户的浏览过程。

# 用于比较的可视化编码

常用的可视化比较方法有四种：并列（juxtaposition）、重叠（superposition）、显示编码（explicit encoding）和动画（animation）。如图所示，X 和 Y 是两个数据，（a）（b）（c）依次是并列、重叠和显示编码方法。并列方法要求用户在两个数据之间不断比较，这里就要求用户记住另一个的数据位置，对用户来说不够方便。重叠是把两个数据放在一起，让用户比较，相比于并列方法更加简单，但是在元素比较多的情况下，图像就会比较混乱。显示编码直接显示了两个数据的差别，更为直观。动画方法需要把动画一遍一遍不断播放，同样不是很方便。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/09/compare.jpg)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/09/compare.jpg)

文章中，作者主要采取了显式编码这种视觉比较方法。在这里，我们需要编码两个信息，一是两个数据集的绝对流量，二是两个数据集比较的流量，这里称之为相对流量。如下图，对于结点，我们用大小表示两个数据集的绝对流量（同一个网页在两个数据集中流量的平均值），同时，用颜色编码相对流量，当网页在数据集 1 中的流量比较大时用紫色表示，当在数据集 2 中流量比较大时用橙色表示。类似的，对于矩阵单元，其内部方形的大小表示两个数据集中相应两个节点之间的平均转移流量，颜色采用了与结点一样的颜色方案来表示转移流量在两个数据中的差异。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/09/encoding1.jpg)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/09/encoding1.jpg)

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/09/matrixwave2.jpg)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/09/matrixwave2.jpg)

# 用户调研

为了评估 MatrixWave 的有效性，作者还开展了一个用户调研来比较 MatrixWave 和桑基图这两种表示形式。结果显示，相比于辛基图，使用 MatrixWave 可以获得更高的准确度（95\% VS 79\%）和更少的完成时间（34.0s VS 38.2s）。MatrixWave 相比于传统的桑基图能够有效地展示大且密集的事件序列数据集，桑基图则可以用来展示数据量比较小的数据，因为桑基图更容易被用户接受。然而由于 MatrixWave 的布局是之字形的，把矩阵旋转过 45 度之后不利于用户的观察分析。
