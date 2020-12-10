---
title: "Origraph: Interactive Network Wrangling"
tags: ["论文评述", "报告"]
date: 2019-09-20
author: 潘嘉铖
mail: panjiacheng@zju.edu.cn
mathjax: true
---

-   论文：Origraph: Interactive Network Wrangling
-   作者：Alex Bigelow, Carolina Nobre, Miriah Meyer, Alexander Lex
-   发表：VIS 2019 ( Conference Paper)

# 作者

1. Alex Bigelow

    - University of Utah (2014-2019 PhD)
    - University of Arizona, Postdoc
    - 兴趣：
        - Graph (network)
        - Visualization authoring
        - Data wrangling

![1569217637977](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/9/23/697673cb0c814d49a77328ede87f84243cfe506f.png)

2. Carolina Nobre

    - University of Utah (2015- PhD)
    - 兴趣：
        - Graph (network)
        - Data wrangling

![1569217666036](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/9/23/75dbec91c0107211cf78cadc53ccfd6aad5fcebb.png)

3. Miriah Meyer

-   University of Utah (associate prof)
-   宾大天文系毕业
-   犹他大学计算机博士
-   哈佛博后研究员

![1569217472666](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/9/23/d1f7772dd55110ce4ff95c60c4f480771bec0246.png)

4. Alexander Lex

-   本硕博：Graz University of Technology
-   哈佛博后研究员（2012-2015）
-   哈佛医学院访问学者（2011）

![1569217477125](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/9/23/1e862fb72b787177c083269bd491118c1e81b889.png)

# 介绍

文章的动机是关于数据整理（Data Wrangling）相关的，主要包括三个方面：

-   数据清洗
-   数据集的合并
-   数据变换

但是迄今为止，没有专门应对图数据的数据整理工具。虽然现有一部分进行图建模（graph modeling）的工具，但是他们或是聚焦于创建一个初始图模型，而不是重建该图模型，又或是一种编程语言，学习曲线太过陡峭。

于是作者提出了 Origraph，一种用于图数据建模&重建的工具。他们的贡献点一共有三个：

1. 提出了一个工具：Origraph
2. 提出了关于图数据整理相关操作的讨论
3. 两个复杂网络建模的案例学习（use case）

下面是他们的 fast forward 视频：https://www.youtube.com/watch?v=bxjDvq6kjeo

# 相关工作

### Graph Editing

图编辑的工作一般假设输入的图都是整理好的，相关的工具有如下几种：

-   Cytoscape

-   Gephi

-   Graphviz

### Wrangling Tabular Data

-   商业化软件有：

    -   Google Refine (OpenRefine)
    -   Data Wrangler (Trifacta Wrangler)
    -   Microsoft Excel

-   与图可视化相关的有：

    -   D-Dupe: An Interactive Tool for Entity Resolution in Social Networks

        利用图可视化来检测数据中的潜在重复值（potential duplicates）

        ![1569218007041](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/9/23/506dee586503fe6f05ab94c50ce68e74cdeab92d.png)

    -   Schema Mapper: Visualization of Mappings Between Schemas

        用图可视化来可视化两种不同数据模式之间的映射

        ![1569218035108](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/9/23/9c5368d5edd7137dad04130a36639c230f227476.png)

    -   GraphCuisine: Interactive Random Graph Generation with Evolutionary Algorithms

        ![1569218087740](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/9/23/d5048d3d57e318d03651cc41daecb7a2b5b43850.png)

    -   NodeXL: 一个 excel 的插件

        ![1569218095841](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/9/23/5d38f73c530154bdf333495e261d98a97898da98.png)

### 编程脚本（Scripting for Graph Wrangling）

-   编程库

    -   NetworkX
    -   Mully: An R Package to Create, Modify and Visualize Multilayered Graphs.

-   图数据库
    -   Neo4j
    -   OrientDB
    -   GraphDB

### 图建模（Network Modeling）

图建模工具的主要目的是，从表格型数据构建图数据。

-   商业系统

    -   TouchGraph Navigator
    -   Centrifuge

-   Orion: A system for modeling, transformation and visualization of multidimensional heterogeneous networks

    Jeffrey Heer 在 2014 年发表于 Information Visualization 的论文，其目的是交互性的提供一个图建模的方法，并且提供了一些图数据的可视化和交互。

    ![1569218325153](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/9/23/faebaea4e56c6dc334c9703348e2cc9953287444.png)

-   Ploceus: Modeling, visualizing, and analyzing tabular data as networks

    Zhicheng Liu, Shamkant B Navathe and John T Stasko 等人在 2014 年发表于 Information Visualization 的论文，与上面的论文类似，也是做图建模的。

    ![1569218372781](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/9/23/3c683923dfc332a0a18b3352de0bc279dca094d5.png)

-   Graphiti: Interactive Specification of Attribute-based Edges for Network Modeling and Visualization

    ArjunSrinivasan, Hyunwoo Park, Alex Endert,Rahul C. Basole 等人发表于 VAST2017 年的论文，它的侧重点在于如何构建点与点之间的边。当用户确定用某种关系作为构建边的关系时，会应用于全局。

# Graph Operation

作者通过对以往的 survey、工作、系统等总结的一系列任务，以及和领域专家的合作经验等，还进行了一些非正式的任务分析，总结了一套针对图数据整理的操作。作者把这些操作分成了三大类：

