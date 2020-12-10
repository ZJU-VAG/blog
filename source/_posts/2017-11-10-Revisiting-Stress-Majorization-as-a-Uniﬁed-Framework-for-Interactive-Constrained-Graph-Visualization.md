---
title: "Revisiting Stress Majorization as a Uniﬁed Framework for Interactive Constrained Graph Visualization"
tags: ["论文评述", "报告"]
date: 2017-11-10
author: 王叙萌
mail: wangxumeng@zju.edu.cn
mathjax: true
---

论文：Revisiting Stress Majorization as a Uniﬁed Framework for Interactive Constrained Graph Visualization

作者：Yunhai Wang, Yanyan Wang, Yinqi Sun, Lifeng Zhu, Kecheng Lu, Chi-Wing Fu, Michael Sedlmair, Oliver Deussen, and Baoquan Chen

发表：2017 TVCG (InfoVis)

## 动机

1. 图数据应用广泛，需求多样，难以适应

2. 没有方法既美观又易读，还能适用于大规模数据

## 贡献

1. 改进模型：改进 stress majorization 模型，将其重新构造成一个可自定义约束的通用可视化框架
2. 使用方法：给出结合三类约束优化布局的方法
3. 相关系统：支持 GPU 加速，可交互探索 10K 节点，90K 边的图形布局

## 相关工作

1. Stress model [Kamada 1989]：

[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/11/QQ%E5%9B%BE%E7%89%8720171110154712.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/11/QQ图片20171110154712.png)

2. 约束图布局：[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/11/QQ%E5%9B%BE%E7%89%8720171110155000.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/11/QQ图片20171110155000.png)

3. 交互探索（Focus+context）：
    - 力引导图直接放大
    - 细节图加约束
    - 考虑 DOI (degree of interest)
    - 用鱼眼

## 方法：

1. 核心方法：[![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/11/QQ%E5%9B%BE%E7%89%8720171110155229.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/11/QQ图片20171110155229.png)

2. 展开并写成矩阵形式：
   [![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/11/QQ%E5%9B%BE%E7%89%8720171110155454.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/11/QQ图片20171110155454.png)

3. 无约束例子
   [![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/11/QQ%E5%9B%BE%E7%89%8720171110155622.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/11/QQ图片20171110155622.png)

4. 迭代过程：

    - 优化方向（D-step）：基于原有方向和新计算的 d 计算矩阵 D
    - 计算坐标（P-step）：基于 LX=JD 计算矩阵 X

5. 考虑用户定义约束（如集合分离、突出结构等）：
   [![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/11/QQ%E5%9B%BE%E7%89%8720171110160048.png)](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/11/QQ图片20171110160048.png)

6. 三种约束：

    - 直接约束

        ![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/11/QQ%E5%9B%BE%E7%89%8720171110160320.png)

    - 度量约束

        ![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/11/QQ%E5%9B%BE%E7%89%8720171110160548.png)

    - 形状约束

        ![img](http://www.cad.zju.edu.cn/home/vagblog/wp-content/uploads/2017/11/QQ%E5%9B%BE%E7%89%8720171110160709.png)

## 评估：

1. 对比方法：
    - 增量添加约束的 IPSep
    - 可拓展多功能的 SV
    - 本方法（不同用户约束权重）
2. 对比属性：
    - Stress Error (SE)
    - Vertical Edge (VE)
    - The number of edge crossings (#EC)
3. 结果：效果远优于其他方法。在处理大量数据时速度有优势。

## 总结：

1. 未来工作：

    - 探究更多的基于形状的约束
    - 自动生成权重
    - 提高性能，适应大图

2. 优点
    - 老问题，新思路
    - 从模型到方法到系统一条龙
    - 方法通用，评估全面
