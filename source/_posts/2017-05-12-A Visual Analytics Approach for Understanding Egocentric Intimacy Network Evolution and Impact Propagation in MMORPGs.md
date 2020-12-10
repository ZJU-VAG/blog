---
title: "A Visual Analytics Approach for Understanding Egocentric Intimacy Network Evolution and Impact Propagation in MMORPGs"
tags: ["论文评述", "报告"]
date: 2017-05-12
author: 朱闽峰
mail: minfeng_zhu@zju.edu.cn
---

论文：A Visual Analytics Approach for Understanding Egocentric Intimacy Network Evolution and Impact Propagation in MMORPGs

作者： Quan Li, Qiaomu Shen, Yao Ming, Peng Xu, Yun Wang, Xiaojuan Ma and Huamin Qu

发表会议：IEEE PacificVis 2017

## **介绍**

大型多人在线角色扮演游戏吸引着众多玩家在沉浸式的虚拟游戏环境中和其他玩家进行社交互动。一款优秀的大型多人在线角色扮演游戏应当满足不同玩家不同层次上的需求。因此，研究玩家的社交互动网络和动态的亲密度变化，有助于我们了解玩家在游戏中需求导向的行为，从而提升游戏设计和营销策略。本文提出的 MMOSeer 是一个用于分析玩家自我中心亲密度网络变化和影响传播的可视分析系统。

## **目标**

一款优秀的大型多人在线角色扮演游戏需要在玩家的满意度上达到内容满意（在游戏中获取新信息）、过程满意（获取经济效益）、社交满意（稳定社交圈完成工会挑战和地下城）和快乐满意（和其他玩家的合作），因此理解游戏中社交互动和影响传播的机制社交网络对开发大型多人在线角色扮演游戏至关重要。游戏分析师希望研究游戏内的社交网络，，分析网络的有效性和稳定性。然而每个玩家的满意度可能是不同的，相比于直接分析整个网络，分析个人的 ego-network 会更加有效。

当前对于动态网络可视化的研究主要关注于整个网络的变化（宏观），没有关注 ego-network（微观）的变化。同时对于 ego-network 的研究少有研究考虑动态变化。本文分析探索大型多人在线角色扮演游戏中 ego-network 动态变化和相互影响。

## **数据**

文章中大型多人在线角色扮演游戏的数据包括两大类。一、角色互动数据，包括交流、打怪、对战等互动数据，玩家之间的亲密度就是是玩家之间互动事件的计数。二、角色状态，主要包括玩家的登录登出时间。

## **可视化设计**

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/05/Picture1.png)

图 1. 可视化界面

### **Intimacy Network Overview**

Intimacy Network Overview 是给了一个所有玩家分布的总览。每个玩家对应的 ego-network 可以用一个向量来表示。向量包括以下属性：

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/05/22.png)

玩家向量属性

基于向量之间的距离，所有玩家的 ego-network 可以用 MDS 投影到二位平面，可以用于分析玩家的分布（图 1A）。

**Interaction Timeline View**

为了展示 ego-network 的动态变化（每个时刻中心玩家的邻居变化），文章使用了一个基于 timeline 的布局。X 轴表示时间，动态网络的随时间变化依次沿着 X 轴变化。为了避免所有点集中在同一个高度造成遮挡，Y 轴上，节点按照先后顺序等距分布。同时用一个长方形把这一个时刻的所有邻居包括起来，长方形的中心等于所有相关节点的中心。如下图所示，x 点是第三个出现的，所以它的高度距离 x 轴有三个距离。长方形的中心为三个节点 x，y 和 z 的平均高度。

![Interaction Timeline View](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/05/Picture22.png)

Interaction Timeline View

为了提取 ego-network 变化的程度，文章计算了 overall change ratio (OCR)值。OCR 值主要基于变化节点数量占所有节点数量的比例计算得到。如下图所示，当网络变化比较大时，OCR 值比较高。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/05/Picture3.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/05/Picture3.png)

为了解释 OCR 值变化的原因，文章使用堆叠柱状图展示每个时刻玩家之间互动行为的比例。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/05/Picture5.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/05/Picture5.png)

### **Summary of Changes of Alters’s Network**

玩家之间互动的影响传播对于游戏中社交网络的稳定也有很重要的作用。Summary of Changes of Alters’s Network 展示了以邻居为中心的 ego-network 变化。其中，X 轴表示亲密度，圆点颜色编码了 OCR 值，圆点大小代表网络节点数量。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/05/Picture6.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/05/Picture6.png)

### **Logon/Logout Timeline**

Logon/Logout Timeline 展示了玩家上线到下线的时间片段，其中红色代表中心节点自己，其余的颜色深浅编码了和中心玩家的亲密度。由于一个玩家的上线时间可能并不长，一行绘制一个玩家会非常浪费空间。本章采用了插空的方法（从第一层开始检查，找到没有其他矩形冲突的一行），把多行内容进行了合并。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/05/Picture7.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/05/Picture7.png)

## **案例分析**

### case1.1

下图所示的是一个典型的 PVP 玩家，我们可以看到

1. OCR 值一直都比较高
2. 在聊天和对战过程中，总是结交新朋友
3. 和朋友之间的互动比较多，Logon/Logout Timeline 中深绿色比较多。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/05/Picture8.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/05/Picture8.png)

### case1.2

PVE 玩家和行为和 PVP 玩家有着很大的不同。我们可以看到，PVE 玩家

1.  大部分时间在打怪

2.  主要是通过聊天结交新朋友
3.  只和少量的朋友有稳定的关系，Logon/Logout Timeline 中深绿色比较少。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/05/Picture9.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/05/Picture9.png)

### case2.1

我们选取一个选取活跃玩家 a（A 红）和最多互动的玩家 b（A 深绿），分析玩家之间的影响传播。我们看到 C 界面中，玩家 b 和他的邻居之间的亲密度随着时间在增加。D 中， 8-11 号的玩家 b 的 ego-network 不变，12 号后 ego-network 开始显著扩张。这说明了和活跃玩家的合作可以扩大玩家之间的社会关系。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/05/Picture10.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/05/Picture10.png)

### case2.2

我们选取了两个非活跃玩家。如下图所示，在 Interaction Timeline View，这两个玩家总是有互动，大部分情况是在组队打怪。通过他们的 ego-network 我们看到，各自的 ego-network 没有明显的扩张。这说明和至交一起玩游戏，不会扩大各自的社交网络。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/05/Picture11.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/05/Picture11.png)