-   模型操作 (modeling operations)：引入新的类，以修改图模型、图拓扑结构
-   个体操作 (item operations)：引入/删除个体，以修改图拓扑结构

-   属性操作 (attribute operations)：管理属性/增加新属性

### **模型操作 **(modeling operations)

模型操作主要有以下几种：

1. 连接/断开 (connecting or disconnecting)

    指定两类节点之间应该通过什么关系连接；

2. 属性提升 (promoting attributes)

    把某个属性提炼，单独形成节点。下图中就把类型（genre）这个属性提炼出来作为节点。

    ![1569219069513](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/9/23/55df2158719e7150a8eafd973adb06351babe186.png)

3. 切面 (faceting)

    把某种属性当成类。下图把类型这个属性当成类。

    ![1569219094243](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/9/23/eef570df9bcac069a11cc2496d701568cfe09a31.png)

4. 点边转化 (converting between nodes and edges)

    把点转化成边，或者把边转化成点。下图把电影节点转化为了边。

    ![1569219133943](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/9/23/12dfbab7a3d521bc5660daf95e820c81471f0a6a.png)

5. 边投影 (edge projection)

    可以通过某种路径，在两类不相连的节点之间构建边。比如下图通过演员-角色-电影-出品公司的关系，把演员和出品公司连在了一起（黄色边）

    ![1569219190612](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/9/23/3303d8bb91941961e7a63b01a938cadf3268e93a.png)

6. 超节点 (creating supernodes)

    把某些点之间的共同点提炼出来作为一个新的超节点，代表这些点。

    ![1569219240359](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/9/23/f734a5f691c239d3602ccbda8b2a2d092a80b24b.png)

7. 卷边 (rolling up edges)

    多重边的聚合。

### 个体操作 (item operations)

个体操作主要有两种：

-   属性过滤 (filtering by attributes)

    根据属性值，移除特定的节点/边

-   连通性过滤 (connectivity-based filtering)

    利用网络的连通性来过滤节点/边。ex. 过滤所有没有出演过任何电影的演员，身价却超过 100 万的。

### 属性操作 (attribute operations)

-   类内属性推导 (deriving in-class attributes)

    ex. 出生日期，死亡日期 推导出 年纪

-   连通性相关属性推导 (connectivity-based attribute derivation)

    通过相连的类来推导节点/边的属性

    ![1569219416375](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/9/23/e433dba958df4449e9ff1bdea4e438cce62d239a.png)

-   改变边的方向性 (changing edge directionality)

    有向边的转换，或者把有向边转化为无向边。

# 系统设计

![1569219457269](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/9/23/6dd3d6447b77277190099538eb06e777857b0475.png)

其中包含三大 View：

-   Network Model View: 展示节点/边之间的关系，

-   Attribute View: 展示节点/边的属性，执行属性相关操作

-   Network Sample View: 展现网络现状的 preview

### 网络模型视图（Network Model View）

![1569219498059](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/9/23/a3e90cfb5f2ef3395fae47c9a9d57dab8f40e795.png)

节点用圆形编码，类别用菱形编码，数量用数字表示，边的一节保持水平（保证 label 可读）。

它提供了包括以下几种的操作：

-   连接/断开 (connecting or disconnecting)
-   点边转化 (converting between nodes and edges)
-   边投影 (edge projection)
-   改变边的方向性 (changing edge directionality)

### 属性视图 (Attribute View)

![1569219601816](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/9/23/7cb4a7e04332f193a96029b95654d100ecf394fa.png)

提供了很多关于属性的操作，包括：

-   属性提升 (promoting attributes)
-   切面 (faceting)
-   属性过滤 (filtering by attributes)
-   连通性过滤 (connectivity-based filtering)
-   类内属性推导 (deriving in-class attributes)
-   连通性相关属性推导 (connectivity-based attribute derivation)

### 网络采样视图 (Network Sample View)

用采样后的网络，展示当前状态。其中采用了深度优先采样方法：A Survey and Taxonomy of Graph Sampling。作者对该方法做了一些改进，平衡了不同类之间的采样，用户可以自由选择节点/边作为种子。

### 操作视图 (Operation Views)

#### Connection Support Interface

主要用于提供连接操作。

![1569219995252](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/9/23/41ac17fcde21252e5ba551d308ba57c14fb26a1a.png)

它会计算一个分数，来推荐哪些关系相连可以作为边。

$$
\operatorname{score}_{n, m}=\sum_{c l a s s \in\{s r c, t r g\}} \frac{\sum_{i t e m \in \text {class}}\left\{\frac{1}{d e g_{n, m}(\text {item})},\text { if } \operatorname{deg}_{n, m}(\text {item})>0\right.}{|class|}
$$

这个分数，会让那种有一对一匹配的关系有更高的分数。当如果两类节点能通过某种关系进行 1 对 1 匹配，没有多也没有少时，这个关系的 score 将会是 2；而如果没有任何的匹配，这种关系的 score 将会是-2。

#### Path-Based Operations

![1569220095085](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2019/9/23/7aebaae16b48d66fe99f8daf1665f8e74add188d.png)

主要提供以下操作：

-   边投影 (edge projection)
-   连通性过滤 (connectivity-based filtering)
-   连通性相关属性推导 (connectivity-based attribute derivation)
