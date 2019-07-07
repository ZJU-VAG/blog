---

title: "Mapping Color to Meaning in Colormap Data Visualizations"
"
tags: ["论文评述", "报告"]

date: 2019-04-19

author: 陈则衔

mathjax: true

---

论文：Mapping Color to Meaning in Colormap Data Visualizations

作者：Karen B. Schloss, Connor C. Gramazio, A. Taylor Silverman, Madeline L. Parker, Audrey S. Wang

发表：IEEE InfoVis 2018

## 摘要

在进行颜色编码的时候，颜色会拥有不同的维度，例如亮度、色调等等。当colormap的映射关系与观测的人推断一致的时候，这可以说是一个好的颜色映射。

## 文章主要研究

- 是哪些因素会造成人们不同的推断映射。

- 过去的文献在这方面是相互矛盾的（背景颜色影响人们先验推断上面)，对其进行了解释说明

## 结论

- 背景颜色是否影响与colormap是否有透明度的变化相关。

- 没有透明度变化==>颜色越深，值越大(dark-is-more bias)

- 有透明度变化==>越不透明，值越大(opaque-is-more-bias)

- 在不同的背景下(浅色、深色)，会造成冲突.

- (opaque-is-more bias)有时候没啥用，有时候要超过(dark-is-more bias)所以最好不要用透明度变化的编码，这样可以自适应任何的背景颜色。

## 介绍

介绍了colormap的要求：perceptual和cognitive。知觉上能感觉出不同的颜色对应着不同的值.感官上能判断出整体两个图的稀疏之分。同样，当colormap的映射关系与观测的人推断一致的时候，这可以说是一个好的颜色映射。研究背景颜色和colormap颜色不同造成的影响，以前的文献，讲的不清楚。可以归类有3种偏差：dark-is-more bias、contrast-is-more bias、opaque-is-more bias。在实验一中测验了这三种不同的偏差，并且计算他们报告的事件。

### 结论

1.背景颜色只有在colormap在透明度上有变化时才有作用。

2.当透明度不变化时，dark-is-more bias更有明显的作用。这和contrast-is-more bias相左。

3.透明度变化时，其影响作用随着透明度的变化幅度增大而增大.opaque-is-more bias和contrast-is-more bias只有细微的差别.因为当透明度变化时，对比度才有意义。

## 相关工作

(1).designing color scales for colormaps
(2).selecting color scales according to data and task 
(3).encoding semantics in colormap visualizations

主要是第三部分:

### designing color scales for colormaps

- Discriminative power

- Uniformity

- Order

### selecting color scales according to data and task

- Different color scales are more or less effective, depending on the properties of data they represent and the tasks needed to interpret the data.

- 不同的任务\数据应当使用不同的颜色映射.

- 单一亮度变化或者用多颜色映射变化.

### encoding semantics in colormap visualizations

## 实验一

### Aim at

How the background color influenced inferred mappings when colormaps were constructed using various standard color scales for visualization.通过RTs时间的不同来得到结论。

### Design
参与人：30个人(avg ags = 22)

数据:比较早上还是晚上目睹的外星生物比较多

数据由argtanc + 高斯噪声生成,一半早上多，一半晚上多。
- 20 colormap conditions(5 color scales * 2 background color * 2(left/right balance))
- 20 diffierent colormaps per conditon
- 20 * 20 = 400 unique colormap imgs
repeat 4 times for four different legend conditions(light/dark-more, greater/fewer-high),different legend只是为了保证他们看了图例。每次要尽快回答左边多还是右边多,错了会有声音提醒，对自己正确率有个把握。开始之前，会有先验测试(20个)：500ms blank gray screen,后面一直等你选。真实测试的时候,80组不同的情况是打乱随机出现的。
结果如下：
![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/04/resulte01.png)

### Conclusion
- 准确率都很高，(mean 97%, 91%-99%)总体来讲，dark-more会更快，但是对于不同的colormap，背景的影响是不一样的。–>可能原因是因为，colormap中含有opaque-is-more bias，和dark-is-more bias共同影响的结局。所以还要看每个colormap的透明度变化。

- 提出了一个叫做Opacity Variation Index的指标，z是均方根误差(RMS,无偏估计量拉力说就是标准差)

- 值越小，代表透明度变化越明显–>和线的变化越接近–感知上透明度变化越明显

- Figure 6.如果只有dark-is-more bias,那么每条线的斜率应该是0，即不受透明度影响,该快多少块多少。但显然，Opacity Variation Index的变化，Faster RTs有变化，说明了这是dark-is-more 和opaque-is-more共同作用的结果

## 实验二

### Aim at
tested our hypothesis that there is an opaque-ismore bias.准备了三种颜色：black、white、blue.分别做线性差值，可以得到如下几组：white-black,white-blue;blue-black;背景颜色分别为：white、blue(rgb:[56,126,185])、black；那么总会有2种背景颜色是有透明度变化的，一种是没有的。

### Method
- participants: 36 – 6(为了让实验人数和实验一相同，并且准确率要>90%)

- conditions: 3 color scales * 3 backgroud colors * 2 encoded lightness mappings * 2 lengend text positions * 2 (left/right balance) = 72

- all: 72 *20 = 1440 trails

- pre-trails: 20

### Results

- RTs:(mean accuracy:97% range: 92%-99%, -6之后 < 90%)

- 在light-background 上，dark-is-more 更快， 在 dark background上，一样快或者light-more encoded更快，在没有透明度影响上，dark-is-more更快

- 出现的反例：认为是其他实验的黑色遗留效应.其他的实验中，色标会有透明度变化，颜色浅的看起来更不透明.这导致opacity-more和dark-more竞争时，降低了dark-more的影响力.他们怀疑这种情况影响到了black background with blue-white color scale.需要进一步调查.
![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2019/04/result21.png)

## General Discussion

- Cuff：表明有dark-is-more bias的存在，但是没有考虑背景颜色

- McGranaghan:表明有contrast-is-more bias，但是切换不同的背景颜色时,dark-is-more bias总是存在，只是在black background上减少了.

- Roth et al.提出dark background上用lighter colors来编码大数据(没有实验测试).这和McGranaghan冲突了.

 

- 作者的结论认为：存在opacity-is-more bias和dark-is-more bias。当背景颜色和color scale没有透明度影响时，只存在dark-is-more bias.有透明度影响时，看透明度变化大小，决定了那个bias影响更大.

- 实验一说明了McGranaghan为什么dark-is-more bias在black background上还是有dark-is-more bias。因为透明度变化不够大，并且参与者想给出一致的答案(潜意识)

 

- 实验二说明了当背景颜色有较大的透明度变化时，opaciity-is-more影响更大.

### Open questions
如何从理论角度上去解释drak-is-more和opaque-is-more的存在.找了很多颜色方面的理论框架。也可以去测试这种情况是从自然界中经验的积累还是看过可视化例子之后形成的。也可以去找那些只用lighter编码的领域专家。

 

### Opacity Variation Index
没啥理论依据，但可能好用。如何最好地量化不透明度的明显变化时一个开放式问题(尚未解决)。

### LAB颜色空间
三个基本坐标表示颜色的亮度（L*, L* = 0生成黑色而L* = 100指示白色），它在红色／品红色和绿色之间的位置（a*负值指示绿色而正值指示品红）和它在黄色和蓝色之间的位置（b*负值指示蓝色而正值指示黄色）。



 

