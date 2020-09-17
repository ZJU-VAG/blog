---
title: "Poemage: Visualizing the Sonic Topology of a Poem"
tags: ["论文评述"]
date: 2015-12-25
author: 王叙萌
mail: wangxumeng@zju.edu.cn
mathjax: true
---

论文：Poemage: Visualizing the Sonic Topology of a Poemcadhyz

作者：Nina McCurdy, Julie Lein, Katharine Coles, Miriah Meyer

会议：TVCG 2015

Poemage 是可视化与抒发万千情感的诗歌紧密结合的产物。它用诗歌一样浪漫的表达方式将诗歌韵律的拓扑结构展现在我们面前。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/12/%E5%9B%BE%E7%89%871.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/12/图片1.png)

作者在与诗人学者不断交流之后，得出了对方在研究诗歌的时候比较关注的三个元素：

-诗的空间：国外的诗不想我国的古诗有五言七律等固定格式，它们允许在诗词间加入空行和空格来增进情感的表达，所以在可视化界面中保留这一元素很重要。

-诗的韵律：探测每个单词属于什么韵律的方法可以在本篇文章一作的另一篇文章 RhymeDesign 中找到。

-诗的韵律拓扑：与之前的诗歌韵律可视化将每个音节做为一个独立的元素不同，Poemage 将一个单词视作一个节点，具有相同韵律视作一种关系，从而得到了拓扑结构。

整个系统就是围绕着如何展示这三个元素而展开的。

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/12/%E5%9B%BE%E7%89%872.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2015/12/图片2.png)

之所以说这篇文章的表达方式很浪漫是因为，作者将诗视作一个流，每一个代表韵律关系的线就是一个细流（做出这种蜿蜒的效果不仅是为了喻义，也是因为作者为了避免有边经过与其无关的点而对使用者产生干扰，故在相近的空格处加上了控制点），它们穿梭在整个流之中。而包含了多种韵律的单词会有许多细流经过，那么它就处在湍流之中。除此之外，作者将韵律拓扑涉及的单词用椭圆形高亮了出来，她们认为，这就像是往水流中扔鹅卵石一样。
