# 博客搬运说明

新的博客，需要用markdown格式进行编写，希望各位去参考markdown的编写格式。在搬运博客的过程中，**务必把这篇博客当做自己的博客进行搬运**，我会在最后做个审查，保证博客搬运的质量。

如果你不熟悉markdown，请务必学习一下markdown的基本格式：[认识与入门Markdown - 少数派](https://sspai.com/post/25137)

推荐markdown的工具：typora；

在博客搬运的过程中有几个点需要注意：

1. 博客的markdown文件请命名为像如下格式：

   `2012-02-15-Chinagraph’2012征文通知.md`

2. 在博客的最上方，包含了这篇博客的基本信息

   ```
   ---
   title: "Vol2velle Printable Interactive Volume Visualization 可打印的交互式体可视化"
   tags: ["论文评述", "报告"]
   date: 2016-02-29
   author: 潘嘉铖
   mathjax: true
   ---
   ```

   注意！！这里一定要写为`---`，**三**个短线

   以上内容中的标点符号，应该全是英文的标点符号，**切勿用中文的标点符号**

   英文的标点后面请加空格；中英文之间加入空格；

   - `title`是博客的名称，请务必加上**引号**

   - 在tag里面需要包含它的类别（因为有些同学写的博客没有勾选分类目录，可能直接被识别为“其他”，请纠正它，一般组会报告标记成`["论文评述", "报告"]`）：

     - 业界新闻
     - 主题报告
     - 学术交流
     - 学术会议
     - 报告
     - 新闻
     - 活动
     - 论文评述
     - 通知
     - 随感

     ps: 这个类别可以在标题上面找到：

     ![1561980353316](https://jackie-image.oss-cn-hangzhou.aliyuncs.com/19-07-01/1561980353316.png)

    - `date`表示这篇博客的发表时间，原始的博客里面应该也有

    - `author`表示这篇博客是谁写的（最好改成中文），如果这个人是admin，那就还是admin即可

    - 如果这篇博客直接跳转到我（潘嘉铖）的博客上了，请直接找我要markdown文件，你再做修改即可；

3. **重要**，接下去也是最麻烦的一步，需要你重新去排版整个markdown文件（为了保证搬运后渲染出来的质量）

   1. 章节标题：每一个小结都可能有一个小标题，请使用`##`作为第一级标题，`###`作为第二级标题以此类推；

   2. 图片：图片可以直接复制，然后到typora中黏贴就能生成；如果图片有问题，请自行联系作者；假如作者已经毕业就算了；

   3. 在markdown里面，没有（1）（2）这样的序号的，请也不要再使用，Markdown里面，直接用`1. `，`2. `这样的序号来表示就行了，示例如下：

     ```
     1. 示例一
     	1. 示例1.1
     	2. 示例1.2
     2. 示例二
     ```

     非有序的序号请使用：

     ```
     - 非有序示例一
     - 非有序示例二
     	- 非有序示例2.1
     	- 非有序示例2.2
     ```

   4. 有些老博客，可能用的是`1)`这样的序号来标志顺序，请在markdown中改为`1. `，`2.`等等；
     如果标志了序号，请注意不要在连续两个序号段落中间留空行，像下面这样会出错：

     ![](http://jackie-image.oss-cn-hangzhou.aliyuncs.com/19-07-02/Snipaste_2019-07-02_16-53-16.jpg)

   5. 如果博客中有公式，希望能将其转为mathjax格式的公式（typora中，在偏好设置中打开【内联公式】的选项）；推荐一个方便的工具（[mathpix](https://mathpix.com/)），可以直接通过截图来产生latex代码；

      行内的公式请使用`$xxx$`，行间的公式请使用：

        ```
        $$
        xxxxxx
        $$
      
        ```

       比如下面这个公式，可以直接截图生成：：
      ![1561975156111](https://jackie-image.oss-cn-hangzhou.aliyuncs.com/19-07-01/1561975156111.png)

      ```
      $$
      H(Y | X)=\sum_{x \in \mathcal{X}, y \in \mathcal{Y}} p(x, y) \log \left(\frac{p(x)}{p(x, y)}\right)
      $$
      ```
      效果如下：

   $$
   H(Y | X)=\sum_{x \in \mathcal{X}, y \in \mathcal{Y}} p(x, y) \log \left(\frac{p(x)}{p(x, y)}\right)
   $$






# 博客配置

我对小涛的 aircloud 主题进行了魔改，所以里面有很多东西都改变了

1. 增加了`hexo-generator-author`，需要对其 index.js 做一些修改：

   ```javascript
   hexo.extend.filter.register('template_locals', function (locals) {
       if (typeof locals.site.authors === 'undefined') {
           const posts = locals.site.posts;
           locals.site.authors = locals.site.posts.map(post => post.author).unique().map(author => ({
               name: author,
               posts: posts.find({
                   author
               })
           }));;
       }
   });
   ```


