---
title: " EdWordle: Consistency-preserving Word Cloud Editing"
tags: ["论文评述", "报告"]
date: 2018-06-08
author: 陈则衔
mail: zexianchen@zju.edu.cn
mathjax: true
---

论文：EdWordle: Consistency-preserving Word Cloud Editing

作者：Yunhai Wang, Xiaowei Chu, Chen Bao, Lifeng Zhu, Oliver Deussen, Baoquan Chen and Michael Sedlmair

发表: IEEE infoVis 2017

## 简介

现有的 Wordle，存在不一致性的问题，即在词云的调整过程中，会将摆放不正确的单词单纯地移动到其他空白区域，这样有可能导致全局大量单词需要改变，最后导致词云结果不尽如人意。

为了保持词云的一致性，合适的编辑改变方式变得更加重要。并且每个单词的临近单词都应该被考虑，因为它们之间可能有着重要的意义。为此本篇文章提出了一个名为 EdWordle 的工具，这个工具主要用到了一个使得词云局部和全局上下文感知交互技术。

该工具是一个编辑词云的工具，在编辑词云的过程中，单词之间的邻里关系可以得到很好的保留，并且有着很好的紧凑性，可以用于编辑词云、提升现有词云并作为一个创作工具使用。

## 工作内容

整个工具的实现基于两个基础，分别为定制的刚体动力学仿真(customized rigid body dynamics)和局部词云布局算法(local Wordle layout Algorithm)。

其中，定制的刚体动力学将每个单词看做刚体，并且对此定义了两种受力，分别为相邻单词的吸引力和中心的吸引力，使得单词可以相互吸引，紧凑且靠近中心。

局部词云布局算法，是在刚体运动结束之后，优化整体布局的边界部分。

作为一个工具，其输入可以是一个已经形成的词云也可以是待生成词云，在词云上，用户可以完成增加、修改、移动等基础交互操作。

在工作完成之后，本文通过了三方面的验证来分别说明

1.具可以在不降低单词邻里关系的情况下，使得词云的紧凑性得到提高；

2.相比起现有最好的可编辑词云工具，EdWordle 更快、更紧凑、更紧凑；

3.可以将其作为一款不错的创作工具

## 定制的刚体动力学仿真

首先，可以将每个单词看成一个两级箱装结构（two-level box representation），两级结构分别为单词结构和字母结构，外层即为单词结构，大小为(W = w, H = min(h of all letter))，字母结构即将每个字母看成一个矩形刚体；两级结构仅仅用在当前单词为最大单词的一半大小的情况下，这是因为单词过小没有必要采取双层结构，紧凑性不会有太大提高但会花费较多资源运算，并不划算，采取普通的单词结构即可。

采取刚体动力学，是因为刚体不易形变，受力运动分析方便，每个刚体的运动状态可以这么定义：Y(t) = (x(t),R(t),P(t),L(t)) ，其中，Y(t)为刚体状态，x(t)为刚体中心位置，R(t)为方向向量，P(t)为角动量，L(t)为角动量。在此基础上，过去大多词云采用的方法为单层的单词结构式刚体，但是这样结果会不够紧凑，而采取单纯的字母结构虽然会更加紧凑，但是会有单词分割情况出现，具体如下图所示。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/06/EdWordle-3-1.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/06/EdWordle-3-1.png)

左图为将 dedicate 移动到 Nation 单词上方的操作，右图分别对应了不同箱装结构对应的结果。(a)为单词结构，可以发现正常移动但是并不紧凑(b)为字母结构，虽然很紧凑，但是 dedicate 会插入到 nation 之间，因为此时它也能达到受力平衡(c)采用了本篇文章提出的双层箱装结构，很紧凑且没有重叠问题

在确定好刚体结构的基础上，加入了迭代衰减的受力系统来使得整个布局在较短时间内达到较好的稳定布局。

整体受力如下图所示，合力由两部分组成，分别为邻居的吸引力和中心的吸引力，邻居吸引力跟万有引力相似，越近力越大，而吸引力于此相反，越近力越小这是为了防止中心力对边界部分缺乏影响力。于此同时，为了防止中心力过大而破坏邻里关系，在合力中为此添加一个常量系数，系数 α 默认值为 0.1。当一个系统受力达不到平衡时，整个系统会发生抖动，为此对合力添加了衰减系数避免震荡，beta 同样是一个常数。当受力平衡时，若速度不为 0，系统同样会继续震荡直至速度为 0，为了加速这个过程，同样对速度添加了衰减函数，使得整体系统快速达到一个稳定状态。 每次操作后，系统布局发生变化，变化过程中，迭代次数最多为 80 次，耗时在 0.6s 左右。

在合力中，在定义邻居吸引力之前，需要先定义邻居关系。当两者刚体的质心相连不会穿过其他刚体时，则认为两者是邻里关系，具体也如下图所示，黑色实现为邻里关系，黑色虚线为中心吸引力。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/06/EdWordle-3-21.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/06/EdWordle-3-21.png)

