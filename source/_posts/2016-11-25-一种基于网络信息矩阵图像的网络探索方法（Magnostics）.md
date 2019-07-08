---
title: "Magnostics: Image-based Search of Interesting Matrix Views for Guided Network Exploration"
tags: ["论文评述", "报告"]
date: 2016-11-25
author: 韩冬明
mathjax: true
---

论文: Magnostics: Image-based Search of Interesting Matrix Views for Guided Network Exploration

作者: Michael Behrisch, Benjamin Bach, Michael Hund, Michael Delz, Laura von Ruden, ¨ Jean-Daniel Fekete and Tobias Schreck

发表期刊: TVCG 2016

![](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/1.jpg)

## 一． 动机

![](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/2.jpg)

网络、关系等数据变成如图的邻接矩阵时（红色代表两个节点也就是人，之间有联系），但是得到的矩阵会因为顺序的问题而出现不同的排列方式，在第一种中会发现因为有聚集的块状区域而很容易地把数据分为两个部分，然后根据数据的具体含义而得知其代表的意思，在此图中可以看出是两个集团。

当分析数据时候，把它转换成矩阵的形式，并运用一些矩阵重排序算法将矩阵变形，变成特定的图案pattern。而现在希望基于图像来查询哪些变形好的矩阵属于同一种pattern。

当前的数据量特别大，数据维度特别多，样式复杂多变，对于探测特定的图像pattern，很难用肉眼去识别一个图案是不是属于一种pattern。当前基于矩阵的图像识别的图像feature特别多，没有一个明确的标准去评定哪种图像特征适合去识别哪种图像的pattern

## 二．贡献

6种用于检测特定pattern的feature

4种用来衡量feature检测结果的评分标准

补充了可视化分析中基于特征的分析的工具

## 三． 实验

![](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/3.jpg)

### 选取feature

作者选取了常用的27种用于描述图像的feature，并新定义了3种feature（下图中红色为新定义的feature）。

![](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/4.jpg)

### 构造数据

作者选取了要探测的6种pattern，并加入4种变化方式，进行组合

#### 6种pattern：

![](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/5.jpg)

#### 4种变化：

![](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/6.jpg)

1. Variations

同一种pattern的不同表现形式

2. Point Swap

随机交换其中的点，分为0, 1, 2, 4, 8, 16, 32的百分比的情况，32%的情况分辨不出其所属的pattern（此时为Noise）

3. Index Swap

随机交换两行或两列，在这里为0-10次随机交换

4. Masking

添加额外的点，(0% to 16%)

### 生成向量

对于每一个矩阵和一个feature，都可以看成是一个向量，并计算之间的欧几里得距离，同一个feature的向量之间距离越近可以认为两个pattern十分相近。

### 标准分析

根据向量的距离进行分析，通过作者定义的4种衡量标准。

#### 1. C1评分标准1

用来评估，一个feature能否把pattern从噪音(Masking)中区分出来，下图中颜色越深代表其评分越高，满分为1。为0或打叉的表示其在此种变化时并没有实际的意义，不需要进行测试。

![](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/7.jpg)

#### 2. C2评分标准2

用来评估，一个feature对于同一种pattern的不同表现形式的区分程度，如果向量间距离越大，说明可以有效的区分。

图片表示对于同一张pattern的不同表现形式（种类） 的矩阵与feature组成向量的距离差，颜色越深表示距离越近。

![](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/8.jpg)

下图中颜色越深表示其C2的评分越高，满分为0.5

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/9.jpg)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/9.jpg)

#### 3. C3评分标准3

用来评估，一个feature对于同一种pattern添加噪音(Point Swap, Index Swap)之后的区分程度，也是对于噪音的敏感程度，越不敏感说明效果越好。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/10.jpg)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/10.jpg)

上图横坐标表示噪音的添加率，纵坐标表示和原pattern向量的距离。黑色的点代表pattern不同表现形式的向量和原pattern向量的距离，红色点表示平均距离，此图表示对于噪音的添加，距离的增长并不快。所以敏感程度很低，C3评分越好

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/11.jpg)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/11.jpg)

上图可以看出距离的增长很快。所以敏感程度很高，C3评分越不好

 

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/12.jpg)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/12.jpg)

此图可以看出距离的增长不是很快。

但是和第一个图比较，虽然敏感性不如它好，但是对于pattern的表现变化区分的很快，也就是图中的黑点。所以C3评分不如第一个图，但是C2评分高于它

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/13.jpg)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/13.jpg)

此图可以看出对于噪音的增加，距离是一个逐渐增大的趋势，趋势越慢说明抗噪音程度越好。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/12.5.jpg)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/12.5.jpg)

上图为C3的评分，颜色越深表示抗噪音干扰的强度越高

#### 4. C4评分标准4

用来评估，一个feature把pattern分别出来的能力，C1表示从噪音模式中区分。把所有的向量两两作差取平均值，来判断对于不同的pattern，他们之间的距离是否距离的比较远，可以进行区分。

下图表示模式之间距离的远近，也就是区分pattern能力的大小，盒须图整体越高的代表其区分能力越大，红色的feature的区分能力很强，C4的评分越高。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/14.jpg)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/14.jpg)

## 五.实验总结
评分标准中，C1，C4为主要评分标准，C2，C3要根据具体的feature的含义特点进行加权处理与取舍。

下图表示feature的C1（蓝色），C2（红色），C3（棕色）的评分，黑色点越多，代表其评分在C1、C2或C3上，所以得feature中的排名越高。图中的框选的feature代表最后作者所选的6种feature

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/15.jpg)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/15.jpg)

## 六.应用

#### 1. 素描识别

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/16.jpg)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/16.jpg)

用户在1中画想查询的pattern，在3中选择feature，在2中可以看到识别到的pattern，可以看出准确率还是很高的。

 

#### 2. 动态图比较

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/17.jpg)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2016/11/17.jpg)

下面每个矩阵图像代表2秒内社团的一个聚合后的矩阵图像，红色代表常来探测BLOCK的feature-BlOCKS，蓝色代表HARALICK也就是对于噪音的探测，每一个点的y坐标是和上一个进行对比得到的，可以看到6-9 的BLOCK pattern的明显变化，BLOCK的样式变得不一样了。10-14可以看出噪音的变化。

