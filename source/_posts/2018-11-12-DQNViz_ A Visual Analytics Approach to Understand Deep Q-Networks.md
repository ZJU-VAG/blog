---
title: " DQNViz: A Visual Analytics Approach to Understand Deep Q-Networks"
tags: ["论文评述", "报告"]
date: 2018-11-12
author: 张天野
mail: zhangtianye1026@zju.edu.cn
mathjax: true
---

论文：DQNViz: A Visual Analytics Approach to Understand Deep Q-Networks

作者：Junpeng Wang, Liang Gou, Han-Wei Shen, and Hao Yang

发表：VAST 2018 (honorable mention)

## 简介

Deep Q-Network (DQN)是 Google DeepMind 研发的用于解决强化学习问题的深度卷积神经网络，用于训练一个能自动玩 Atari 2600 游戏的代理。其目的让代理跟环境（游戏）进行交互，代理需要进行游戏内的操作，完成操作后，根据某种奖励机制，不同游戏状态会获得不同的奖励，DQN 的最终目标是使整个训练过程的全部奖励之和达到最大。下图为不断循环的训练过程：[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/11/%E5%9B%BE%E7%89%871.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/11/图片1.png)

训练结束后将得到一个事件序列，包括状态(r)、操作(a)、奖励(r)：

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/11/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20181112151723.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/11/微信截图_20181112151723.png)

DQN 的最终目标则是使得整体奖励最大化：[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/11/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20181112151809.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/11/微信截图_20181112151809.png)

然而，跟监督、非监督的机器学习使用固定的数据集训练不同，强化学习的训练数据是被训练的代理的经验，是在训练过程中逐渐生成的，需要对其进行动态总结来理解数据。同时，我们又如何解释代理进行某些操作的行为？如何调整训练过程中的随机操作的比例？目前仍然缺乏一个面向强化学习模型的可视分析工具。

### 本文的贡献在于：

-   系统-分四个层次表现 DQN 模型的细节

-   可视设计-从 DQN 模型生成的事件序列数据

-   知识-优化控制训练过程中的随机输入

## 设计需求

-   R1.提供模型在训练过程中的各种统计值

-   R2.揭示代理获得的经验中的行为模式 (behavior patterns)

-   R3.允许分段分析与对比

## 数据获取

### 数据对象：训练打砖块游戏的 DQN 数据

-   五条命：未接到球时失去一条命

-   四种操作：不操作(0)、弹球(1)、左(2)、右(3)

-   四种奖励：0, 1, 4, 7

### 训练 DQN 参数：共训练 200 轮，每轮训练 25W 步，测试 2.5W 步

### 收集数据（仅测试阶段的每步数据，包括以下内容）：

a.操作 b.奖励 c.游戏屏幕（值域为[0,255]的 84\*84 矩阵） d.生命 e.是否终止 f.是否随机 g.当前步的预测 Q 值 h.当前步的目标 Q 值

### 数据的层次关系

-   步 (Step)：包含八种数据的训练步

-   段 (Segment)：某个长度的一串连续的 Step

-   集 (Episode)：游戏开始到结束的所有 Step

-   轮 (Epoch)：一轮的所有训练步，共 25,000 步

## 可视分析系统

DQNvis 的系统是一个自顶向下探索的系统，如图：

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/11/%E5%9B%BE%E7%89%872.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/11/图片2.png)

系统共分为四个视图。

-   Statistics View（左上）：用于展示训练过程中的统计值变化（上半部分）与不同的操作、奖励在各轮中占得比重（下半部分），每张图的横轴均表示轮数（epoch）。

-   Epoch View（右上）:在 Statistics View 中选中某一轮后，epoch view 会显示该轮所有 episode 中的操作（上）与奖励（下）分布。

-   Trajectory View（下方）: 横轴为训练步数，纵轴轴从下往上表示游戏屏幕中从左到右的顺序，因此折线可以表示代理在游戏中的运动轨迹，不同的操作用不同颜色点叠加在折线上，背景的颜色填充表示 DQN 预测 Q 值或目标 Q 值的变化，折线上的矩形长条颜色高亮表示获得的奖励。

同时，在 Trajectory View 中，将每集 (Episode) 划分为长度 100 的段 (Segment)，使用 DTW 计算一轮内 (Epoch) 所有段之间的相似性，并用层次聚类找到相似的模式。此外，也可通过用正则表达式定义模式，在数据中进行搜索。

-   Segment View（下图）：一个 segment 包含游戏屏幕的许多帧，每一帧屏幕是一个 84\*84 的矩阵，每四个连续帧为一个状态。DQN 共 5 层（三个卷积层，两个全连接层），整个网络中共 160 个 filter。提取每个 filter 中被最大化激活的状态，并计算该状态屏幕中每个像素点的显著性（也有被激活的与没被激活的像素点之分）。左侧柱状图表示每个 filter 激活的像素点数目，中间 PCA 投影使用每个 filter 的被激活状态的显著性矩阵计算，点的大小表示激活的像素数目，右侧的四个屏幕选择某种聚合方式，将一个 segment 中所有状态的像素激活情况表示。

## 案例

这里介绍一个通过使用 DQNvis 系统调整随机操作比例的案例。

实验一：专家认为训练完 200 轮以后的代理应该比随机操作强，因此不需要随机操作。得到的测试结果分为三阶段。一阶段正常，但是二阶段中代理未学习到要发球的知识，因此一直拿球未发，导致游戏在三阶段因为长时间而崩溃，如图。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/11/%E5%9B%BE%E7%89%873.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/11/图片3.png)

实验二：通过实验一，专家认识到训练过程中是需要随机操作的，尤其是在代理反复重复相同操作模式但无奖励时。因此缓存了 20 步的训练数据，并在缓存中使用正则表达式搜索重复 3 次及以上的操作模式，在搜索到的这种结果后增加随机操作。得到的训练结果如图，也是分为三阶段，一阶段正常，二阶段仍重复一个相同的模式，但是模式长度较长，完成一次需 50 步，因为在二阶段不断重复一个模式过长，游戏最终也在三阶段崩溃了。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/11/%E5%9B%BE%E7%89%874.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2018/11/图片4.png)

实验三：根据实验 1 与 2，专家对算法进行优化，将缓存长度变为 100，搜索的模式为重复 2 次及的模式，得到的最后结果中，随机操作实际占 2%，小于预定的 5%。

## 专家访谈

在访谈中，所有专家都认为系统非常好用，但也提出了一些建议：

-   游戏屏幕上板的位置是横向的，而视图是纵向，不易于理解

-   需要展示神经网络结构与过滤器的位置
-   方法简单，不适用于操作空间大的游戏（AlphaGo）
