---
title: "Augmenting Static Visualizations with PapARVis Designer"
tags: ["论文评述", "报告"]
date: 2020-08-27
author: 温圳
mail: 498621483@qq.com
mathjax: true
---

# 基本信息

-   **论文：** Augmenting Static Visualizations with PapARVis Designer
-   **作者：** Chen, Zhutian, Wai Tong, Qianwen Wang, Benjamin Bach, and Huamin Qu
-   **来源：** ACM CHI 2020
    \_![image.png](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/9/1/8c6e6486070e6f1999e79ed25ca063c14c8f569b.png)

# 介绍

利用 AR 增强可视化，可以将物理世界和数字世界结合展现，Figure 1 中展示了现实和增强后的效果。PapARVis Designer 是一个设计 AR 增强静态可视化的创作环境。

## 设计标准

1. 图形一致性
1. 可读性
1. 合法性：增强前后，相同的视觉数值对应相同的数据。Figure 2b 中增强前后相同数据的对应弧长发生了变化，这是不合法的。

![image.png](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/9/1/c6a4b1a0a5798b8496b01f57c64821640ce8dafd.png)

## 主要特性

1. AR 预览：在桌面平台上预览 AR 效果
1. 校验器：辅助设计与 debug

## 设计目标

1. 只使用一个工具完成可视化的设计、测试、debug、发布。
1. 可以在设计平台上预览可视化，避免来回切换设备。
1. 提供自动设计辅助。

## 增强模式

![image.png](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/9/1/9303d3d217855243034f05a1d61173da668631ce.png)

如上图所示，有四种增强模式：

1. **Extended View**：同一视图、相同视觉编码（Figure 3a）
1. **Composite View**：同一视图、不同视觉编码（Figure 3b）
1. **Small Multiple**：不同视图、相同视觉编码（Figure 3c）
1. **Multiple View**：不同视图、不同视觉编码（Figure 3d）

## 使用场景

Figure 7 中，a - d 是 k 的增强结果；e - j 展示了多种不同的增强方式，子图中是静态可视化。

Figure 7e 中应用比较有趣，是在一张统计所有学生成绩分布的图表上，利用 AR 显示个人成绩在分布中的位置，很好地展示了个人信息，又保护了个人隐私。
![image.png](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/9/1/a355a9f85b46fe9a94c8cd17d3c879905e213059.png)

# 具体设计

## WorkFlow

![image.png](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/9/1/9667e14e724207ee1f5a00eb406a44e08ddb1625.png)
在原有的静态可视化 $$V_s$$  的基础上，设计增强虚拟可视化 $$V_v$$，利用 AR 将两者结合成为可视化 $$V_{AR}$$  展示出来。
![image.png](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/9/1/4091105889d03853e4a523fdecada76421e1b622.png)
系统主要包含三个模块：

1. **VegaAR Editor**：基于 [Vega Editor](https://github.com/vega/editor)，用于创建 $V_s$  可视化，并在 ar block 中定义 $V_v$。发布时将内容上传到 SpecHub，生成二维码链接。
1. **SpecHub**：部署在云端，用于接收和托管 VegaAR Editor 上传的内容，生成 $V_s$  参考图像用于 AR 识别，解析 $V_v$  用于生成 AR 可视化。
1. **AR Viewer**：通过扫描二维码，获取 SpecHub 上相应的配置文件，查看 AR 增强可视化效果，实现在 iOS、Android、Web 平台上。

## AR 预览

在 Vega Editor 的基础上添加 ar block 配置，用于定义 $V_v$，并提供预览效果。

$V_v$  的物理空间由 Vega 定义，与 $V_s$相关。

## 校验器

![image.png](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/9/1/4c32a5a5519682bf5940b3fb4364ba391296486f.png)

检测原始数据与合并增强数据后的数据，经过数据变换后，原始数据对应的数值是否保持不变。如果不变，证明增强方式合法。Figure 6 中是对 Figure 4c 中发生的合法性错误的提示。

# 实验结果

邀请 12 位没有 AR 经验的可视化设计者，进行了分组实验。

## 测试流程

Base Mode：移除 AR 预览和校验器特性，作为 baseline。

Pro Mode：完整版 PapARVis Designer。

![image.png](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/9/1/0816d03f07899eda8fab320c649056dda5e2a281.png)

## 测试结果

![image.png](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/9/1/3966aa377656c2dab11ff998dd2a805f54cff69f.png)
![image.png](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/9/1/5bb2faa202022e72cd087eb35339d73fb342cad6.png)
![image.png](http://www.cad.zju.edu.cn/home/vagblog/images/photo_bed/2020/9/1/f0e352ba5875f3bc5ac6dde386a6f1e07daeeb51.png)

## 实验总结

1. PapARVis Designer 的 AR 模块类似于一个黑盒部署在服务器上，设计者有时无法判断错误出在 AR 模块上，还是自己的设计上。
1. 设计者在设计时容易混淆现实可视化和虚拟可视化。如果能直接在原场景上进行设计可能更好。
1. 校验器检测到错误时的提示可能被忽视，无法帮助到设计者 debug。把提示变成类似编译器编译错误的强制警告可能更好。
1. 参与者们认为，这项技术可以应用于公共展示中，例如信息板、公园地图、互动性艺术品等。

# 总结 & 心得

PapARVis Designer 的本质还是在桌面端做静态可视化设计，然后通过 AR 展现出来。首先，使用起来需要一定的 Vega 或 D3 基础。另外，当原始数据无法获取或数据量较大时，手动创建可视化非常困难，难以应用在增强他人的可视化上。

当然 PapARVis Designer 也有很多优点，可以用来克服现实可视化的空间限制，在旧的可视化上展示新数据，拓展可视化的细节，做隐私保护，显示个人信息等。

另一方面，相较于传统现实的可视化，AR 是虚拟的可视化。它可以用来辅助增强现实的可视化，可以打破平面的限制拓展到 3D 层面，一定程度上给人更直观的感受和更强的代入感。除了本文中 2D 静态的 AR 可视化，3D AR、交互动态 AR、场景适应的 AR 也是 AR 可视化可以研究的方向。
