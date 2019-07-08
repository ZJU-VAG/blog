---
title: "Visualization System Requirements for Data Processing Pipeline Design and Optimization"
tags: ["论文评述", "报告"]
date: 2017-09-21
author: 李宗壮
---

## **动机**

数据数量和复杂性的上升需要一个设计和优化数据处理流程。可视化可以支持这一过程,但尽管有很多视觉系统参数分析的例子,这仍然需要系统地评估用户的需求和符合这些需求范例可视化方法。

 

对此作者对于流程也进行了简单的定义如图：

流程是一组计算指令或者说步骤

每个指令有一个特殊的算法参数

设计一个流程需要选择不同的计算步骤

在优化中，用户通常会固定一些计算步骤

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/09/22.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/09/22.png)

 

本文有四个贡献点：通过八个案例展现了这一工作挑战的广度；通过对八个案例的整合回顾总结了用户需求对总结出的用户需求；相应的匹配可视化的功能；最后定义了未来可视化研究的挑战；



相关工作分为两个大类，流程设计和优化的方法以及框架和特征。

文章给出八个案例，每个案例都是一个利益相关者为了实现某个目的而要解决一个问题。作者设计了对利益相关者的半结构化的采访，来探求其中重要的事项以及目前可视化工具在设计优化数据处理流水线里的局限性。这些案例分别的领域是：

- 比较基因组学
- 三维图像分割
- 二维图像分割
- 化学工程
- 经济建模
- 航空发动机设计
- 系统生成树
- 分子演化

对八个案例进行统合分析得到用户需求。为了验证需求，两个作者选取了28篇在设计和优化流程的可视化领域有代表性的文章

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/09/221.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/09/221.png)

 

本文把作者的需求分为了三大类：输入，计算和输出。如图所示

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/09/222.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/09/222.png)

输入，包含数据的各个方面，体积，速度，多样性，真实性

计算，包括用户在设计流程，执行计算步骤时做出的各种选择未知/已知的流程，流程假设，组合（参数）的数量，对流程的理解，出处

输出，包含基于流程的最后或者中间步骤的选择得到的需求输出的数量，输出质量的主观性，与输入，参数，程序的敏感性，不确定性，评估时间，环境

对于可视化的实例，对描述的不同方面分别例证。来自八个案例或者28篇文献三部分，对应输入，计算和输出。文章指出交互的可视化方法是对三个方面都有帮助的方法

## **输入数据的可视评估**

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/09/224.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/09/224.png)

## **计算的视觉支持**

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/09/225.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/09/225.png)

## **输出的可视化探索**

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/09/227.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/09/227.png)

 

在研究中发现的一些值得注意的事实

案例研究更多的是不确定的流程，假定，评估时间和内容，其中评估时间在终端用户场景张是很重要的指标。

设计过程的背景会影响用户在设计和优化时所做出的选择。比如时间，预算，资源等的限制，人的专业技能，预期受众等。

最后文章总结了今后可视化技术面临的挑战：

- 改变用户的工作流
- 协助参数选择
- 代表误差和不确定性
- 利用衍生措施的力量
- 对大量不动产的利用
- 改善用户交互
- 大数据的扩展

 