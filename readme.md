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


