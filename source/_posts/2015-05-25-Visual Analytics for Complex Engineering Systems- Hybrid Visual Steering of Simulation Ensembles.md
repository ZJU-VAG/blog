---
title: "Visual Analytics for Complex Engineering Systems: Hybrid Visual Steering of Simulation Ensembles"
tags: ["论文评述", "报告"]
date: 2015-05-25
author: 陆俊华
mail: akiori@zju.edu.cn
mathjax: true
---

## 简介

本文提出的是一种复杂工程系统可视分析的新方法—-仿真集的混合可视操控(Hybrid Visual Steering of Simulation Ensembles). 它在传统的仿真相关的可视化方法基础上增加了一个自动优化的组件(方法). 在这样一个提出问题解决问题过程中, 作者(们)先是提出一个对复杂系统的混合可视操控(Hybrid Visual Steering) 的任务的抽象, 然后他们以汽车发动机中的共轨燃油喷射系统进行一个案例分析, 广泛联合了领域专家, 与专家们进行深入讨论, 并设计完善了这个方法和一个针对该领域的系统原型.

## 方法概览

下面是方法的一个概览: 蓝色是最原始的复杂系统可视化的一个系统流程, 然后一步步上升的过程

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/pic1.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/pic1.png)

由于当今科学技术的发展, 仿真已经不是一个一个跑一个个看的了, 常常是对于同一个模型同时可以跑多组不同的参数, 这样跑出来不同的结果更高效找出最优点. 当然有时候也有缺点就是可能会在无目的的情况下多跑了许多点, 使得人无法清楚的分辨或者找出想要的结果. 在这种情况下作者提出了这种混合可视操控的方法, 最显著的一个特征是在一般系统的基础上添加了自动优化的功能. 这个功能背后是一个计算回归方程的模块, 可以用回归模型模拟仿真的函数, 提高效率. 此外还提供在回归基础上进一步优化回归模型等等的功能. 下图是基于共轨燃油喷射系统设计的实例及其说明. 文中声称结合了大量公司专家的评论和指点.

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/2.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/05/2.png)

这种方法具有一定的普适性, 可以适用于: 可用多维参数空间仿真模型表示的复杂系统. 作者们正探索扩展到医学图像分割, 空气流动模拟和交通模拟等领域. 但尽管方法论、工作流程具有一定的普适性, 但是系统的各个组件仍需根据针对的领域进行特殊化和改进.
