---
title: "Neurolines: 用地铁图隐喻可视化纳米级的神经连接信息"
tags: ["论文评述"]
date: 2014-11-17
author: 侯雨濛
mathjax: false
---

论文：Neurolines: A subway map metaphor for visualizing nanoscale neuronal connectivity

作者：Ali K.Al‑Awami, Johanna Beyer, Hendrik Strobelt, Narayanan Kasthuri, Jeff W. Lichtman, Hanspeter Pfister, Markus Hadwiger

发表会议：Infovis 2014

## 一、简介

#### 1. 工作起源——在神经元重建的细节分析过程中，没有有效的可视化方法来辅助分析。这个过程重视：morphology, structure, connectivity

#### 2. 前人工作主要着眼于：

1. 可视化完全抽象的连接图——弊端：舍弃了 morphology 和 structure 信息
2. 渲染原始 EM（电子显微镜）数据——弊端：会产生 visual clutter

#### 3. 本文工作：基于解刨学上的树状结构，提出了一个 multi-scale（多尺度）可视化方法，用二维的可视化方法去表达三维空间内的数据信息。

## 二、本文贡献

#### 1. 将神经突结构抽象到没有视觉重叠的二维空间，同时保留其拓扑结构和连接信息。

#### 2. multi-scale 的可视化和导航模式，可以很好地同时可视化数千个神经元。用户能够通过 zoom 交互定位到某一个 level 去观察，能保存神经元的 contextual overview

#### 3. 开发 NeuroLines Application（作为 ConnectomeExplorer 插件）

#### 4. 专家利用该系统对真实世界数据完成的 Case Studies

## 三、生物学背景——神经科学的工作流

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/11/13.png)

<center>图1：神经科学的工作流</center>
## 四、NeuroLines的设计

#### 1. 主要思想：将三维空间中神经突复杂的枝干和连接模式，抽象成简化的二维表达。二维表达的设计思路受启发于地铁图，这样的方案可以在保留枝干和突触相对位置的同时，减少视觉重叠。

#### 2. 设计考虑：尊重专家的需求和意见

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/11/22.png)

<center>图2：NeuroLines设计原型</br>
a) 圆柱形区域切分数据的三维体渲染; b) 直接呈现神经突骨骼结构的三维可视化方案; c) 表达连接信息的抽象二维可视化，忽略空间信息; d) 第一个三维地铁图原型（在三维体渲染的基础上展示连接信息）
</center>

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/11/31.png)

<center>图3：NeuroLines的最终设计：二维地铁图隐喻</center>
## 五、任务分析

#### 1. 定义主要目标：

1. Explore & Identify patterns in synaptic connections
2. Explore & Identify patterns in branching structures
3. Explore synaptic pathways

#### 2. 定义主要任务：

1. Selecting a subset
2. Single-neurite analysis
3. Multi-neurite analysis
4. Synapse analysis
5. Connectivity analysis

## 六、Scalability Challenges

#### 原因：专家需求 – hierarchical navigate through a large set of neurites

为了测试，构建了 5 种参数化的仿真器：

​ S1-多个神经元

​ S2-多个神经突

​ S3-多个枝干

​ S4-多个突触

​ S5-多个神经突间的连接

## 七、可视元素设计

#### 1. 系统概览- 3-tier focus-and-context mainview:

1.  Working set
2.  Subset
3.  Individual neurites

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/11/41.png)

<center>图4：系统概览</center>
好处:

​ a. 同时性 & 多层级，从概览到细节

​ b. 完善的探索性交互：zoom（缩放）, slide（滑动）, drilling down into the data（探索）

​ c. 引用 Working set 的概念，可以通过检索定位到感兴趣的数据集

#### 2. 视图：Navigation Bar

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/11/51.png)

<center>图5：Navigation Bar</center>
神经突的视觉编码：垂直排布的平行线；平行线的色彩编码：根据所选属性、所选标准排序的编码

#### 3. 视图：Neurite Overvire

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/11/61.png)

<center>图6：Neurite Overvire</br>一块子数据集信息的概览级可视化</center>
#### 4. 视图：Workspace View

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/11/71.png)

<center>图7：Neurite Overvire</br>某一条神经突数据的细节级可视化</center>
#### 5. 视图：On-Demand Electron Microscopy Views

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/11/81.png)

<center>图8：On-Demand Electron Microscopy Views</br>根据需求，辅助性地提供电子显微镜扫描结果图</center>
## 八、抽象计算

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/11/91.jpg)

<center>图9：抽象计算示意图</center>
#### 1. 神经突的抽象计算
1. 保留相对距离
2. 拉直树枝
3. 位移树枝到正确的角度
4. 使用相对尺度

#### 2. 树枝的抽象计算

1. 贪婪的算法 – 先画树干，然后迭代地从右往左加树枝；每次添加都改变竖直方向，避免视觉交叉。
2. 如果树枝的高度超过当前 level 的高度范围，collapse it

#### 3. 突触的抽象计算

1. 突触原本不在神经突的切分结构上，所以要根据原始的 3D 结构将突触位置投影到神经突上，用 Circle Node 去表示
2. Mean-shift cluster – 对于一组投影位置重叠的突触，每条树枝单独计算

#### 4. 突触连接的抽象计算

解决突触连接 clutter 的方法：

1. 只在需要时画
2. 用 stubs（桩）代替 lines
3. Highlight 不同结构中的相同突触

## 九、抽象计算

#### 1. 排序和筛选

filtering – 在 working set 中检所，支持动态检索

Multi-criteria sorting – 根据多个类别/数值型数据排序

#### 2. 工作区交互

Pinning – 保持标记状态

Pivoting – 基于选定 pivot 对全局其他对象进行排序和缩放，使易于找到 neighbors

#### 3. 连接性探索

支持选取、多关联发现和高亮等交互，但分析过程依然依靠人工

## 十、抽象计算

#### 1. 应用

应用方式：ConnectomeExporer 插件

语言和框架：C++ & OpenGL,

​ GUI: QT

​ Synthesizing Data: Python

所用数据：

领域真实世界数据 – 3D Volumn

合成数据 – Scalability Analysis

1. Neurons & Neuron Connectivity
2. Neurites & Braches Patterns
3. Connectivity: Synapse Generation

#### 2. 评估：

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/11/101.png)

<center>图10：系统表现和尺度性评估</center>
渲染效率：几千个神经突的渲染需要几秒，能保持交互性

Branching Scalability: 能很好的工作到 10 级子树枝，否则子树枝会被不适当地 collapse

## 十一、案例分析

#### 1. Relating Variations in Synapse Structure to Neuron Connectivity

​ “How much of the variance in the structure of synapses can be explained by the connectivity of neurons? ”

![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2014/11/111.png)

<center>图11：第一个案例分析</center>
#### 2. Relating Variance in Synapse Structure to the Branching Structure of Excitatory Dendrites

​ How the branching structure influences the attributes of synapses along the neurite.
