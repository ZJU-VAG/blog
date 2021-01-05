# 浙江大学可视分析小组博客

[国内镜像](http://zjuvag.gitee.io/blog) | [国际镜像](http://zjuvag.org/blog)

## 如何在本地初始化？

1. 你需要有一个 github 账户，并且需要成为 ZJUVAG github 小组的成员；
2. 添加之后，进行项目的 clone：`git clone git@github.com:ZJUVAG/blog.git`
3. 当 clone 到本地后，进行 `npm install` 操作
4. 对本地的一些文件和配置进行修改

   - 对 `node_modules/hexo-generator-author/index.js` 进行修改：

   ```javascript
   // 原文件中：
   hexo.extend.filter.register("template_locals", function (locals) {
     if (typeof locals.site.authors === "undefined") {
       locals.site.authors = locals.site.posts
         .map((post) => post.author)
         .unique();
     }
   });

   // 改为如下：
   hexo.extend.filter.register("template_locals", function (locals) {
     if (typeof locals.site.authors === "undefined") {
       const posts = locals.site.posts;
       locals.site.authors = locals.site.posts
         .map((post) => post.author)
         .unique()
         .map((author) => ({
           name: author,
           posts: posts.find({
             author,
           }),
         }));
     }
   });
   ```

   - 对 `node_modules/hexo-renderer-kramed/lib/renderer.js` 进行修改：

   ```javascript
   // 原文件中
   function formatText(text) {
     // Fit kramed's rule: $$ + \1 + $$
     return text.replace(/`\$(.*?)\$`/g, "$$$$$1$$$$");
   }

   // 改为如下：
   function formatText(text) {
     return text;
   }
   ```

   - 对 `node_modules/hexo-renderer-mathjax/mathjax.html` 进行修改，最后一个 script 标签改为：

   ```html
   <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.1/MathJax.js?config=TeX-MML-AM_CHTML"></script>
   ```

   - 对 `node_modules/kramed/lib/rules/inline.js` 进行修改：

   ```javascript
   escape: /^\\([\\`*{}\[\]()#$+\-.!_>])/,
   // 改为
   escape: /^\\([`*\[\]()# +\-.!_>])/,


   em: /^\b_((?:__|[\s\S])+?)_\b|^\*((?:\*\*|[\s\S])+?)\*(?!\*)/,
   // 改为
   em: /^\*((?:\*\*|[\s\S])+?)\*(?!\*)/,
   ```

## 如何添加新的博客？

1. 在[source/\_posts](https://github.com/ZJU-VAG/blog/tree/master/source/_posts)下面添加一个新的 markdown 文件，命名方式参考已有的文档（20xx-mm-dd-title.md）；
2. 文档的头部应该包含以下内容（下面这个案例仅供参考，具体可以参考已有的文档），这些信息会被识别为文章的基本信息：

   ```markdown
   ---
   title: "Wavelet-based Visual Analysis of Dynamic Networks"
   tags: ["论文评述", "报告"]
   date: 2019-01-07
   author: 潘嘉铖
   mail: panjiacheng@zju.edu.cn
   mathjax: true
   ---
   ```

3. 当在 `source/_posts` 中添加完新的文档后，执行以下命令，能完成自动部署：

   ```bash
   npm run deploy
   ```
