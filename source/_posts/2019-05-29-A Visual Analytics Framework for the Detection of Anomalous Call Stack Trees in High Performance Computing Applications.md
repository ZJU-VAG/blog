---
title: "A Visual Analytics Framework for the Detection of Anomalous Call Stack Trees in High Performance Computing Applications"
tags: ["论文评述", "报告"]
date: 2019-05-29
author: 韩东明
mail: dongminghan@zju.edu.cn
mathjax: true
---

论文：A Visual Analytics Framework for the Detection of Anomalous Call Stack Trees in High Performance Computing Applications

作者：Cong Xie, Wei Xu, Klaus Mueller

发表：IEEE InfoVis 2018

一句话：一种用来检测分析异常代码调用栈的可视分析方法，基于 embedding 和 OCSVM 来交互式理解分析异常调用栈。

## 问题

耗时异常，父子节点相互调用，兄弟节点直接的通信中会有耗时异常

-   不同孩子对同一父亲
-   有沟通关系的兄弟节点
-   同一孩子被不同的父亲

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/%E5%9B%BE%E7%89%8719.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/图片19.png)

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/%E5%9B%BE%E7%89%8724.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/图片24.png)

这是 chrome 页面代码的调用栈，展示了调用顺序，时间，父子节点。

## 解决方案

为了解决异常代码检测的问题，这篇文章的解决方案是“找出异常的树结构”。全篇也是围绕着，如何建立树结构，如何表示树结构的信息，如何发现其中异常。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/%E5%9B%BE%E7%89%8734.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/图片34.png)

## 贡献

1.  把异常行为的检测范化为异常树结构的检测（Formulate）
2.  Stack2vec，优化了 Graph kernel approach，然后用神经网络学习树表达（Approach）
3.  可视异常检测方法支持用户查找，验证，标记（Visualization）

## 目标

1. 异常分布的概览 Overview
2. 异常调用树的排序 Rank
3. 调用树的详情 Detail-1
4. 调用树的时序模式 Detail-2

## 方法

1. 生成调用树
2. 学习树表达
3. 检测异常树
4. 可视化

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/%E5%9B%BE%E7%89%8743.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/图片43.png)

### 生成调用树

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/%E5%9B%BE%E7%89%8734.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/图片34.png)

这里就是把代码抽取成树结构

### 学习树表达

1. 抽取树结构（Weisfeiler-Lehman Algorithm ）
2. 类比树袋表达（Bag-of-Words）
3. 生成树表达（Skip-Gram Model）

#### 抽取树结构&类比树表达

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/%E5%9B%BE%E7%89%8754.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/图片54.png)

用 WL 算法，给每个点赋予 label，每种 label 都表示了一种子树结构。那么一棵树的结构就可以被多种子树结构所代表。

#### 生成树表达

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/%E5%9B%BE%E7%89%8763.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/图片63.png)

类比于 Doc2vec，读入的树结构表达当做一个文档，用来预测子树结构，也就是单词。中间的权重就是每个树的 embedding

### 检测异常树

-   不能用密度分布
-   异常较少
-   没有足够异常标记
-   采用 OCSVM(One-Class Support Vector Machine)
-   一种无监督的异常检测算法，利用标记信息来改进模型生成

## 可视化

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/%E5%9B%BE%E7%89%8772.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/图片72.png)

(a) 投影视图，可以用 PCA，MDS，或者异常检测，每个点代表一个树，这样就可以看到异常的地方

(b) 异常推荐视图，用来推荐异常的树结构，每个图代表一个树（只展示了一部分）

(c) 树细节视图，用来看树结构的组成细节

(d) 树时间和通信细节视图，用来看树结构在时间和通信维度上的细节信息

(e) 超参数面板，用来调节 WL 参数，机器学习模型参数，投影方法等

## 评估

-   3 个 Case Study
-   Quantitative Analysis: Performance, Complexity
-   User Feedback: Learning Cost, Usability

### Case Study

#### 通信延迟

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/%E5%9B%BE%E7%89%8792.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/图片92.png)

从异常检测的投影视图中发现，异常树结构。发现耗时很多（圆的半径编码了耗时）

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/Snipaste_2019-05-29_13-35-47.jpg)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/Snipaste_2019-05-29_13-35-47.jpg)

看细节图，发现是某几个函数引起的

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/%E5%9B%BE%E7%89%87142.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/图片142.png)

而正常的图应该是，孩子函数用时都比较少

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/%E5%9B%BE%E7%89%87103.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/图片103.png)

进一步看时间和通信，在这个程序下正常的应该频繁通信，但是突然有一段通信要等很久。

#### 聚类异常

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/%E5%9B%BE%E7%89%87151.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/图片151.png)

投影视图中看到一些离群的点组成的聚类，发现这些点都用同样的问题。集体异常的情况。

### Performance

专家标注了所有的异常点，然后通过不同的算法组合测试准确率

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/%E5%9B%BE%E7%89%87123.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/05/图片123.png)

## 总结

本文研究的问题很简单，也很重要，一句话就可以说的明白。用 WL+Doc2vec 的方法表示树结构，并根据树结构的特性，对 WL 优化了一下。用生成的向量去做异常检测，加入可视化的交互来反馈。同时设计了可视分析系统，以及对应的可视化设计。评估做的也特别全面。
