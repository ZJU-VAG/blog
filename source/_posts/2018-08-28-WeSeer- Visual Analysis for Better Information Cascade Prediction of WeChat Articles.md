---
title: "WeSeer: Visual Analysis for Better Information Cascade Prediction of WeChat Articles"
tags: ["论文评述", "报告"]
date: 2019-10-18
author: 卢金璇
mail: 11821132@zju.edu.cn
mathjax: true
---

论文：Weseer : Visual Analysis for Better Information Cascade Prediction of WeChat Articles

作者：Quan Li, Ziming Wu, Lingling Yi, Kristanto Sean N, Huamin Qu, Member, IEEE and Xiaojuan Ma

发表：IEEE transactions on visualization and computer graphics. TVCG,2018

WeSeer 是一个交互式推理系统，可帮助领域专家基于 SEISMIC 流程理解和改进预测模型，以获得更好的预测结果。 还提供了微信发布预测背后的预测原因。

## 动机

微信是一种新型的社交网络服务，每月有用户活跃大约 10.4 亿。除了传递信息、宣传文章，阅读和分享已成为微信用户的重要活动。目前，预测微信文章的流行度收到极大的关注。因为微信信息比较丰富，每天有 1.5 亿新文章，但只有 0.007%文章被人分享大于 10000 次。预测文章的流行能帮助微信提高推荐应用软件，甚至能预防异常文章，控制他们的遥远传播，还可以预测文章未来的趋势并开展有效的广告活动。

#### 挑战

-   大量的文章共享记录是多维的，因此难以组织和可视化它们

-   展开内部机制需要不同程度的努力，因为它可能涉及提取不同的参数集

-   目前很少有研究的经验可以用于大幅提升通过获得的视觉见解来重塑预测准确性，并进一步增强解读不同预测结果背后原因

#### 贡献

-   研究并增强了 point process based，以改善预测结果。

-   设计了一个可视推理系统，以支持专家对 point process-based model 的理解

-   通过案例研究验证提出的方法的有效性，以支持所生成结果的可解释性

## 相关工作

### 已有研究相关工作分成 3 类

**预测信息流行：**研究人员通过一些著名的微博平台来分析信息传播特征。有一些研究通过网络结构和时间变 化的特征并利用不同的学习算法来解决级联预测的问题。

**视觉信息传播分析**：视觉分析可以提供对信息传播的理解
fluxflow 研究异常信息在社交媒体中的传播。他们利用机器学习算法来检测异常，并提供新颖的视觉设计来描 绘检测到的线程以进行深入分析。

![](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/11/16/a4dd435dfeade4065422838e96e7e59b2b930efb.jpeg)

​ OpinionFlow，以使分析人员能够发现意见传播模型

![](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/11/16/944e0a9332bacce25c4c78d2e5432a4d7e5dd62a.png)

**视觉预测社交媒体分析**：尽管研究人员通过提出不同的模型或采用有效的功能为预测分析做出贡献，但与可 靠的模型仍然存在差距。 通过了解现有行为，可视化分析系统可帮助您基于基础训练模型预测未来的信息趋势，使用可视化技术获得见解或可视化验证预测结果。一些研究人员对常用算法进行了调查，并讨论了使用户参与正在进行的计算的可能性。

![](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/11/16/33f364315e36d6fe53ad4b7ae8663466af324e1a.jpeg)

## 方法

### 微信的传播文章

微信的传播文章过程分成 3 种方法：从官方分享文章，从朋友圈分享文章，或者直接传递给朋友。

![](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/11/16/d5ab117fd53f51543149e4a52ea30f3494d9b49f.jpeg)

### **_SEISMIC ：_**

本文提出了 point process-based 模型，SEISMIC(Self-Exciting Model of Information Cascades)预测文章的最终传播数量。这个模型只需要考虑分享历史记录和度量（朋友数量）SEISMIC 有两个重要的组成部分。

1. 传染性（及时共享文章的可能性，分享的概率）

