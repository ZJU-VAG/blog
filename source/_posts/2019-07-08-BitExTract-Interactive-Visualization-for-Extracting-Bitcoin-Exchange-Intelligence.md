---
title: "BitExTract: Interactive Visualization for Extracting Bitcoin Exchange Intelligence"
tags: ["论文评述", "报告"]
date: 2019-07-08 23:00:00
author: 王毅超
mail: 403624799@qq.com
mathjax: true
---

发表：IEEE TVCG 2018

作者：Xuanwu Yue, Xinhuan Shu, Xinyu Zhu, Xinnan Du, Zheqing Yu, Dimitrios Papadopoulos, and Siyuan Liu（第一作者：岳轩武，香港科技大学在读博士；通讯作者：Siyuan Liu，宾夕法尼亚州立大学 smeal 商学院助理教授)

简介：这篇 paper 介绍了一个分析比特币交易的可视化系统：BitExTract

## 系统概览

![img](http://www.cad.zju.edu.cn/home/vagblog/images/20190708/wps1.png)

## 相关工作

现有工作主要分为三个层面，如下图所示：

​ ![img](http://www.cad.zju.edu.cn/home/vagblog/images/20190708/wps2.jpg)

​ 整体上，作者借鉴已有部分研究成果的，并且针对文中提出的缺少和不足做了对应的设计。最终融合，做出了一个分析比特币交易演化的可视化系统 BitExtract。

## 任务分析

​ 在项目的进行过程中，作者与 4 位专家，2 位比特币金融专家、2 位高级交易专家，有长达 6 个月的合作。在 6 个月的合作中，他们针对该系统不断的讨论、设计、修改、迭代。并提出了基于三个层面的，6 个核心问题。其中有两个关键词：第一，时间，随时间演化情况。第二，其次特定事件的影响情况。![img](http://www.cad.zju.edu.cn/home/vagblog/images/20190708/wps3.jpg)

## 面临挑战

1. 交易数据量大，10GB+

2. 交易网络复杂，要考虑交易的数量大小、频次、地理位置

3. 可视化设计既要全面、又要易于被理解

## 本文贡献

1. 第一个允许用户通过交互去分析、比较不同比特币交易平台演化的可视化系统

2. 块状平行坐标图同时显示出多个交易平台随着时间的演化

3. 将系统整合进专家和实践者的分析中，发现更深层次和更有价值的背后信息

## 数据

### 初始数据

​ 该项目的数据可以描述为分布在 5 个大洲的 65 个交易平台，在 7 年间，超过 6000 万次交易，在结合一些新闻事件信息和公司信息。形成最初的数据

![img](http://www.cad.zju.edu.cn/home/vagblog/images/20190708/wps4.png)

### 数据加工

​ 比特币的数据交易时基于 NxN 的交易，但是这种交易数据难以被理解和可视化，该项目将其按比例拆解成 1 对 1 的交易。

![img](http://www.cad.zju.edu.cn/home/vagblog/images/20190708/wps5.jpg)

并在最初的数据中提取出三个参数：Market Share /Network Standing /Business Proximity。具体解释如下图：

![img](http://www.cad.zju.edu.cn/home/vagblog/images/20190708/wps6.jpg)

## 可视化面板介绍

![img](http://www.cad.zju.edu.cn/home/vagblog/images/20190708/wps7.png)

**概览介绍**

​ **comparison View**整体用来表达整体市场和交易平台随时间交易的变化情况

​ **Massive Sequence View** 主要反映整体市场和交易平台的买和卖的情况随时间的变化情况

​ **Connection View** 主要用来表达交易平台之间的关系以及单个情况

​ **Exchange List Panel** 可以概览每个交易平台的情况，以及作为一个选择的面板，用来选择一个或多个交易平台。

### 单个视图介绍

1. **Comparison View**

![img](http://www.cad.zju.edu.cn/home/vagblog/images/20190708/wps8.jpg)

​ 如上图，Comparison View 建立在平行坐标的基础之上，平行坐标是用来表达高维信息的。而这里的高维，指的则是不同的时间段。

​ 一个竖状的大矩形记录了一个月的交易历史。它的宽度代表该月总计客户数量。矩形中的每一行代表某个交易公司。那么行与行的排序是什么方式呢？有三种（network standing，买卖差额，或者交易数量的多少）

​ 还有两种数据填充方式（一个是买卖差额，一个是交易数量的大小）营业额指的是：收到的数量减去发送出去的数量，有点像平常商家最终的利润收入（是收入减去支出）。红色表示最终是正的，蓝色表示是负的。

之间的连线连接的是同一种公司，或者说是同一公司。如上面的黄线突出显示某一公司。

​ 该视图回答了任务分析中的两个核心问题：T5 单个平台的表现随时间如何变化？T6 单个平台的有什么重要的特殊时期？

2. **Exchange List Panel**

![img](http://www.cad.zju.edu.cn/home/vagblog/images/20190708/wps9.jpg)

​ Exchange List Panel 面板主要是用来：让用户快速选择一个确定的交易平台，在 USD 中查看它的历史交易数量。每一个小的柱状图显示的是某一个国家，随着时间交易数量的变化。用户可以选择两种排序方式：一种是按首次进行交易的时间先后排序。时间早的排下面，时间晚的排上面，一种是按大洲排序，即亚洲的放一块，欧洲的放一块，类似的。每个颜色是一个大洲。

3. **Massive Sequence View **

![img](http://www.cad.zju.edu.cn/home/vagblog/images/20190708/wps10.jpg)

​ Massive Sequence View 提供了一个易被理解的全局买卖概览图。颜色填充依据买卖差额。红色的代表卖出的多于买入的，蓝色代表买入的多余卖出的。根据一个一个单位来绘制。

​ 下部分的图表，横坐标是时间，纵坐标是比特币不同时间的价格。上下两张图共享时间轴。

​ 上部分的图表：每行是一个交易所，右侧写着交易所的名字，行与行之间的排序是按照参与交易的年龄大小进行的。新出现的在上面，年老的在下面。水平向的长条填充反映出：买卖差额。在某个时间点是卖出大于买入呢？还是买入大于卖出？

​ 2013 年到 2015 年斜边比较明显，表明：有大量交易所出现，开始交易。16 年之后有多出空白，表示有部分交易所倒闭、停业。

​ 整体而言基于这个视图可以回答 T1/T2/T3 三个问题

​ T1 整体市场网络的模式随着时间如何演化？

​ T2 特定的事件对整体市场会有什么影响？

​ T3 平台之间的联系随着时间如何变化？

![img](http://www.cad.zju.edu.cn/home/vagblog/images/20190708/wps11.jpg)

​ 在两种交互下 Massive Sequence View 会有不同的显示方式：

交互 1：

​ 如果选定某一个交易平台，右上角，就会显示和该交易平台相关的所有交易。而整体面板的也会做相应的联动变化。

交互 2：

​ 选择一定的时间区间，新闻面板就会显示相应时间段内，所发生的的相关事件。时间段的选择也会影响 Comparison View 视图和 Connection View 视图的时间段变量。

4. **Connection View**

![img](http://www.cad.zju.edu.cn/home/vagblog/images/20190708/wps12.jpg)

​ Connection View 主要目标是可视化具体交易行为，并辅以地理层级信息，如大洲、国家、个体。主要回应前面的 T3/T6 问题：T3 平台之间的联系随着时间如何变化？T6 单个平台的有什么重要的特殊时期？

​ Connection View 是一个比较综合的视图，由两个部分组成：外侧、内侧部分。一个大洲是一种颜色，同一个大洲内，不同国家用不同的颜色透明度来表示。外圈的弧长由这个大洲的交易数量在市场的份额比例决定。也可以选择某一个弧，由“世界视图”进入“大洲内部”的交易视图。中心一圈节点连线，代表两者之间的 Business Proximity,具体计算公式如图。 Vt 代表 a 和 b 之间的交易数量。而 Ft 代表 a,b 之间的交易频率。a 和 β 在这里大小相同，因为他们认为两个因素对 Business Proximity 同样重要。也可以将任一节点拖至中间，变成个体视图，只显示和该平台相关的交易份额和交易平台

个体视图：

![img](http://www.cad.zju.edu.cn/home/vagblog/images/20190708/wps13.jpg)

​ 个体视图，中心节点和周围节点的连线的粗细代表交易的数量大小，从中心节点向外代表一段时间，上面的每一个点代表一个时间点。在该线上，箭头越大越密，代表此刻交易额越大。红色代表发出比特币，蓝色代表收入收入比特币。

## 用户评估

参与人员：领域专家、比特币交易者和研究者

三个案例研究：

1. **市场繁荣原因的探索**

![img](http://www.cad.zju.edu.cn/home/vagblog/images/20190708/wps14.jpg)

​ 通过 Comparison View 可以观察到从 2015 年 7 月到 2015 年 12 月，矩形的宽度在变宽，这也意味着这个市场逐渐繁荣。为了探究繁荣背后的原因，查看该时间段的 Connection View 发现基于中国的交易平台占据了市场分额的主要部分。在 Exchange List Panel 里面选择了中国的交易平台后，观察发现中国的交易平台的份额都在逐渐上升。所以确定该时间的比特币市场繁荣是因为中国市场的大量交易导致。

2. **分析政策事件的影响**（中国禁止比特币交易）

![img](http://www.cad.zju.edu.cn/home/vagblog/images/20190708/wps15.jpg)

​ 中国禁止比特币交易，具体是体现在 2017 年的 2 月中国人民银行对中国最大的比特币交易平台“火币”进行监管服务，之后该平台中国区提取比特币的业务暂停。随着监管开始，该平台的亚洲市场份额，有大幅度下降，该平台和中国其他比特币交易平台间的联系也大幅度减弱，该平台的北美市场份额有所增加。随着 2017 年 6 月该平台重启比特币提取业务，该平台恢复了部分和中国其他平台的联系。但是中国的市场份额并没有恢复。

![img](http://www.cad.zju.edu.cn/home/vagblog/images/20190708/wps16.jpg)

​ 查看 Comparison View 发现该平台的市场份额，随着监管开始，市场份额下降，随着监管结束，市场份额有一定的恢复，但是亚洲的市场份额没有恢复。

3. **两家交易平台在使用 BitGo 后的，可靠性的对比探索**

BitGo 服务，可以理解为一个监管钱包，或者一个中间人。发出的比特币要经由该钱包，才能发出。

![img](http://www.cad.zju.edu.cn/home/vagblog/images/20190708/wps17.jpg)

Bitfinex 和 Kraken 是两家表面看似相同的交易平台，也都使用了 BitGo 服务。但是到底谁更可靠呢？

从上面的 A/B 两图可以看出两交易平台在使用该服务后，买卖情况表现基本相同

![img](http://www.cad.zju.edu.cn/home/vagblog/images/20190708/wps18.jpg)

​ 分析上图 Comparison View,发现两者 Inverse Volatility 有很大的差别。由指标含义可以推测：两平台在使用 BitGo 服务后，可靠性方面 Kraken 大于 Bitfinex。分析细节得知是由于：Bitfinex 将绝大部分比特币都交给了 BitGo 监管服务。自己钱包只留了非常少的一部分。而 Kraken 只在 BitGo 放了必要数量的比特币，自己保留了绝大多数比特币。因此 Kraken 的 Inverse volatility 几乎没有受影响，这也保证了其平台的稳健性。之后 2016 年 8 月，BitGo 服务被黑客攻击，导致价值 7000 万美元的比特币被盗，Bitfinex 也因此终止了所有与其交易伙伴的关系。

## 总结-未来工作

​ 该系统通过从各个层面对市场进行解读，也回答了一开始提出的 6 个核心问题。从而更好的帮助研究者和交易者去分析和决策。作者有意向在未来将该系统拓展成实时系统、增加应对短期冲击分析、能够分析其它数字货币。
