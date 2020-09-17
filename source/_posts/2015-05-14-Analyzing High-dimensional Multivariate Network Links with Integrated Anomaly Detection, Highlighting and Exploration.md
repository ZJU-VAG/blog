---
title: "Analyzing High-dimensional Multivariate Network Links with Integrated Anomaly Detection, Highlighting and Exploration"
tags: ["论文评述", "报告"]
date: 2015-05-14
author: 朱闽峰
mail: minfeng_zhu@zju.edu.cn
mathjax: true
---

Analyzing High-dimensional Multivariate Network Links with Integrated Anomaly Detection, Highlighting and Exploration

Sungahnn Ko, Shehzad Afzal, Simon Walton, Yang Yang, Junghoon Chae, Abish Malik,Yun Jang, Min Chen and David Ebert, Fellow, IEEE

为了分析高维多变量网络，特别是点和边都有多个属性的网络图，本文提出了两个可视化设计来简化复杂的网络结构。

这篇文章用的是航班延误数据，包括延误原因和延误时间。Carrier Delay 是由于航空公司的问题，比如飞机的机械问题，NAS delay 是由于国家航公系统管制，Security Delay 包括因为安全漏洞的重新登机，设备筛选的等待时间，Late Arrival Delay 是由于同一架飞机在上一个飞机场就延误了，NAS delay 和 Security Delay 是政府原因，Late Arrival Delay 和 Carrier Delay 是航公公司的原因。这个数据中，主要的属性都图的边上，所以主要的可视化对象是边。

第一个可视化设计线（thread），

一条边由很多条线构成，线的颜色代表延误原因，线的粗细代表值得大小，值越大，线跨度就越大，就是越粗。图中黄色的线数值有 0.5 是最粗的，所以 carry delay 是导致航班延误的主要原因。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/t11.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/t11.png)

一条边由很多条线构成，线的颜色代表延误原因，线的粗细代表值得大小，值越大，线跨度就越大，就是越粗。

第二个设计花瓣（petal），

边的交叉重叠不利于我们可视化分析，我们把每条边的属性放置到结点上，在中心是一个饼图，所有从这个结点出发的航班的延误信息都统计在中心的饼图上。外层就是花瓣，花瓣编码的是某一个方向的航班的信息。所有到两条紫色射线的覆盖范围内目的地的航线都被统计在同一块花瓣上。花瓣的颜色的长度是延误时间值。在花瓣上的颜色展示的是 5 个延迟原因的分布。图中红色箭头所指的方向的主要延迟原因是航空管制延迟。当我们选择一个花瓣的时候，就会出现一个和所选方向一样大的园，用于比较。默认每朵花有 12 个花瓣，但是用户可以把花瓣进行合并或者拆分。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/p1.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/p1.png)

外层就是花瓣，花瓣编码的是某一个方向的航班的信息。所有到两条紫色射线的覆盖范围内目的地的航线都被统计在同一块花瓣上。

文章中还用了时间视图和邻接矩阵的可视化方法展示航班延误随时间的关系以及航线之间的相互关系，这些可视化方法将在案例中介绍。

在日历这个视图中，总体上来说 2007 年比 2006 有更多的航班延误，季节性上来说，每年 459 9 10 月份航班延误比较小，到了夏天延误都是比较高的。同时我们也看到不是所有节假日都是延误高峰，有些节假日的航班延误比较高，特别是冬天和夏天，有些节假日的延误就比较低。在天气比较糟糕的时候 比如暴风雪，也是造成延误的原因。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/t.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/t.png)

在时钟视图中，航班延误从早上 6 点开始不断增加，直到晚上 6 点达到最高峰。同时，我们可看到延误的原因主要是 Late Arrival Delay 其他延误原因基本都保持相同的比例。这说明如果航线有足够多的时间间隔，航班延误就可以被有效降低。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/t21.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/t21.png)

图 a ORD 在水平方向和数值方向 红色的像素点都非常明显，延误较多。在图 b 中 我们看到 ORD 这个机场延误原因主要是 Late Arrival Delay。同时，我们看到有 5 条竖直的蓝色点状线，以 EWR JFK LGA ORD PHL 等机场为目的地的飞机主要是因为 NAS delay，其中有四个机场是在 1969 年颁布的 HDR 的管理下，这从另一方面说明 HDR 的管理强度还不够。图中我们可以看到橘黄色和绿色比较多，航班延误的原因主要是机场自己造成的。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/m1.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/m1.png)

首先 我们看左边的两个机场 SEA LAS ，飞向 HNL（夏威夷）的飞机都有相当高的延误时间，主要原因是 Carrier Delay。再者我们看到 飞向东北方向的飞机，都有不同程度的蓝色，说明受到航空管制比较多。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/%E5%9B%BE%E7%89%8711.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/图片11.png)

总结：线和花瓣的设计可以作为一个新颖的设计很有效的解决了 网络图中边太多造成重叠的现象。花瓣的设计融入了地理方向信息，对于运输，交通活着物流产业等有地理信息的可视化设计很有帮助。但是，花瓣的设计能够展示的特性还是比较少的，许多 pattern 需要用邻接矩阵这些可视化方法才能展现出来，整个系统并没有以花瓣界面为核心，感觉比较零散。
