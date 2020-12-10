---
title: "Visual Genealogy of Deep Neural Networks"
tags: ["论文评述", "报告"]
date: 2020-09-03
author: 潘如晟
mathjax: true
---
### 作者介绍

![作者介绍](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/9/3/5616316076265589fcc234a3cedbe98a3613c319.png)

### 背景/挑战

#### DNN的发展趋势
  - 数量猛增
  - 结构复杂
  - 种类繁多

基于以上事实，本文认为对于科研人员和学习者而言，需要有一个高效的DNN探索工具来帮助他们快速的梳理现有的DNN成果，提高学习的效率。

本文提出了如下图所示的DNN Genealogy可视化方案。包含data module 和visualzation module两大模块。

![DNN Genealogy](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/9/3/8529d9f14a9faacbeb459f8fde8a6616ef368ebe.png)

### Data Module

![论文过滤](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/9/3/f4fe54119ce61021f32b9b72433dfffe18bfa9a8.png)

通过上述自动+半手动的方法从16465篇论文中得到了140篇论文，并从中提取出66种DNN。对于每种GNN，本文从架构、性能统计、相关论文和文字简介四个方面对每个GNN进行总结。由此每种GNN作为一个节点，他们之间的关联作为边，就得到的一张有向无环图，用于后续的可视化。下图是这66种DNN所包含的9种架构：

![9种DNN架构](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/9/3/9c1414b3011bdbb0d41d7abd446469db75569534.png)


### Visualzation Module
#### Evolution visualization

![Evolution](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/9/3/a4fe94844f9854a58c11fc3ba36840686f4522bc.png)

#### DNN Viusalization

![DNN](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/9/3/8bb9047969c99bfbe65f0a11a3237c3320ba7a2f.png)

### 系统界面

![system](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/9/3/b90f54e0c80a173f6be3b3882c7d27c05b07deb5.png)

### 案例分析

#### 理解 DNNs
- 探索和学习 DNNs
- 理解DNNs的演化模式

#### Applying DNNs
- 选择合适的DNN
- 生成设计DNNs的教程

### 局限

- 忽略了训练方法
- 支持的DNN类型有待扩展
- DOI设计不够合理