2. 人类反应时间（发布给用户的文章与用户共享该文章的时间之间的延迟）。
    $$
    \lambda_{t}=p_{t} \cdot \sum_{t_{i} \leq t} n_{i} \phi\left(t-t_{i}\right)
    $$
    网络平均度是

$$
n_{*}=\left(1 / R_{\infty}\right) \sum_{i=0}^{R_{\infty}} n_{i}
$$

节点度是独立的并且平均程度平均分布。

### 评估

本文采用两种评估指标来衡量预测模型的准确性。 （1）绝对百分比误差（APE）（2）突破文章覆盖率（收集最终排名前 100 名的文章的真实清单和根据他们的方法生成预测的前 100 名列表。 然后，通过量化他们之间的重叠程度来评估这些方法）。

### WeSeer

在微信场景中，文章的传染性会有不同，所以本文改进了 SEISMIC 使用传播速度来调整时间戳记的原始传染性。从专家经验把网络平均度定成 140。但是 SEISMIC 假设节点是独立，文章随着时间传播，实际上会有许多用户暴露多次，用户对不同类型的文章可能也有完全不同的口味。因此为了准确地预测就把固定的平均度改成范围。

![](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/11/16/c7809affa39cf6dd09def7de4ba2387f70aa4d29.jpeg)

#### **对比方法 ：**

使用 APE 来对比每短时间的 SEISMIC 和 WeSeer，还显示了它们的最终传播值的预测以及真实的最终值（“ GroundTruth”）。

![](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/11/16/18d6e355876ad251ababcee51bc369ef393367ad.png)

### 专家需求

专家对可视推理系统的需求有三条件:

-   识别文章传染性和平均网络度对最终预测结果的影响

-   可视化传播统计信息和个人活动

-   交互式过滤有趣的时刻

## 系统界面

四种视图可帮专家了解模型机制和传播预测的原因结果。

![](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/11/16/25e23e189f1c77e961bb704a179eda63dbb97b3f.jpeg)

(a)信息视图显示所研究的微信文章及其发布者的基本信息。

(b)预测视图显示了一日传播时间为了了解和比较文章的传染性和平均度的影响。

(c)探索视图通过 what-if analysis 假设分析来阐明单个用户对模型性能的贡献

(d)传播试图显示相关传播和所涉及的用户信息。

### 案例分析

展示的文章可以分为三类。

-   celebrity (introduction of some celebrities)

-   event (some emergency events)

-   chicken-soup” articles (e.g., festival greetings and inspirational articles)

**_案例： Highly Flexible Toward Articles_**

![](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/11/16/b0366fbd977275b65f326a7ef269b2816ce6da9e.jpeg)

在案例使用了鸡汤文章来评估。SEISMIC 直到一天时间的最后一刻才能给出预测的结果。传播范围覆盖了中国大陆的大部分地区，并吸引了不同年龄的人们，但他们的平均朋友数量相对较低（0-1,000）。

WeSeer 可以迅速找到准确的估计值，并且在一天的时间范围内跨时间范围的大部分调整后平均程度仅为 45。对专家来说这篇文章虽然最终传播数量超过一万人分享，但是他只在某些用户社区中传播，而不是传播到更大的群体。所以专家认为这篇文章是缺乏多元化，是一篇质量低的文章。

**Quantitative Evaluation：**

![](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/11/16/9cec37b6e8bff45986a928a1a16d6437bf47b892.png)

本文把 SEISMIC 和 WeSeer 文章的前 100 个最常共享的微信文章。 每行代表一篇文章，每列代表一个时间间隔。 白色表示时间 t 的前 100 名文章的预测列表无法覆盖给定的文章，绿色表示成功覆盖。从图来看，WeSeer 的成功覆盖率比 SEISMIC 高，说明他们的算法比原来更准确。

## 总结

**优点：** 可以帮助专家理解机制模型，把算法提高准确性

**不足：** 没利用文章内容进行分析，没有考虑不同朋友的分享概率。大部分用户都在亚洲地区，他们传播文章的时间也有可能只是早上或者晚上当地时间。无法预测“慢发作”文章,如果文章的延迟爆发发生在预设的一日传播窗口之后很长时间，WeSeer 可能无法获取任何信号。
