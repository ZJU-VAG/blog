---
title: "DecisionFlow：高维时序事件数据的可视分析"
tags: ["论文评述", "报告"]
date: 2014-10-10
author: 朱标
mathjax: true
---

论文：DecisionFlow: Visual Analytics for High-Dimensional Temporal Event Sequence Data  
作者：David Gotz and Harry Stavropoulos  
发表会议：vast 2014

本文使用的数据是由一个美国医疗机构提供的，该数据记录了从客户被接收开始的所有事件，一共有 32000 个客户，8000 种事件类型。每个事件都由三个要素组成，即事件类型、发生事件和发生主体（event type，time，entity），由一系列此类事件组成的数据就是题目中提到的时序事件数据（ Temporal Event Sequence Data），而高维（High-Dimensional ）指的是事件类型非常多。

本文主要的动机是由于之前的方法都不能处理维度（事件类型）超过 20 的此类数据，主要由于高维数据在可视表达上容易产生混乱，不便于用户观察、交互。因此，本文主要着眼于解决高维的问题，能对之前提到的医疗数据进行交互、有效的可视分析。

传统上，领域专家对此类医疗数据分析的目的是为了分析某个病症与哪些因素有关。他们的分析过程分为两步：首先，定义一些选择条件对病人进行筛选；然后，使用统计分析软件（SAS）对筛选结果进行分析。本文方法也遵循了这个流程，但是可视编码和交互的定义使得用户无需编程即可快速、高效地进行分析。

#### 本文方法介绍：

1. 首先，需要用户对时序事件数据进行 query。一个 query 由 Preconditions、Episode 和 Outcome 三个部分组成：Episode 部分对应用户希望得到并用于后续分析的数据；Preconditions 在这个数据里面相当于客户的病史，作为一个检索条件，但是对应的数据并不参与后续分析；Outcome 则可以理解为用户需要分析的病症。下图(a-c)定义的 query 解释如下：用户想要分析的是在发生心绞痛之后 18 个月内进行过心脏瓣膜置换术的用户在这段时间内以及心绞痛发生前 1 年的数据，先决条件是这些用户要有至少 3 次的血脂异常病史，并且最后得了主动脉上的某种疾病。  
   下图(e)是对搜索结果的一个表意性图解，如果满足(a)(b)条件的，就用颜色进行高亮编码，对于(c)，如果有这种病症的客户，就用一个红点表示，反之留白。

[![](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/10/%E5%9B%BE%E7%89%873.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/10/%E5%9B%BE%E7%89%873.png)

2. 在查询操作后，对于上图中高亮的数据，本文采用了一种基于 milestone 的 DecisionFlow Graph 的形式进行表示，如下图所示。图中的三个蓝色图元（顶点）就是 milestone，它们对应了用户在查询阶段定义的事件（矩形表示心绞痛往前一年的时间点，后两个圆圈分别表示心绞痛和心脏手术两个事件）。在这个图中，每个用户的数据被心绞痛的这个事件分割成两部分，即心绞痛发生之前的数据和发生之后的数据，这两部分数据被分别存储在两条边上面。

[![](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/10/%E5%9B%BE%E7%89%874.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/10/%E5%9B%BE%E7%89%874.png)

3. 以上都是传统的对时序事件数据的处理方案，即查询 + 聚合表达。本文在此基础上，还定义了一些 operator，支持 milestone 的添加、删除和过滤。下图是一个添加 milestone 的过程，本文称之为 promotion，顾名思义，是将原先不是 milestone 的事件“提升”为一个 milestone。经过 promotion 的操作，原先的一条边一般会增加到三条边，如图中(c)(d)(e)所示，边(e)代表了不包含新 milestone 的用户数据，(c)(d)则是包含新 milestone 的用户数据被分割成的两部分。milestone 的删除操作和添加操作相反，一般三条边会降到一条边。milestone 过滤操作更好理解，比如只选择经过（或不经过）某一 milestone 的数据。这样一来，本文方法可以让用户对数据从粗略到精细进行自由探索。本文也是通过种方式来支持“高维”数据的可视化与交互，同时又保证“高维”数据可视化的结果不至于太混乱。

[![](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/10/%E5%9B%BE%E7%89%875.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/10/%E5%9B%BE%E7%89%875.png)

4. 下图是本文对 DecisionFlow Graph 的可视编码方案。每个 milestone 用一个灰色的条表示，d0-2 编码了各自对应边的统计信息，高度表示包含数据数目的相对大小，宽度包含了数据平均的持续时间（及每条数据在两个 milestone 之间时间的平均），颜色编码了数据中符合 Outcome 条件的比例。介于 d0-2 和 milestone 之间的矩形只用于保持 milestone 和边之间视觉上的连接关系，不用作编码任何信息。

[![](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/10/6.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/10/6.png)

5. 此外，本文还在 DecisionFlow Graph 的基础上，定义了一些交互，如下图所示。当用户选中一条边，相应的客户数据在其余边上的分布情况也会相应地进行高亮。当鼠标悬浮到边上，会显示精确的统计信息。

[![](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/10/%E5%9B%BE%E7%89%876.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/10/%E5%9B%BE%E7%89%876.png)

6. 此外，还有另外两个联动视图分别展示所选中边的统计信息和系数（odds ratio 和 correlation）

[![](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/10/7.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/10/7.png)

#### User Study

本文数据和领域密切相关，但是并未请领域专家合作做 case study，只是设计了一系列简单任务，让 12 个用户去完成，在准确率和用时上都表明了本文方法的有效性。之后对用户的问卷调查也普遍对系统的易用性表示肯定。唯一不足的是 DecisionFlow Graph 中的 link edge 会让用户产生疑惑，总误认为编码了什么信息在里面。

#### 总结

1. 提出了一个用于分析高维时序事件数据的可视分析系统，user study 表明系统易用

2. 当前方法只针对点事件，不支持分析持续一段时间的事件

3. 缺少领域专家的 evaluation

4. 没有做 case study，只是通过 user study 对系统的局部进行易用性的证明，系统用于分析真实数据的有效性说明不够充分。

5. 没有加入 mining 算法，对用户的操作（promotion/demotion）不能进行提示、引导。
