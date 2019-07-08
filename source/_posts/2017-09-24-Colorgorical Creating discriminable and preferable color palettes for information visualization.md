---
title: "Colorgorical: Creating discriminable and preferable color palettes for information visualization"
tags: ["论文评述", "报告"]
date: 2017-09-24
author: 梅鸿辉
---

论文：Colorgorical: Creating discriminable and preferable color palettes for information visualization

作者：Connor C. Gramazio, David H. Laidlaw, Karen B. Schloss

简介：本文介绍了一个调色板工具Colorgorical。其中涉及到多种与人类感知相关的颜色度量，以及感知相关的用户交互设计。此外还有出色的现成颜色设计。



**相比纯艺术的设计考量，在可视化中使用颜色需要额外考虑到区分度。但从颜色理论来说，区分度和审美表现相矛盾，如何平衡两者之间的关系是本文主要想要解决的问题，从以下两个方面着手**

- 设计了从不同方面对颜色进行评价的4种颜色分数
- 设计了可以通过交互调整参数的可变颜色生成模型

颜色分数有四种：

- Perceptual Distance
- Name Difference
- Name Uniqueness
- Pair Preference

Perceptual Distance:

颜色分分数在CIELAB空间下进行，L*为亮度，a*和b*分别为由绿到黄和由蓝到红的分布，取值范围-128~+128中属于sRGB的部分，可以用在典型的屏幕显示中（6位十六进制颜色码）

其中，a*b*可以被转换为类似极坐标的chroma (C, radius) 和 hue (H, angle)

计算方法如下，DE76简单的计算了在L*a*b*空间中的欧氏距离，改进的DE00算法额外考虑了色调旋转(RT)和不同区域的修正(S)
$$
\begin{array}{c}{\mathrm{DE}_{76}=\sqrt{\Delta L^{2}+\Delta a^{2}+\Delta b^{2}}} \\ {\mathrm{DE}_{00}=\sqrt{\left(\frac{\Delta L}{S_{L}}\right)^{2}+\left(\frac{\Delta C}{S_{C}}\right)^{2}+\left(\frac{\Delta H}{S_{H}}\right)^{2}+R_{T} \frac{\Delta C}{S_{C}} \frac{\Delta H}{S_{H}}}}\end{array}
$$
**Name Difference / Name Uniqueness**

颜色名称基于XKCD color-name的153个名字和其互相之间的关联度

Name Difference统计关联度之间的分布差异

[![Name Difference](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/09/%E5%9B%BE%E7%89%872.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/09/%E5%9B%BE%E7%89%872.png)

Name Uniqueness统计某一种颜色与其他所有颜色关联度分布的奇异性

[![Name Uniqueness](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/09/%E5%9B%BE%E7%89%873.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/09/%E5%9B%BE%E7%89%873.png)

**Pair Preference**

Pair preference是一个基于经验参数的审美评估函数。当然，与实际人眼感知的漂亮与否有一定差别。
$$
\operatorname{PP}\left(c_{1}, c_{2}\right)=75.15 \sum \kappa+47.61|\Delta L|-46.42|\Delta H|
$$
本文采用的颜色生成模型迭代的一个一个生成颜色，其中颜色的总数可以用户调节；过程中使用到了这四个分数的加权平均，用户可以通过滑动滑块调节权重。因此，此模型可以提供用户干预的颜色生成。

具体步骤如下：

- 初始化模型
  - 等距(15单位)采样CIELAB空间中的8325个离散颜色点
  - 去除L>85和L<25
  - 去除不好看的颜色（深黄绿色部分）
  - 基于用户定义过滤颜色
  - 去除pair preference较低的
- 开始
  - 从剩余颜色中随机采样一个种子颜色
  - 或者用户指定
  - 移除与其区分度过低的颜色
- 添加颜色
  - 加权计算所有剩余颜色与已有颜色间的分数
  - 从分数大于阈值的颜色中随机选取

随后，文章从模型设定的主观评估和与其他工业标准的比较两方面进行了实验和评估

**模型设定的主观评估**

作者进行了4个假设

- P1 颜色更少的调色板区分度更大
- P2 颜色区分测试的反应时间(response time)和错误(error)与Perceptual Distance负相关，与Pair Preference正相关；喜好(preference rating)测试则相反
- P3 颜色数与区分度和喜好都相关
- P4 调节滑块可以显著影响对应的区分度/喜好

作者选取了多种配置进行颜色生成，然后对结果从反应时间(response time)、错误(error)和喜好(preference rating)三个方面进行了实验。

从结果来看，4个假设基本成立。下图是不同分数与上述三个测试的相关程度

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/09/%E5%9B%BE%E7%89%875.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/09/%E5%9B%BE%E7%89%875.png)

下图是不同参数对结果的影响程度（Name  Uniqueness影响不大没有显示）

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/09/%E5%9B%BE%E7%89%876.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/09/%E5%9B%BE%E7%89%876.png)

**与其他工业标准的比较**

作者挑出了在上面试验中得到的结果中比较好的两组，包括低错误(error)和高喜好(preference rating)连个，与现有一些调色板进行了比较。选取的调色板如下：

[![palettes](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/09/%E5%9B%BE%E7%89%877.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/09/%E5%9B%BE%E7%89%877.png)

同样是上面的三个实验，其中反应时间(RT)和错误率(error)类似于是没有显示

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/09/%E5%9B%BE%E7%89%878.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/09/%E5%9B%BE%E7%89%878.png)