为了证明力的有效性，以下可以通过一个具体例子看出，具体如下图，(a)为删除*conceived*单词;(b)只用上相邻吸引力，发现不够紧凑;(c)加上中心力，发现破坏了邻里关系，比如*vain*和*resolve*，两者在(a)中是邻居而此时不是;(d)加上常量系数 α=0.1，发现效果很好[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/06/EdWordle-3-3.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/06/EdWordle-3-3.png)[
](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/06/EdWordle-3-2.png)[
](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/06/EdWordle-3-2.png)

## 局部词云布局算法

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/06/EdWrodle-4-1.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/06/EdWrodle-4-1.png)

算法如上图所示，可以分成四个部分来进行：

1.首先找到表现不好的单词

2.给它找几个候选位置(spiral scheme of Worlde )

3.挑一个不怎么破坏邻里关系中最好的

4.可能会有点破坏，但是可以更紧凑，所以对用户来说是可选操作

表现不好的单词在边界处寻找，边界定义为，在中心点为圆心画圈，其中半径 R = β\*min(w,h)，该圈为则认为是边界部分，圈外所有单词认定为布局不好的单词，其中 β=0.8，用户在操作过程中可以修改。当寻找候选位置时，如(b)所示，以当前刚体质心与布局中心连线中点作为基准点，按照螺旋式向外寻找候选位置，先到先得，候选个数 k=20，同样用户可以修改。螺旋式寻找方法详情来自于另一篇论文 J. Feinberg. Wordle-beautiful word clouds. http://www.wordle.net/.2009. 至此，完成了该工具的主要算法部分。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/06/EdWordle-4-2.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/06/EdWordle-4-2.png)

## 验证

前文所言，该篇文章总共进行了 3 个 case，详细描述一下前 2 个 case 的具体过程。

​ **case 1：定量分析**

通过与 Barth 等人提出的语义词云相比较，来说明能在保持单词邻里关系的情况下，EdWordle 的紧凑性更好。

比较指标为 Barth 等人提出的 6 个指标，分别为：实现邻接关系、失真率、紧凑性、统一面积利用率、长宽比以及运行时间，在该 case 中，主要比较实现邻接关系和紧凑性。

两者使用的布局算法为 Star Forest&&Cycle Cover，原因在于这两个算法在语义词云方面表现地较好。

数据集为 WIKI 英文文本和 SEA&&ALENEX 的 56 篇科学论文

实验结果如下

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/06/EdWordle-5-1.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/06/EdWordle-5-1.png)

​ (a)中为邻里关系比较，图中实线均为输入，在(a)图中，只有黄线稍差一点，其他几乎一样；(b)为紧凑性比较，波点为输出，发现 EdWordle 要明显优于输入

​ **case 2：与现有最优的词云编辑器 ManiWordle 做对比**

首先，基于 EdWordle 本身编辑器有好几个版本，先做一个挑选，其版本包括如下 3 个，

1.不预测用户移动后产生的结果

2.预测并告知用户移动后产生的布局结果

3.连带影响，即移动桌子，桌子上的苹果同样也会移动的移动方式

挑选了 6 个测试者，一致认为版本 2 是最好的，所以选版本 2 与 ManiWordle 作对比

​ **用户操作任务：**

1.两两放置，给予两个单词 x,y，指定拜访

2.语义错位，需要用户将相同颜色的单词放在一起

具体如下图所示，为了用户操作方便，将所有需要移动的单词都用矩形颜色框高亮显示，相同颜色即为匹配操作的一对

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/06/EdWordle-5-2.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/06/EdWordle-5-2.png)

​ **实验前的假设：**

1.在相同的操作任务下，EdWordle 效率更高

2.Task1 中，EdWordle 准确率更高

3.EdWordle 布局更紧凑

4.EdWordle 主观评分更高，因为可预测

​ **测试指标如下：**

效率: 时间 + 点击次数 + 鼠标移动距离

准确性: 统计没有按照 task 要求正确放置单词的个数

紧凑性&&主观评分:用 ManiWordle 用过的调查问卷(6 个问题);其中 评级分布由（_十分不同意_ 到*十分同意* 共 7 个评级）

​ **数据集**

Task1:“Participatory Visualization with Wordle” by Viegas et al.

Task2:全敏珠维基条目

​ **参与人员**

8 男 8 女,20-29 岁之间，平均 22 岁，大多为当地大学生，没有眼科问题，没用过相似工具，所有人都要用 2 个工具完成 2 个 task

​ **流程**

1.2min 介绍任务;

2.task1

3.task2

4.做调查问卷，在做问卷的过程中，参与人员可以再次使用工具，并且查看自己 task 后的词云布局结果

​ **实验结果**

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/06/EdWordle-5-31.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/06/EdWordle-5-31.png)

​ 左上角图为 4 个测试指标，实线为 EdWordle，可以发现每个指标 EdWordle 都表现地更好；错误方面因为 task2 只要把相同颜色放在一起所以没有错误，而 task1 也是 EdWordle 表现更好，错误更少；在调查问卷方面，EdWordle 也占据了绝对的优势

## 总结

​ 总体来说，实现了一个款可以在线编辑的词云布局工具，并且在布局过程中可以较好保证邻里关系和紧凑性，与力引导图等比较接近。

​ 该工具在线网站：http://www.edwordle.net/
